<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ca3ee-101">在本练习中，将把 Microsoft Graph 合并到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="ca3ee-102">对于此应用程序，您将使用[Microsoft Graph JavaScript 客户端库](https://github.com/microsoftgraph/msgraph-sdk-javascript)对 microsoft graph 进行调用。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="ca3ee-103">从 Outlook 获取日历事件</span><span class="sxs-lookup"><span data-stu-id="ca3ee-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="ca3ee-104">在本节中，您将扩展`GraphManager`类以添加一个函数，以获取用户的事件并更新`CalendarScreen`以使用这些新函数。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-104">In this section you will extend the `GraphManager` class to add a function to get the user's events and update `CalendarScreen` to use these new functions.</span></span>

1. <span data-ttu-id="ca3ee-105">打开**GraphTutorial/graph/GraphManager**文件，并将以下方法添加到`GraphManager`类中。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-105">Open the **GraphTutorial/graph/GraphManager.js** file and add the following method to the `GraphManager` class.</span></span>

    ```js
    static getEvents = async() => {
      // GET /me/events
      return graphClient.api('/me/events')
        // $select='subject,organizer,start,end'
        // Only return these fields in results
        .select('subject,organizer,start,end')
        // $orderby=createdDateTime DESC
        // Sort results by when they were created, newest first
        .orderby('createdDateTime DESC')
        .get();
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="ca3ee-106">考虑中`getEvents`的代码执行的操作。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-106">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="ca3ee-107">将调用的 URL 为`/v1.0/me/events`。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-107">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="ca3ee-108">`select`函数将为每个事件返回的字段限制为仅应用程序实际使用的字段。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-108">The `select` function limits the fields returned for each events to just those the app will actually use.</span></span>
    > - <span data-ttu-id="ca3ee-109">`orderby`函数按其创建日期和时间对结果进行排序，最新项目最先开始。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-109">The `orderby` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="ca3ee-110">打开**GraphTutorial/views/CalendarScreen**并将其全部内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-110">Open the **GraphTutorial/views/CalendarScreen.js** and replace its entire contents with the following code.</span></span>

    ```JSX
    import React from 'react';
    import {
      ActivityIndicator,
      FlatList,
      Modal,
      ScrollView,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { Icon } from 'react-native-elements';
    import { GraphManager } from '../graph/GraphManager';

    export default class CalendarScreen extends React.Component {
      static navigationOptions = ({navigation}) => {
        return {
          title: 'Calendar',
          headerLeft: <Icon iconStyle={{ marginLeft: 10, color: 'white' }} size={30} name="menu" onPress={navigation.toggleDrawer} />
        };
      }

      state = {
        loadingEvents: true,
        events: []
      };

      async componentDidMount() {
        try {
          const events = await GraphManager.getEvents();

          this.setState({
            loadingEvents: false,
            events: events.value
          });
        } catch(error) {
          alert(error);
        }
      }

      // Temporary JSON view
      render() {
        return (
          <View style={styles.container}>
            <Modal visible={this.state.loadingEvents}>
              <View style={styles.loading}>
                <ActivityIndicator animating={this.state.loadingEvents} size='large' />
              </View>
            </Modal>
            <ScrollView>
              <Text>{JSON.stringify(this.state.events, null, 2)}</Text>
            </ScrollView>
          </View>
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

<span data-ttu-id="ca3ee-111">您现在可以运行应用程序，登录，然后点击菜单中的 "**日历**" 导航项。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-111">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="ca3ee-112">您应该会看到应用程序中的事件的 JSON 转储。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-112">You should see a JSON dump of the events in the app.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="ca3ee-113">显示结果</span><span class="sxs-lookup"><span data-stu-id="ca3ee-113">Display the results</span></span>

<span data-ttu-id="ca3ee-114">现在，您可以将 JSON 转储替换为以用户友好的方式显示结果的内容。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-114">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="ca3ee-115">在本节中，您将添加`FlatList`到日历屏幕以呈现事件。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-115">In this section, you will add a `FlatList` to the calendar screen to render the events.</span></span>

1. <span data-ttu-id="ca3ee-116">打开**GraphTutorial/graph/GraphManager**文件，并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-116">Open the **GraphTutorial/graph/GraphManager.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import moment from 'moment';
    ```

1. <span data-ttu-id="ca3ee-117">将以下方法添加\*\*\*\* 到类`CalendarScreen`声明的上方。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-117">Add the following method **above** the `CalendarScreen` class declaration.</span></span>

    ```js
    convertDateTime = (dateTime) => {
      const utcTime = moment.utc(dateTime);
      return utcTime.local().format('MMM Do H:mm a');
    };
    ```

1. <span data-ttu-id="ca3ee-118">将`render`方法`ScrollView`中的替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-118">Replace the `ScrollView` in the `render` method with the following.</span></span>

    ```JSX
    <FlatList data={this.state.events}
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

1. <span data-ttu-id="ca3ee-119">运行应用程序，登录，然后点击 "**日历**" 导航项。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-119">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="ca3ee-120">您应该会看到事件列表。</span><span class="sxs-lookup"><span data-stu-id="ca3ee-120">You should see the list of events.</span></span>

    ![事件表的屏幕截图](./images/calendar-list.png)
