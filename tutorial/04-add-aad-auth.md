<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f4768-101">在本练习中，你将扩展上一练习中的应用程序，以支持 Azure AD 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="f4768-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="f4768-102">若要获取所需的 OAuth 访问令牌以调用 Microsoft Graph，这是必需的。</span><span class="sxs-lookup"><span data-stu-id="f4768-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="f4768-103">若要执行此操作，请将[响应本机应用程序-auth](https://github.com/FormidableLabs/react-native-app-auth)库集成到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="f4768-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="f4768-104">在名为 " **auth**" 的**GraphTutorial**目录中创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="f4768-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="f4768-105">在名为**AuthConfig**的**GraphTutorial/auth**目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="f4768-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.js**.</span></span> <span data-ttu-id="f4768-106">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="f4768-106">Add the following code to the file.</span></span>

    ```js
    export const AuthConfig = {
      appId = 'YOUR_APP_ID_HERE',
      appScopes = [
        'openid',
        'offline_access',
        'profile',
        'User.Read',
        'Calendars.Read'
      ]
    };
    ```

    <span data-ttu-id="f4768-107">将`YOUR_APP_ID_HERE`替换为应用注册中的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f4768-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4768-108">如果您使用的是源代码管理（如 git），现在是从源代码管理中排除**AuthConfig**文件以避免无意中泄漏您的应用程序 ID 的最佳时机。</span><span class="sxs-lookup"><span data-stu-id="f4768-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="f4768-109">实施登录</span><span class="sxs-lookup"><span data-stu-id="f4768-109">Implement sign-in</span></span>

<span data-ttu-id="f4768-110">在本节中，您将创建身份验证帮助程序类，并更新应用程序以进行登录和注销。</span><span class="sxs-lookup"><span data-stu-id="f4768-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="f4768-111">在名为**AuthManager**的**GraphTutorial/auth**目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="f4768-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.js**.</span></span> <span data-ttu-id="f4768-112">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="f4768-112">Add the following code to the file.</span></span>

    ```js
    import { AuthConfig } from './AuthConfig';
    import { AsyncStorage } from 'react-native';
    import { authorize, refresh } from 'react-native-app-auth';
    import moment from 'moment';

    const config = {
      clientId: AuthConfig.appId,
      redirectUrl: Platform.OS === 'ios' ? 'urn:ietf:wg:oauth:2.0:oob' : 'graph-tutorial://react-native-auth',
      scopes: AuthConfig.appScopes,
      additionalParameters: { prompt: 'select_account' },
      serviceConfiguration: {
        authorizationEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/authorize',
        tokenEndpoint: 'https://login.microsoftonline.com/common/oauth2/v2.0/token',
      }
    };

    export class AuthManager {

      static signInAsync = async () => {
        const result = await authorize(config);

        // Store the access token, refresh token, and expiration time in storage
        await AsyncStorage.setItem('userToken', result.accessToken);
        await AsyncStorage.setItem('refreshToken', result.refreshToken);
        await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);
      }

      static signOutAsync = async () => {
        // Clear storage
        await AsyncStorage.removeItem('userToken');
        await AsyncStorage.removeItem('refreshToken');
        await AsyncStorage.removeItem('expireTime');
      }

      static getAccessTokenAsync = async() => {
        const expireTime = await AsyncStorage.getItem('expireTime');

        if (expireTime !== null) {
          // Get expiration time - 5 minutes
          // If it's <= 5 minutes before expiration, then refresh
          const expire = moment(expireTime).subtract(5, 'minutes');
          const now = moment();

          if (now.isSameOrAfter(expire)) {
            // Expired, refresh
            const refreshToken = await AsyncStorage.getItem('refreshToken');

            const result = await refresh(config, {refreshToken: refreshToken});

            // Store the new access token, refresh token, and expiration time in storage
            await AsyncStorage.setItem('userToken', result.accessToken);
            await AsyncStorage.setItem('refreshToken', result.refreshToken);
            await AsyncStorage.setItem('expireTime', result.accessTokenExpirationDate);

            return result.accessToken;
          }

          // Not expired, just return saved access token
          const accessToken = await AsyncStorage.getItem('userToken');
          return accessToken;
        }

        return null;
      }
    }
    ```

1. <span data-ttu-id="f4768-113">打开**GraphTutorial/views/SignInScreen**文件，并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="f4768-113">Open the **GraphTutorial/views/SignInScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f4768-114">将现有`_signInAsync`的方法替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="f4768-114">Replace the existing `_signInAsync` method with the following.</span></span>

    ```js
    _signInAsync = async () => {
      try {
        await AuthManager.signInAsync();
        this.props.navigation.navigate('App');
      } catch (error) {
        alert(error);
      }
    };

1. Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f4768-115">将下列方法添加到 `HomeScreen` 类。</span><span class="sxs-lookup"><span data-stu-id="f4768-115">Add the following method to the `HomeScreen` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        const accessToken = await AuthManager.getAccessTokenAsync();

        // TEMPORARY
        this.setState({userName: accessToken, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="f4768-116">打开**GraphTutorial/menu/DrawerMenu**文件，并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="f4768-116">Open the **GraphTutorial/menus/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="f4768-117">在`_onItemPressed`中，将`// TEMPORARY`行替换为以下代码行。</span><span class="sxs-lookup"><span data-stu-id="f4768-117">In `_onItemPressed`, replace the `// TEMPORARY` line with the following.</span></span>

    ```js
    await AuthManager.signOutAsync();
    ```

1. <span data-ttu-id="f4768-118">保存所做的更改，并在仿真程序中重新加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="f4768-118">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="f4768-119">如果你登录到应用，你应该会看到 "**欢迎**" 屏幕上显示的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="f4768-119">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="f4768-120">获取用户详细信息</span><span class="sxs-lookup"><span data-stu-id="f4768-120">Get user details</span></span>

<span data-ttu-id="f4768-121">在本节中，您将为 Graph 客户端库创建自定义身份验证提供程序，创建帮助程序类以保存对 Microsoft Graph 的所有调用， `HomeScreen`并`DrawerMenuContent`更新和类以使用此新类来获取已登录的用户。</span><span class="sxs-lookup"><span data-stu-id="f4768-121">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `HomeScreen` and `DrawerMenuContent` classes to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="f4768-122">在名为**graph**的**GraphTutorial**目录中创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="f4768-122">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="f4768-123">在名为**GraphAuthProvider**的**GraphTutorial/graph**目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="f4768-123">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.js**.</span></span> <span data-ttu-id="f4768-124">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="f4768-124">Add the following code to the file.</span></span>

    ```js
    import { AuthManager } from '../auth/AuthManager';

    // Used by Graph client to get access tokens
    // See https://github.com/microsoftgraph/msgraph-sdk-javascript/blob/dev/docs/CustomAuthenticationProvider.md
    export class GraphAuthProvider {
      getAccessToken = async() => {
        return await AuthManager.getAccessTokenAsync();
      }
    }
    ```

1. <span data-ttu-id="f4768-125">在名为**GraphManager**的**GraphTutorial/graph**目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="f4768-125">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.js**.</span></span> <span data-ttu-id="f4768-126">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="f4768-126">Add the following code to the file.</span></span>

    ```js
    import { Client } from '@microsoft/microsoft-graph-client';
    import { GraphAuthProvider } from './GraphAuthProvider';

    // Set the authProvider to an instance
    // of GraphAuthProvider
    const clientOptions = {
      authProvider: new GraphAuthProvider()
    };

    // Initialize the client
    const graphClient = Client.initWithMiddleware(clientOptions);

    export class GraphManager {
      static getUserAsync = async() => {
        // GET /me
        return graphClient.api('/me').get();
      }
    }
    ```

1. <span data-ttu-id="f4768-127">打开**GraphTutorial/views/HomeScreen**文件，并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="f4768-127">Open the **GraphTutorial/views/HomeScreen.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="f4768-128">将`componentDidMount`方法替换为以下方法。</span><span class="sxs-lookup"><span data-stu-id="f4768-128">Replace the `componentDidMount` method with the following.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();
        // Set the user name to the user's given name
        this.setState({userName: user.givenName, userLoading: false});
      } catch (error) {
        alert(error);
      }
    }
    ```

1. <span data-ttu-id="f4768-129">打开**GraphTutorial/views/DrawerMenu**文件，并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="f4768-129">Open the **GraphTutorial/views/DrawerMenu.js** file and add the following `import` statement to the top of the file.</span></span>

    ```js
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="f4768-130">将以下`componentDidMount`方法添加到`DrawerMenuContent`类中。</span><span class="sxs-lookup"><span data-stu-id="f4768-130">Add the following `componentDidMount` method to the `DrawerMenuContent` class.</span></span>

    ```js
    async componentDidMount() {
      try {
        // Get the signed-in user from Graph
        const user = await GraphManager.getUserAsync();

        // Update UI with display name and email
        this.setState({
          userName: user.displayName,
          // Work/School accounts have email address in mail attribute
          // Personal accounts have it in userPrincipalName
          userEmail: user.mail !== null ? user.mail : user.userPrincipalName,
        });
      } catch(error) {
        alert(error);
      }
    }
    ```

<span data-ttu-id="f4768-131">如果现在保存更改并重新加载应用程序，则在使用用户的显示名称和电子邮件地址更新 UI 后，登录 UI。</span><span class="sxs-lookup"><span data-stu-id="f4768-131">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
