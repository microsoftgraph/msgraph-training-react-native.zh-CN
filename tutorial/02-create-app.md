<!-- markdownlint-disable MD002 MD041 -->

首先创建新的响应本机项目。

1. 在要创建项目的目录中打开命令行界面（CLI）。 运行以下命令，运行[响应本机的 cli](https://github.com/facebook/react-native)工具并创建新的响应本机项目。

    ```Shell
    npx react-native init GraphTutorial --template react-native-template-typescript
    ```

1. **可选：** 通过运行项目验证您的开发环境是否已正确配置。 在 CLI 中，将目录更改为刚创建的**GraphTutorial**目录，并运行下列命令之一。

    - 对于 iOS：`npx react-native run-ios`
    - 对于 Android：启动 Android 仿真程序实例并运行`npx react-native run-android`

## <a name="install-dependencies"></a>安装依赖项

在继续之前，请安装稍后将使用的一些其他依赖项。

- [响应-导航](https://reactnavigation.org)以处理应用程序中的视图之间的导航。
- [响应-本机-笔势-处理程序](https://github.com/kmagiera/react-native-gesture-handler)、[响应本机安全区域上下文](https://github.com/th3rdwave/react-native-safe-area-context)、[响应本机屏幕](https://github.com/kmagiera/react-native-screens)、[响应本机](https://github.com/kmagiera/react-native-reanimated)恢复以及响应导航所需的[屏蔽视图](https://github.com/react-native-community/react-native-masked-view)。
- [响应-本机元素](https://react-native-training.github.io/react-native-elements/docs/getting_started.html)和[响应本机向量图标](https://github.com/oblador/react-native-vector-icons)，以便为 UI 提供图标。
- [响应-本机-](https://github.com/FormidableLabs/react-native-app-auth)对处理身份验证和令牌管理的应用程序身份验证。
- 用于为令牌提供存储的[异步存储](https://github.com/react-native-community/react-native-async-storage)。
- 处理日期和时间的分析和比较的[时间](https://momentjs.com)。
- microsoft graph-用于调用 Microsoft Graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。

1. 在响应本机项目的根目录中打开您的 CLI。
1. 运行以下命令。

    ```Shell
    npm install @react-navigation/native@5.1.5 @react-navigation/drawer@5.4.1 @react-navigation/stack@5.2.10
    npm install @react-native-community/masked-view@0.1.7 react-native-safe-area-context@0.7.3
    npm install react-native-reanimated@1.8.0 react-native-screens@2.4.0 @react-native-community/async-storage@1.9.0
    npm install react-native-elements@1.2.7 react-native-vector-icons@6.6.0 react-native-gesture-handler@1.6.1
    npm install react-native-app-auth@5.1.1 moment@2.24.0 @microsoft/microsoft-graph-client@2.0.0
    ```

### <a name="link-and-configure-dependencies-for-ios"></a>链接和配置 iOS 的依存关系

> [!NOTE]
> 如果您没有设定 iOS 的目标，则可以跳过此部分。

1. 在**GraphTutorial/ios**目录中打开您的 CLI。
1. 运行以下命令。

    ```Shell
    pod install
    ```

1. 在文本编辑器中打开**GraphTutorial/ios/GraphTutorial/Info. plist**文件。 将以下代码添加到文件中`</dict>`最后一行的前面。

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

1. 在文本编辑器中打开**GraphTutorial/ios/GraphTutorial/AppDelegate**文件。 将其内容替换为以下内容。

    :::code language="objc" source="../demo/GraphTutorial/ios/GraphTutorial/AppDelegate.h":::

### <a name="configure-dependencies-for-android"></a>配置适用于 Android 的依赖项

> [!NOTE]
> 如果你没有设定 Android 的目标，则可以跳过此部分。

1. 在编辑器中打开**GraphTutorial/android/app/gradle**文件。
1. 找到该`defaultConfig`条目，并将以下属性添加`defaultConfig`到内部。

    ```Gradle
    manifestPlaceholders = [
        appAuthRedirectScheme: 'graph-tutorial'
    ]
    ```

    该`defaultConfig`条目应如下所示。

    :::code language="gradle" source="../demo/GraphTutorial/android/app/build.gradle" id="DefaultConfigSnippet":::

1. 将以下行添加到文件末尾。

    ```Gradle
    apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
    ```

1. 保存文件。

## <a name="design-the-app"></a>设计应用程序

应用程序将使用[导航抽屉](https://reactnavigation.org/docs/drawer-based-navigation.html)在不同视图之间导航。 在此步骤中，将创建应用程序使用的基本视图，并实现导航抽屉。

### <a name="create-views"></a>创建视图

在本节中，您将创建用于支持[身份验证流](https://reactnavigation.org/docs/auth-flow)的应用程序视图。

1. 打开**GraphTutorial/index** ，并将以下语句添加到文件顶部，在任何其他`import`语句之前。

    ```javascript
    import 'react-native-gesture-handler';
    ```

1. 在名为 "**屏幕**" 的**GraphTutorial**目录中创建一个新目录。
1. 在名为**HomeScreen**的**GraphTutorial/屏幕**目录中创建一个新文件。 将以下代码添加到文件中。

    ```typescript
    import React from 'react';
    import {
      ActivityIndicator,
      Alert,
      StyleSheet,
      Text,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

    const Stack = createStackNavigator();
    const UserState = React.createContext({userLoading: true, userName: ''});

    type HomeScreenState = {
      userLoading: boolean;
      userName: string;
    }

    const HomeComponent = () => {
      const userState = React.useContext(UserState);

      return (
        <View style={styles.container}>
          <ActivityIndicator animating={userState.userLoading} size='large' />
          {userState.userLoading ? null: <Text>Hello {userState.userName}!</Text>}
        </View>
      );
    }

    export default class HomeScreen extends React.Component {

      state: HomeScreenState = {
        userLoading: true,
        userName: ''
      };

      render() {
        return (
          <UserState.Provider value={this.state}>
              <Stack.Navigator screenOptions={headerOptions}>
                <Stack.Screen name='Home'
                  component={HomeComponent}
                  options={{
                    title: 'Welcome',
                    headerLeft: () => <DrawerToggle/>
                  }} />
              </Stack.Navigator>
          </UserState.Provider>
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

1. 在名为**CalendarScreen**的**GraphTutorial/屏幕**目录中创建一个新文件。 将以下代码添加到文件中。

    ```typescript
    import React from 'react';
    import {
      Text,
      StyleSheet,
      View,
    } from 'react-native';
    import { createStackNavigator } from '@react-navigation/stack';
    import { DrawerToggle, headerOptions } from '../menus/HeaderComponents';

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
          <Stack.Navigator screenOptions={ headerOptions }>
            <Stack.Screen name='Calendar'
              component={ CalendarComponent }
              options={{
                title: 'Calendar',
                headerLeft: () => <DrawerToggle/>
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

1. 在名为**SignInScreen**的**GraphTutorial/屏幕**目录中创建一个新文件。 将以下代码添加到文件中。

    ```typescript
    // Adapted from https://reactnavigation.org/docs/auth-flow
    import React from 'react';
    import {
      Alert,
      Button,
      StyleSheet,
      View,
    } from 'react-native';
    import { NavigationContext } from '@react-navigation/native';

    export default class SignInScreen extends React.Component {
      static contextType = NavigationContext;

      static navigationOptions = {
        title: 'Please sign in',
      };

      _signInAsync = async () => {
        const navigation = this.context;

        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [ { name: 'Main' } ]
        });
      };

      render() {
        const navigation = this.context;
        navigation.setOptions({
          title: 'Please sign in',
          headerShown: true
        });

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

1. 在名为**AuthLoadingScreen**的**GraphTutorial/屏幕**目录中创建一个新文件。 将以下代码添加到文件中。

    :::code language="typescript" source="../demo/GraphTutorial/screens/AuthLoadingScreen.tsx" id="AuthLoadingScreenSnippet":::

### <a name="create-a-navigation-drawer"></a>创建导航抽屉

在本节中，您将为应用程序创建一个菜单，并更新应用程序以使用响应导航在屏幕之间移动。

1. 在**GraphTutorial**目录中创建**一个名为**"menu" 的新目录。
1. 在名为**HeaderComponents**的**GraphTutorial/菜单**目录中创建一个新文件。 将以下代码添加到文件中。

    :::code language="typescript" source="../demo/GraphTutorial/menus/HeaderComponents.tsx" id="HeaderComponentSnippet":::

1. 在名为**DrawerMenu**的**GraphTutorial/菜单**目录中创建一个新文件。 将以下代码添加到文件中。

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
    import { NavigationContext } from '@react-navigation/native';

    import HomeScreen from '../screens/HomeScreen';
    import CalendarScreen from '../screens/CalendarScreen';

    const Drawer = createDrawerNavigator();

    type CustomDrawerContentProps = DrawerContentComponentProps & {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
      signOut: () => void;
    }

    type DrawerMenuState = {
      userName: string;
      userEmail: string;
      userPhoto: ImageSourcePropType;
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

    export default class DrawerMenuContent extends React.Component {
      static contextType = NavigationContext;

      state: DrawerMenuState = {
        // TEMPORARY
        userName: 'Adele Vance',
        userEmail: 'adelev@contoso.com',
        userPhoto: require('../images/no-profile-pic.png')
      }

      _signOut = async () => {
        const navigation = this.context;
        // Sign out
        // TEMPORARY
        navigation.reset({
          index: 0,
          routes: [{ name: 'SignIn' }]
        });
      }

      render() {
        const navigation = this.context;
        navigation.setOptions({
          headerShown: false,
        });

        return (
          <Drawer.Navigator
            drawerType='front'
            drawerContent={props => (
              <CustomDrawerContent {...props}
                userName={this.state.userName}
                userEmail={this.state.userEmail}
                userPhoto={this.state.userPhoto}
                signOut={this._signOut} />
            )}>
            <Drawer.Screen name='Home'
              component={HomeScreen}
              options={{drawerLabel: 'Home'}} />
            <Drawer.Screen name='Calendar'
              component={CalendarScreen}
              options={{drawerLabel: 'Calendar'}} />
          </Drawer.Navigator>
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

1. 在名为**images**的**GraphTutorial**目录中创建一个新目录。
1. 在此目录中添加名为**no-profile-pic**的默认配置文件映像。 您可以使用任何您喜欢的图像，也可以使用[此示例中的](https://github.com/microsoftgraph/msgraph-training-react-native/blob/master/demo/GraphTutorial/images/no-profile-pic.png)任何图像。

1. 打开**GraphTutorial/App. tsx**文件，并将整个内容替换为以下内容。

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AppSnippet":::

1. 保存所有更改。

1. 在仿真程序中重新加载应用程序。

在点击 "登录 **" 或 "注销** **"** 按钮时，应用的菜单应工作在两个片段之间导航并发生变化。

![Android 上的应用程序的屏幕截图](./images/android-app-screens.png)

![IOS 上的应用程序的屏幕截图](./images/ios-app-screens.png)
