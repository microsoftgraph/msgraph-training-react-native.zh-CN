<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="5d4e4-101">在本练习中，将把 Microsoft Graph 合并到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="5d4e4-102">对于此应用程序，您将使用 [Microsoft Graph JavaScript 客户端库](https://github.com/microsoftgraph/msgraph-sdk-javascript) 对 microsoft graph 进行调用。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="5d4e4-103">从 Outlook 获取日历事件</span><span class="sxs-lookup"><span data-stu-id="5d4e4-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="5d4e4-104">在本节中，您将扩展 `GraphManager` 类以添加一个函数，以获取当前星期的用户事件，并更新 `CalendarScreen` 以使用这些新函数。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-104">In this section you will extend the `GraphManager` class to add a function to get the user's events for the current week and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="5d4e4-105">打开 **GraphTutorial/graph/GraphManager** 文件，并将以下方法添加到 `GraphManager` 类中。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-105">Open the **GraphTutorial/graph/GraphManager.tsx** file and add the following method to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="GetCalendarViewSnippet":::

    > [!NOTE]
    > <span data-ttu-id="5d4e4-106">考虑中的代码 `getCalendarView` 执行的操作。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-106">Consider what the code in `getCalendarView` is doing.</span></span>
    >
    > - <span data-ttu-id="5d4e4-107">将调用的 URL 为 `/v1.0/me/calendarView` 。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-107">The URL that will be called is `/v1.0/me/calendarView`.</span></span>
    > - <span data-ttu-id="5d4e4-108">`header`函数将 `Prefer: outlook.timezone` 标头添加到请求，从而导致响应中的时间位于用户的首选时区中。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-108">The `header` function adds the `Prefer: outlook.timezone` header to the request, causing the times in the response to be in the user's preferred time zone.</span></span>
    > - <span data-ttu-id="5d4e4-109">`query`函数添加 `startDateTime` 和 `endDateTime` 参数，定义日历视图的时间窗口。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-109">The `query` function adds the `startDateTime` and `endDateTime` parameters, defining the window of time for the calendar view.</span></span>
    > - <span data-ttu-id="5d4e4-110">`select`函数将为每个事件返回的字段限制为仅应用程序实际使用的字段。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-110">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="5d4e4-111">`orderby`函数按开始时间对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-111">The `orderby` function sorts the results by the start time.</span></span>
    > - <span data-ttu-id="5d4e4-112">`top`函数将结果限制为前50个事件。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-112">The `top` function limits the results to the first 50 events.</span></span>

1. <span data-ttu-id="5d4e4-113">打开 **GraphTutorial/views/CalendarScreen** 并将其全部内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-113">Open the **GraphTutorial/views/CalendarScreen.tsx** and replace its entire contents with the following code.</span></span>

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      FlatList,
      Modal,
      Platform,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import moment from 'moment-timezone';
    import { findOneIana } from 'windows-iana';

    import { UserContext } from '../UserContext';
    import { GraphManager } from '../graph/GraphManager';

    const Stack = createStackNavigator();
    const CalendarState = React.createContext<CalendarScreenState>({
      loadingEvents: true,
      events: []
    });

    type CalendarScreenState = {
      loadingEvents: boolean;
      events: MicrosoftGraph.Event[];
    }

    // Temporary JSON view
    const CalendarComponent = () => {
      const calendarState = React.useContext(CalendarState);

      return (
        <View style={styles.container}>
          <Modal visible={calendarState.loadingEvents}>
            <View style={styles.loading}>
              <ActivityIndicator
                color={Platform.OS === 'android' ? '#276b80' : undefined}
                animating={calendarState.loadingEvents}
                size='large' />
            </View>
          </Modal>
          <ScrollView>
            <Text>{JSON.stringify(calendarState.events, null, 2)}</Text>
          </ScrollView>
        </View>
      );
    }

    export default class CalendarScreen extends React.Component {
      static contextType = UserContext;

      state: CalendarScreenState = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const tz = this.context.userTimeZone || 'UTC';
          // Convert user's Windows time zone ("Pacific Standard Time")
          // to IANA format ("America/Los_Angeles")
          // Moment.js needs IANA format
          const ianaTimeZone = findOneIana(tz);

          // Get midnight on the start of the current week in the user's
          // time zone, but in UTC. For example, for PST, the time value
          // would be 07:00:00Z
          const startOfWeek = moment
            .tz(ianaTimeZone!.valueOf())
            .startOf('week')
            .utc();

          const endOfWeek = moment(startOfWeek)
            .add(7, 'day');

          const events = await GraphManager.getCalendarView(
            startOfWeek.format(),
            endOfWeek.format(),
            tz);

          this.setState({
            loadingEvents: false,
            events: events.value
          });
        } catch(error) {
          Alert.alert(
            'Error getting events',
            JSON.stringify(error),
            [
              {
                text: 'OK'
              }
            ],
            { cancelable: false }
          );

        }
      }

      render() {
        return (
          <CalendarState.Provider value={this.state}>
            <Stack.Navigator>
              <Stack.Screen name='Calendar'
                component={ CalendarComponent }
                options={{
                  headerShown: false
                }} />
            </Stack.Navigator>
          </CalendarState.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      loading: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
      },
      eventItem: {
        padding: 10
      },
      eventSubject: {
        fontWeight: '700',
        fontSize: 18
      },
      eventOrganizer: {
        fontWeight: '200'
      },
      eventDuration: {
        fontWeight: '200'
      }
    });
    ```

<span data-ttu-id="5d4e4-114">您现在可以运行应用程序，登录，然后点击菜单中的 " **日历** " 导航项。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-114">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="5d4e4-115">您应该会看到应用程序中的事件的 JSON 转储。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-115">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="5d4e4-116">显示结果</span><span class="sxs-lookup"><span data-stu-id="5d4e4-116">Display the results</span></span>

<span data-ttu-id="5d4e4-117">现在，您可以将 JSON 转储替换为以用户友好的方式显示结果的内容。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="5d4e4-118">在本节中，您将添加 `FlatList` 到日历屏幕以呈现事件。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-118">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="5d4e4-119">将以下方法添加 **above** 到 `CalendarScreen` 类声明的上方。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-119">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/CalendarScreen.tsx" id="ConvertDateSnippet":::

1. <span data-ttu-id="5d4e4-120">`ScrollView`将方法中的替换 `CalendarComponent` 为以下项。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-120">Replace the `ScrollView` in the `CalendarComponent` method with the following.</span></span>

    ```typescript
    <FlatList data={calendarState.events}
      renderItem={({item}) =>
        <View style={styles.eventItem}>
          <Text style={styles.eventSubject}>{item.subject}</Text>
          <Text style={styles.eventOrganizer}>{item.organizer.emailAddress.name}</Text>
          <Text style={styles.eventDuration}>
            {convertDateTime(item.start.dateTime)} - {convertDateTime(item.end.dateTime)}
          </Text>
        </View>
      } />
    ```

1. <span data-ttu-id="5d4e4-121">运行应用程序，登录，然后点击 " **日历** " 导航项。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-121">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="5d4e4-122">您应该会看到事件列表。</span><span class="sxs-lookup"><span data-stu-id="5d4e4-122">You should see the list of events.</span></span>

    ![事件表的屏幕截图](./images/calendar-list.png)
