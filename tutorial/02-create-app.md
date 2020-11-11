<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9ee57-101">首先创建新的响应本机项目。</span><span class="sxs-lookup"><span data-stu-id="9ee57-101">Begin by creating a new React Native project.</span></span>

1. <span data-ttu-id="9ee57-102">在您要在其中创建项目的目录中 (CLI) 打开命令行界面。</span><span class="sxs-lookup"><span data-stu-id="9ee57-102">Open your command line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="9ee57-103">运行以下命令，运行 [响应本机的 cli](https://github.com/facebook/react-native) 工具并创建新的响应本机项目。</span><span class="sxs-lookup"><span data-stu-id="9ee57-103">Run the following command to run the [react-native-cli](https://github.com/facebook/react-native) tool and create a new React Native project.</span></span>

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. <span data-ttu-id="9ee57-104">**可选：** 通过运行项目验证您的开发环境是否已正确配置。</span><span class="sxs-lookup"><span data-stu-id="9ee57-104">**Optional:** Verify that your development environment is configured correctly by running the project.</span></span> <span data-ttu-id="9ee57-105">在 CLI 中，将目录更改为刚创建的 **GraphTutorial** 目录，并运行下列命令之一。</span><span class="sxs-lookup"><span data-stu-id="9ee57-105">In your CLI, change the directory to the **GraphTutorial** directory you just created, and run one of the following commands.</span></span>

    - <span data-ttu-id="9ee57-106">对于 iOS： `npx react-native run-ios`</span><span class="sxs-lookup"><span data-stu-id="9ee57-106">For iOS: `npx react-native run-ios`</span></span>
    - <span data-ttu-id="9ee57-107">对于 Android：启动 Android 仿真程序实例并运行 `npx react-native run-android`</span><span class="sxs-lookup"><span data-stu-id="9ee57-107">For Android: Launch an Android emulator instance and run `npx react-native run-android`</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="9ee57-108">安装依赖项</span><span class="sxs-lookup"><span data-stu-id="9ee57-108">Install dependencies</span></span>

<span data-ttu-id="9ee57-109">在继续之前，请安装稍后将使用的一些其他依赖项。</span><span class="sxs-lookup"><span data-stu-id="9ee57-109">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="9ee57-110">[响应-导航](https://reactnavigation.org) 以处理应用程序中的视图之间的导航。</span><span class="sxs-lookup"><span data-stu-id="9ee57-110">[react-navigation](https://reactnavigation.org) to handle navigation between views in the app.</span></span>
- <span data-ttu-id="9ee57-111">[响应-本机-笔势-处理程序](https://github.com/kmagiera/react-native-gesture-handler)、 [响应本机安全区域上下文](https://github.com/th3rdwave/react-native-safe-area-context)、 [响应本机屏幕](https://github.com/kmagiera/react-native-screens)、 [响应本机](https://github.com/kmagiera/react-native-reanimated)恢复以及响应导航所需的 [屏蔽视图](https://github.com/react-native-community/react-native-masked-view) 。</span><span class="sxs-lookup"><span data-stu-id="9ee57-111">[react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler), [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context), [react-native-screens](https://github.com/kmagiera/react-native-screens), [react-native-reanimate](https://github.com/kmagiera/react-native-reanimated), and [masked-view](https://github.com/react-native-community/react-native-masked-view) required by react-navigation.</span></span>
- <span data-ttu-id="9ee57-112">[响应-本机元素](https://reactnativeelements.com/docs/) 和 [响应本机向量图标](https://github.com/oblador/react-native-vector-icons) ，以便为 UI 提供图标。</span><span class="sxs-lookup"><span data-stu-id="9ee57-112">[react-native-elements](https://reactnativeelements.com/docs/) and [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) to provide icons for the UI.</span></span>
- <span data-ttu-id="9ee57-113">[响应-本机-](https://github.com/FormidableLabs/react-native-app-auth) 对处理身份验证和令牌管理的应用程序身份验证。</span><span class="sxs-lookup"><span data-stu-id="9ee57-113">[react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) to handle authentication and token management.</span></span>
- <span data-ttu-id="9ee57-114">用于为令牌提供存储的[异步存储](https://react-native-async-storage.github.io/async-storage/docs/install)。</span><span class="sxs-lookup"><span data-stu-id="9ee57-114">[async-storage](https://react-native-async-storage.github.io/async-storage/docs/install) to provide storage for tokens.</span></span>
- <span data-ttu-id="9ee57-115">[datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) 将日期和时间选取器添加到 UI。</span><span class="sxs-lookup"><span data-stu-id="9ee57-115">[datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) to add date and time pickers to the UI.</span></span>
- <span data-ttu-id="9ee57-116">处理日期和时间的分析和比较的[时间](https://momentjs.com)。</span><span class="sxs-lookup"><span data-stu-id="9ee57-116">[moment](https://momentjs.com) to handle parsing and comparison of dates and times.</span></span>
- <span data-ttu-id="9ee57-117">用于将 Windows 时间区域转换为 IANA 格式的[windows-iana](https://github.com/rubenillodo/windows-iana) 。</span><span class="sxs-lookup"><span data-stu-id="9ee57-117">[windows-iana](https://github.com/rubenillodo/windows-iana) for translating Windows time zones to IANA format.</span></span>
- <span data-ttu-id="9ee57-118">microsoft graph-用于调用 Microsoft Graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。</span><span class="sxs-lookup"><span data-stu-id="9ee57-118">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="9ee57-119">在响应本机项目的根目录中打开您的 CLI。</span><span class="sxs-lookup"><span data-stu-id="9ee57-119">Open your CLI in the root directory of your React Native project.</span></span>
1. <span data-ttu-id="9ee57-120">运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="9ee57-120">Run the following command.</span></span>

    ```Shell
    npm install @react-navigation/native@5.8.8 @react-navigation/drawer@5.11.1 @react-navigation/stack@5.12.5
    npm install @react-native-community/masked-view@0.1.10 react-native-safe-area-context@3.1.8 windows-iana
    npm install react-native-reanimated@1.13.1 react-native-screens@2.14.0 @react-native-async-storage/async-storage@1.13.2
    npm install react-native-elements@2.3.2 react-native-vector-icons@7.1.0 react-native-gesture-handler@1.8.0
    npm install react-native-app-auth@6.0.1 moment@2.29.1 moment-timezone @microsoft/microsoft-graph-client@2.1.1
    npm install @react-native-community/datetimepicker@3.0.4
    npm install @microsoft/microsoft-graph-types --save-dev
    ```

### <a name="link-and-configure-dependencies-for-ios"></a><span data-ttu-id="9ee57-121">链接和配置 iOS 的依存关系</span><span class="sxs-lookup"><span data-stu-id="9ee57-121">Link and configure dependencies for iOS</span></span>

> [!NOTE]
> <span data-ttu-id="9ee57-122">如果您没有设定 iOS 的目标，则可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="9ee57-122">If you are not targeting iOS, you can skip this section.</span></span>

1. <span data-ttu-id="9ee57-123">在 **GraphTutorial/ios** 目录中打开您的 CLI。</span><span class="sxs-lookup"><span data-stu-id="9ee57-123">Open your CLI in the **GraphTutorial/ios** directory.</span></span>
1. <span data-ttu-id="9ee57-124">运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="9ee57-124">Run the following command.</span></span>

    ```Shell
    pod install
    ```

1. <span data-ttu-id="9ee57-125">在文本编辑器中打开 **GraphTutorial/ios/GraphTutorial/Info. plist** 文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-125">Open the **GraphTutorial/ios/GraphTutorial/Info.plist** file in a text editor.</span></span> <span data-ttu-id="9ee57-126">将以下代码添加到 `</dict>` 文件中最后一行的前面。</span><span class="sxs-lookup"><span data-stu-id="9ee57-126">Add the following just before the last `</dict>` line in the file.</span></span>

    ```xml
    <key>UIAppFonts</key>
    <array>
      <string>AntDesign.ttf</string>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>Feather.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>FontAwesome5_Brands.ttf</string>
      <string>FontAwesome5_Regular.ttf</string>
      <string>FontAwesome5_Solid.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>Zocial.ttf</string>
    </array>
    ```

1. <span data-ttu-id="9ee57-127">在文本编辑器中打开 **GraphTutorial/ios/GraphTutorial/AppDelegate** 文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-127">Open the **GraphTutorial/ios/GraphTutorial/AppDelegate.h** file in a text editor.</span></span> <span data-ttu-id="9ee57-128">将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="9ee57-128">Replace its contents with the following.</span></span>

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a><span data-ttu-id="9ee57-129">配置适用于 Android 的依赖项</span><span class="sxs-lookup"><span data-stu-id="9ee57-129">Configure dependencies for Android</span></span>

> [!NOTE]
> <span data-ttu-id="9ee57-130">如果你没有设定 Android 的目标，则可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="9ee57-130">If you are not targeting Android, you can skip this section.</span></span>

1. <span data-ttu-id="9ee57-131">在编辑器中打开 **GraphTutorial/android/app/gradle** 文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-131">Open the **GraphTutorial/android/app/build.gradle** file in an editor.</span></span>
1. <span data-ttu-id="9ee57-132">找到该 `defaultConfig` 条目，并将以下属性添加到内部 `defaultConfig` 。</span><span class="sxs-lookup"><span data-stu-id="9ee57-132">Locate the `defaultConfig` entry and add the following property inside `defaultConfig`.</span></span>

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    <span data-ttu-id="9ee57-133">该 `defaultConfig` 条目应如下所示。</span><span class="sxs-lookup"><span data-stu-id="9ee57-133">The `defaultConfig` entry should look similar to the following.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. <span data-ttu-id="9ee57-134">将以下行添加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="9ee57-134">Add the following line to the end of the file.</span></span>

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. <span data-ttu-id="9ee57-135">保存文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-135">Save the file.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="9ee57-136">设计应用程序</span><span class="sxs-lookup"><span data-stu-id="9ee57-136">Design the app</span></span>

<span data-ttu-id="9ee57-137">应用程序将使用 [导航抽屉](https://reactnavigation.org/docs/drawer-based-navigation.html) 在不同视图之间导航。</span><span class="sxs-lookup"><span data-stu-id="9ee57-137">The application will use a [navigation drawer](https://reactnavigation.org/docs/drawer-based-navigation.html) to navigate between different views.</span></span> <span data-ttu-id="9ee57-138">在此步骤中，将创建应用程序使用的基本视图，并实现导航抽屉。</span><span class="sxs-lookup"><span data-stu-id="9ee57-138">In this step you will create the basic views used by the app and implement the navigation drawer.</span></span>

### <a name="create-views"></a><span data-ttu-id="9ee57-139">创建视图</span><span class="sxs-lookup"><span data-stu-id="9ee57-139">Create views</span></span>

<span data-ttu-id="9ee57-140">在本节中，您将创建用于支持 [身份验证流](https://reactnavigation.org/docs/auth-flow)的应用程序视图。</span><span class="sxs-lookup"><span data-stu-id="9ee57-140">In this section you will create the views for the app to support an [authentication flow](https://reactnavigation.org/docs/auth-flow).</span></span>

1. <span data-ttu-id="9ee57-141">打开 **GraphTutorial/index.js** 并将以下语句添加到文件顶部，在任何其他语句之前 `import` 。</span><span class="sxs-lookup"><span data-stu-id="9ee57-141">Open **GraphTutorial/index.js** and add the following to the top of the file, before any other `import` statements.</span></span>

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. <span data-ttu-id="9ee57-142">在名为 **AuthContext** 的 **GraphTutorial** 目录中创建一个新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="9ee57-142">Create a new file in the **GraphTutorial** directory named **AuthContext.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/AuthContext.tsx" id="AuthContextSnippet":::

1. <span data-ttu-id="9ee57-143">在名为 **UserContext** 的 **GraphTutorial** 目录中创建一个新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="9ee57-143">Create a new file in the **GraphTutorial** directory named **UserContext.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/UserContext.tsx" id="UserContextSnippet":::

1. <span data-ttu-id="9ee57-144">在名为 " **屏幕** " 的 **GraphTutorial** 目录中创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="9ee57-144">Create a new directory in the **GraphTutorial** directory named **screens**.</span></span>
1. <span data-ttu-id="9ee57-145">在名为 **HomeScreen** 的 **GraphTutorial/屏幕** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-145">Create a new file in the **GraphTutorial/screens** directory named **HomeScreen.tsx**.</span></span> <span data-ttu-id="9ee57-146">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="9ee57-146">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="HomeScreenSnippet":::

1. <span data-ttu-id="9ee57-147">在名为 **CalendarScreen** 的 **GraphTutorial/屏幕** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-147">Create a new file in the **GraphTutorial/screens** directory named **CalendarScreen.tsx**.</span></span> <span data-ttu-id="9ee57-148">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="9ee57-148">Add the following code to the file.</span></span>

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';

    const Stack = createStackNavigator();

    // Temporary placeholder view
    const CalendarComponent = () => (
      <View style={styles.container}>
        <Text>Calendar</Text>
      </View>
    );

    export default class CalendarScreen extends React.Component {

      render() {
        return (
          <Stack.Navigator>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                headerShown: false
              }} />
          </Stack.Navigator>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="9ee57-149">在名为 **SignInScreen** 的 **GraphTutorial/屏幕** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-149">Create a new file in the **GraphTutorial/screens** directory named **SignInScreen.tsx**.</span></span> <span data-ttu-id="9ee57-150">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="9ee57-150">Add the following code to the file.</span></span>

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';

    type SignInProps = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default class SignInScreen extends React.Component<SignInProps> {
      static contextType = AuthContext;

      _signInAsync = async () => {
        await this.context.signIn();
      };

      componentDidMount() {
        this.props.navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });
      }

      render() {
        return (
          <View style={styles.container}>
            <Button title='Sign In' onPress={this._signInAsync}/>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center'
      }
    });
    ```

1. <span data-ttu-id="9ee57-151">在名为 **AuthLoadingScreen** 的 **GraphTutorial/屏幕** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-151">Create a new file in the **GraphTutorial/screens** directory named **AuthLoadingScreen.tsx**.</span></span> <span data-ttu-id="9ee57-152">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="9ee57-152">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="9ee57-153">创建导航抽屉</span><span class="sxs-lookup"><span data-stu-id="9ee57-153">Create a navigation drawer</span></span>

<span data-ttu-id="9ee57-154">在本节中，您将为应用程序创建一个菜单，并更新应用程序以使用响应导航在屏幕之间移动。</span><span class="sxs-lookup"><span data-stu-id="9ee57-154">In this section you will create a menu for the application, and update the application to use react-navigation to move between screens.</span></span>

1. <span data-ttu-id="9ee57-155">在 **GraphTutorial** 目录中创建 **一个名为** "menu" 的新目录。</span><span class="sxs-lookup"><span data-stu-id="9ee57-155">Create a new directory in the **GraphTutorial** directory named **menus**.</span></span>

1. <span data-ttu-id="9ee57-156">在名为 **DrawerMenu** 的 **GraphTutorial/菜单** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="9ee57-156">Create a new file in the **GraphTutorial/menus** directory named **DrawerMenu.tsx**.</span></span> <span data-ttu-id="9ee57-157">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="9ee57-157">Add the following code to the file.</span></span>

    ```typescript
    import React, { FC } from 'react';
    import {
      Alert,
      Image,
      StyleSheet,
      Text,
      View,
      ImageSourcePropType
    } from 'react-native';
    import {
      createDrawerNavigator,
      DrawerContentScrollView,
      DrawerItem,
      DrawerItemList,
      DrawerContentComponentProps
    } from '@react-navigation/drawer';
    import { ParamListBase } from '@react-navigation/native';
    import { StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from '../AuthContext';
    import { UserContext } from '../UserContext';
    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuProps = {
      navigation: StackNavigationProp<ParamListBase>;
    }

    const CustomDrawerContent: FC<CustomDrawerContentProps> = props => (
      <DrawerContentScrollView {...props}>
          <View style={styles.profileView}>
            <Image source={props.userPhoto}
              resizeMode='contain'
              style={styles.profilePhoto} />
            <Text style={styles.profileUserName}>{props.userName}</Text>
            <Text style={styles.profileEmail}>{props.userEmail}</Text>
          </View>
          <DrawerItemList {...props} />
          <DrawerItem label='Sign Out' onPress={props.signOut}/>
      </DrawerContentScrollView>
    );

    export default class DrawerMenuContent extends React.Component<DrawerMenuProps> {
      static contextType = AuthContext;

      state = {
        // TEMPORARY
        userLoading: true,
        userFirstName: 'Adele',
        userFullName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userTimeZone: 'UTC',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        this.context.signOut();
      }

      async componentDidMount() {
        this.props.navigation.setOptions({
          headerShown: false,
        });
      }

      render() {
        const userLoaded = !this.state.userLoading;

        return (
          <UserContext.Provider value={this.state}>
            <Drawer.Navigator
              drawerType='front'
              screenOptions={{
                headerStyle: {
                  backgroundColor: '#276b80'
                },
                headerTintColor: 'white'
              }}
              drawerContent={props => (
                <CustomDrawerContent {...props}
                  userName={this.state.userFullName}
                  userEmail={this.state.userEmail}
                  userPhoto={this.state.userPhoto}
                  signOut={this._signOut} />
              )}>
              <Drawer.Screen name='Home'
                component={HomeScreen}
                options={{drawerLabel: 'Home', headerTitle: 'Welcome'}} />
              { userLoaded &&
                <Drawer.Screen name='Calendar'
                  component={CalendarScreen}
                  options={{drawerLabel: 'Calendar'}} />
              }
            </Drawer.Navigator>
          </UserContext.Provider>
        );
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1
      },
      profileView: {
        alignItems: 'center',
        padding: 10
      },
      profilePhoto: {
        width: 80,
        height: 80,
        borderRadius: 40
      },
      profileUserName: {
        fontWeight: '700'
      },
      profileEmail: {
        fontWeight: '200',
        fontSize: 10
      }
    });
    ```

1. <span data-ttu-id="9ee57-158">在名为 **images** 的 **GraphTutorial** 目录中创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="9ee57-158">Create a new directory in the **GraphTutorial** directory named **images**.</span></span>
1. <span data-ttu-id="9ee57-159">在此目录中添加一个名为 **no-profile-pic.png** 的默认配置文件映像。</span><span class="sxs-lookup"><span data-stu-id="9ee57-159">Add a default profile image named **no-profile-pic.png** in this directory.</span></span> <span data-ttu-id="9ee57-160">您可以使用任何您喜欢的图像，也可以使用 [此示例中的](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)任何图像。</span><span class="sxs-lookup"><span data-stu-id="9ee57-160">You can use any image you like, or use [the one from this sample](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png).</span></span>

1. <span data-ttu-id="9ee57-161">打开 **GraphTutorial/App. tsx** 文件，并将整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="9ee57-161">Open the **GraphTutorial/App.tsx** file and replace the entire contents with the following.</span></span>

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import * as React from 'react';
    import { NavigationContainer, ParamListBase } from '@react-navigation/native';
    import { createStackNavigator, StackNavigationProp } from '@react-navigation/stack'

    import { AuthContext } from './AuthContext';
    import SignInScreen from './screens/SignInScreen';
    import DrawerMenuContent from './menus/DrawerMenu'
    import AuthLoadingScreen from './screens/AuthLoadingScreen';

    const Stack = createStackNavigator();

    type Props = {
      navigation: StackNavigationProp<ParamListBase>;
    };

    export default function App({ navigation }: Props) {
      const [state, dispatch] = React.useReducer(
        (prevState: any, action: any) => {
          switch (action.type) {
            case 'RESTORE_TOKEN':
              return {
                ...prevState,
                userToken: action.token,
                isLoading: false
              };
            case 'SIGN_IN':
              return {
                ...prevState,
                isSignOut: false,
                userToken: action.token
              }
            case 'SIGN_OUT':
              return {
                ...prevState,
                isSignOut: true,
                userToken: null
              }
          }
        },
        {
          isLoading: true,
          isSignOut: false,
          userToken: null
        }
      );

      React.useEffect(() => {
        const bootstrapAsync = async () => {
          let userToken = null;
          // TEMPORARY
          dispatch({ type: 'RESTORE_TOKEN', token: userToken });
        };

        bootstrapAsync();
      }, []);

      const authContext = React.useMemo(
        () => ({
          signIn: async () => {
            dispatch({ type: 'SIGN_IN', token: 'placeholder-token' });
          },
          signOut: async () => {
            dispatch({ type: 'SIGN_OUT' });
          }
        }),
        []
      );

      return (
        <AuthContext.Provider value={authContext}>
          <NavigationContainer>
            <Stack.Navigator>
              {state.isLoading ? (
                <Stack.Screen name="Loading" component={AuthLoadingScreen} />
              ) : state.userToken == null ? (
                <Stack.Screen name="SignIn" component={SignInScreen} />
              ) : (
                <Stack.Screen name="Main" component={DrawerMenuContent} />
              )}
            </Stack.Navigator>
          </NavigationContainer>
        </AuthContext.Provider>
      );
    }
    ```

1. <span data-ttu-id="9ee57-162">保存所有更改。</span><span class="sxs-lookup"><span data-stu-id="9ee57-162">Save all of your changes.</span></span>

1. <span data-ttu-id="9ee57-163">在仿真程序中重新加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="9ee57-163">Reload the application in your emulator.</span></span>

<span data-ttu-id="9ee57-164">在点击 "登录 **" 或 "注销** **"** 按钮时，应用的菜单应工作在两个片段之间导航并发生变化。</span><span class="sxs-lookup"><span data-stu-id="9ee57-164">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![Android 上的应用程序的屏幕截图](./images/android-app-screens.png)

![IOS 上的应用程序的屏幕截图](./images/ios-app-screens.png)
