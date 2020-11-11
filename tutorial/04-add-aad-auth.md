<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="3bfeb-101">在本练习中，你将扩展上一练习中的应用程序，以支持 Azure AD 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="3bfeb-102">若要获取所需的 OAuth 访问令牌以调用 Microsoft Graph，这是必需的。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="3bfeb-103">若要执行此操作，请将 [响应本机应用程序-auth](https://github.com/FormidableLabs/react-native-app-auth) 库集成到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-103">To do this, you will integrate the [react-native-app-auth](https://github.com/FormidableLabs/react-native-app-auth) library into the application.</span></span>

1. <span data-ttu-id="3bfeb-104">在名为 " **auth** " 的 **GraphTutorial** 目录中创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-104">Create a new directory in the **GraphTutorial** directory named **auth**.</span></span>
1. <span data-ttu-id="3bfeb-105">在名为 **AuthConfig** 的 **GraphTutorial/auth** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-105">Create a new file in the **GraphTutorial/auth** directory named **AuthConfig.ts**.</span></span> <span data-ttu-id="3bfeb-106">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-106">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.example.ts":::

    <span data-ttu-id="3bfeb-107">`YOUR_APP_ID_HERE`将替换为应用注册中的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-107">Replace `YOUR_APP_ID_HERE` with the app ID from your app registration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bfeb-108">如果使用的是源代码管理（如 git），现在是从源代码控制中排除 **AuthConfig** 文件以避免无意中泄漏您的应用程序 ID 的最佳时机。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-108">If you're using source control such as git, now would be a good time to exclude the **AuthConfig.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="3bfeb-109">实施登录</span><span class="sxs-lookup"><span data-stu-id="3bfeb-109">Implement sign-in</span></span>

<span data-ttu-id="3bfeb-110">在本节中，您将创建身份验证帮助程序类，并更新应用程序以进行登录和注销。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-110">In this section you will create an authentication helper class, and update the app to sign in and sign out.</span></span>

1. <span data-ttu-id="3bfeb-111">在名为 **AuthManager** 的 **GraphTutorial/auth** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-111">Create a new file in the **GraphTutorial/auth** directory named **AuthManager.ts**.</span></span> <span data-ttu-id="3bfeb-112">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-112">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. <span data-ttu-id="3bfeb-113">打开 **GraphTutorial/App. tsx** 文件，并将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-113">Open the **GraphTutorial/App.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from './auth/AuthManager';
    ```

1. <span data-ttu-id="3bfeb-114">将现有 `authContext` 声明替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-114">Replace the existing `authContext` declaration with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/App.tsx" id="AuthContextSnippet" highlight="4-6,9":::

1. <span data-ttu-id="3bfeb-115">打开 **GraphTutorial/menu/DrawerMenu** 文件，并将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-115">Open the **GraphTutorial/menus/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. <span data-ttu-id="3bfeb-116">将以下代码添加到 `componentDidMount` 函数中。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-116">Add the following code to the `componentDidMount` function.</span></span>

    ```typescript
    try {
      const accessToken = await AuthManager.getAccessTokenAsync();

      // TEMPORARY
      this.setState({userFirstName: accessToken, userLoading: false});
    } catch (error) {
      Alert.alert(
        'Error getting token',
        JSON.stringify(error),
        [
          {
            text: 'OK'
          }
        ],
        { cancelable: false }
      );
    }
    ```

1. <span data-ttu-id="3bfeb-117">保存所做的更改，并在仿真程序中重新加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-117">Save your changes and reload the application in your emulator.</span></span>

<span data-ttu-id="3bfeb-118">如果你登录到应用，你应该会看到 " **欢迎** " 屏幕上显示的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-118">If you sign in to the app, you should see an access token displayed on the **Welcome** screen.</span></span>

## <a name="get-user-details"></a><span data-ttu-id="3bfeb-119">获取用户详细信息</span><span class="sxs-lookup"><span data-stu-id="3bfeb-119">Get user details</span></span>

<span data-ttu-id="3bfeb-120">在本节中，您将为 Graph 客户端库创建自定义身份验证提供程序，创建帮助程序类以保存对 Microsoft Graph 的所有调用，并更新 `DrawerMenuContent` 类以使用此新类来获取已登录的用户。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-120">In this section you will create a custom authentication provider for the Graph client library, create a helper class to hold all of the calls to Microsoft Graph and update the `DrawerMenuContent` class to use this new class to get the logged-in user.</span></span>

1. <span data-ttu-id="3bfeb-121">在名为 **graph** 的 **GraphTutorial** 目录中创建一个新目录。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-121">Create a new directory in the **GraphTutorial** directory named **graph**.</span></span>
1. <span data-ttu-id="3bfeb-122">在名为 **GraphAuthProvider** 的 **GraphTutorial/graph** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-122">Create a new file in the **GraphTutorial/graph** directory named **GraphAuthProvider.ts**.</span></span> <span data-ttu-id="3bfeb-123">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-123">Add the following code to the file.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. <span data-ttu-id="3bfeb-124">在名为 **GraphManager** 的 **GraphTutorial/graph** 目录中创建一个新文件。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-124">Create a new file in the **GraphTutorial/graph** directory named **GraphManager.ts**.</span></span> <span data-ttu-id="3bfeb-125">将以下代码添加到文件中。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-125">Add the following code to the file.</span></span>

    ```typescript
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
        return await graphClient
          .api('/me')
          .select('displayName,givenName,mail,mailboxSettings,userPrincipalName')
          .get();
      }
    }
    ```

1. <span data-ttu-id="3bfeb-126">打开 **GraphTutorial/views/DrawerMenu** 文件，并将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-126">Open the **GraphTutorial/views/DrawerMenu.tsx** file and add the following `import` statement to the top of the file.</span></span>

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. <span data-ttu-id="3bfeb-127">将 `componentDidMount` 方法替换为以下方法。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-127">Replace the `componentDidMount` method with the following.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

<span data-ttu-id="3bfeb-128">如果现在保存更改并重新加载应用程序，则在使用用户的显示名称和电子邮件地址更新 UI 后，登录 UI。</span><span class="sxs-lookup"><span data-stu-id="3bfeb-128">If you save your changes and reload the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
