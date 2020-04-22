<!-- markdownlint-disable MD002 MD041 -->

在本练习中，你将扩展上一练习中的应用程序，以支持 Azure AD 的身份验证。 若要获取所需的 OAuth 访问令牌以调用 Microsoft Graph，这是必需的。 若要执行此操作，请将[响应本机应用程序-auth](https://github.com/FormidableLabs/react-native-app-auth)库集成到应用程序中。

1. 在名为 " **auth**" 的**GraphTutorial**目录中创建一个新目录。
1. 在名为**AuthConfig**的**GraphTutorial/auth**目录中创建一个新文件。 将以下代码添加到文件中。

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthConfig.ts.example":::

    将`YOUR_APP_ID_HERE`替换为应用注册中的应用 ID。

> [!IMPORTANT]
> 如果使用的是源代码管理（如 git），现在是从源代码控制中排除**AuthConfig**文件以避免无意中泄漏您的应用程序 ID 的最佳时机。

## <a name="implement-sign-in"></a>实施登录

在本节中，您将创建身份验证帮助程序类，并更新应用程序以进行登录和注销。

1. 在名为**AuthManager**的**GraphTutorial/auth**目录中创建一个新文件。 将以下代码添加到文件中。

    :::code language="typescript" source="../demo/GraphTutorial/auth/AuthManager.ts" id="AuthManagerSnippet":::

1. 打开**GraphTutorial/views/SignInScreen**文件，并将以下`import`语句添加到文件顶部。

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. 将现有`_signInAsync`的方法替换为以下项。

    :::code language="typescript" source="../demo/GraphTutorial/screens/SignInScreen.tsx" id="SignInAsyncSnippet":::

1. 打开**GraphTutorial/views/HomeScreen**文件，并将以下`import`语句添加到文件顶部。

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. 将下列方法添加到 `HomeScreen` 类。

    ```typescript
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

1. 打开**GraphTutorial/menu/DrawerMenu**文件，并将以下`import`语句添加到文件顶部。

    ```typescript
    import { AuthManager } from '../auth/AuthManager';
    ```

1. 将现有`_signOut`的方法替换为以下项。

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="SignOutSnippet" highlight="5":::

1. 保存所做的更改，并在仿真程序中重新加载应用程序。

如果你登录到应用，你应该会看到 "**欢迎**" 屏幕上显示的访问令牌。

## <a name="get-user-details"></a>获取用户详细信息

在本节中，您将为 Graph 客户端库创建自定义身份验证提供程序，创建帮助程序类以保存对 Microsoft Graph 的所有调用， `HomeScreen`并`DrawerMenuContent`更新和类以使用此新类来获取已登录的用户。

1. 在名为**graph**的**GraphTutorial**目录中创建一个新目录。
1. 在名为**GraphAuthProvider**的**GraphTutorial/graph**目录中创建一个新文件。 将以下代码添加到文件中。

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphAuthProvider.ts" id="AuthProviderSnippet":::

1. 在名为**GraphManager**的**GraphTutorial/graph**目录中创建一个新文件。 将以下代码添加到文件中。

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
        return graphClient.api('/me').get();
      }
    }
    ```

1. 打开**GraphTutorial/views/HomeScreen**文件，并将以下`import`语句添加到文件顶部。

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. 将`componentDidMount`方法替换为以下方法。

    :::code language="typescript" source="../demo/GraphTutorial/screens/HomeScreen.tsx" id="ComponentDidMountSnippet" highlight="3-6,9":::

1. 打开**GraphTutorial/views/DrawerMenu**文件，并将以下`import`语句添加到文件顶部。

    ```typescript
    import { GraphManager } from '../graph/GraphManager';
    ```

1. 将以下`componentDidMount`方法添加到`DrawerMenuContent`类中。

    :::code language="typescript" source="../demo/GraphTutorial/menus/DrawerMenu.tsx" id="ComponentDidMountSnippet":::

如果现在保存更改并重新加载应用程序，则在使用用户的显示名称和电子邮件地址更新 UI 后，登录 UI。
