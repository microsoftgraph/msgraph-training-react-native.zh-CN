# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="88fa3-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="88fa3-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88fa3-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="88fa3-102">Prerequisites</span></span>

<span data-ttu-id="88fa3-103">若要在此文件夹中运行已完成的项目，您需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="88fa3-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="88fa3-104">至少以下之一：</span><span class="sxs-lookup"><span data-stu-id="88fa3-104">At least one of the following:</span></span>
  - <span data-ttu-id="88fa3-105">[Android Studio](https://developer.android.com/studio/) **和** [Java 开发工具包](https://jdk.java.net)（在 Android 上运行示例所必需）</span><span class="sxs-lookup"><span data-stu-id="88fa3-105">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="88fa3-106">[Xcode](https://developer.apple.com/xcode/) （在 iOS 上运行示例所必需）</span><span class="sxs-lookup"><span data-stu-id="88fa3-106">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="88fa3-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="88fa3-107">Node.js</span></span>](https://nodejs.org)
- <span data-ttu-id="88fa3-108">使用 Outlook.com 上的邮箱的个人 Microsoft 帐户，或者是 Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="88fa3-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

> <span data-ttu-id="88fa3-109">**注意：** 本教程是使用响应本机 CLI 编写的，其中包含特定的先决条件，具体取决于您的操作系统和目标平台。</span><span class="sxs-lookup"><span data-stu-id="88fa3-109">**Note:** This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="88fa3-110">有关配置开发计算机的说明，请参阅[响应原生入门](https://facebook.github.io/react-native/docs/getting-started)。</span><span class="sxs-lookup"><span data-stu-id="88fa3-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="88fa3-111">下面列出了用于本教程的版本。</span><span class="sxs-lookup"><span data-stu-id="88fa3-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="88fa3-112">本指南中的步骤可能适用于其他版本，但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="88fa3-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="88fa3-113">适用于 Android 9.0 SDK 的 android Studio 3.6.2 版本</span><span class="sxs-lookup"><span data-stu-id="88fa3-113">Android Studio version 3.6.2 with the Android 9.0 SDK</span></span>
> - <span data-ttu-id="88fa3-114">Java 开发工具包版本12.0。2</span><span class="sxs-lookup"><span data-stu-id="88fa3-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="88fa3-115">Xcode 版本11。4</span><span class="sxs-lookup"><span data-stu-id="88fa3-115">Xcode version 11.4</span></span>
> - <span data-ttu-id="88fa3-116">Node.js 版本12.16。2</span><span class="sxs-lookup"><span data-stu-id="88fa3-116">Node.js version 12.16.2</span></span>

<span data-ttu-id="88fa3-117">如果你没有 Microsoft 帐户，可以使用以下几种方法获取免费帐户：</span><span class="sxs-lookup"><span data-stu-id="88fa3-117">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="88fa3-118">你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="88fa3-118">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="88fa3-119">你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="88fa3-119">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="88fa3-120">将应用程序注册到 Azure Active Directory 管理中心</span><span class="sxs-lookup"><span data-stu-id="88fa3-120">Register an application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="88fa3-121">打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。然后，使用**个人帐户**（亦称为“Microsoft 帐户”）或**工作或学校帐户**登录。</span><span class="sxs-lookup"><span data-stu-id="88fa3-121">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="88fa3-122">选择左侧导航栏中的“**Azure Active Directory**”，再选择“**管理**”下的“**应用注册**”。</span><span class="sxs-lookup"><span data-stu-id="88fa3-122">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="88fa3-123">应用注册的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="88fa3-123">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="88fa3-124">选择“新注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="88fa3-124">Select **New registration**.</span></span> <span data-ttu-id="88fa3-125">在“注册应用”\*\*\*\* 页上，按如下方式设置值。</span><span class="sxs-lookup"><span data-stu-id="88fa3-125">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="88fa3-126">将“名称”\*\*\*\* 设置为“`React Native Graph Tutorial`”。</span><span class="sxs-lookup"><span data-stu-id="88fa3-126">Set **Name** to `React Native Graph Tutorial`.</span></span>
    - <span data-ttu-id="88fa3-127">将“受支持的帐户类型”\*\*\*\* 设置为“任何组织目录中的帐户和个人 Microsoft 帐户”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="88fa3-127">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="88fa3-128">在 "**重定向 URI**" 下，将下拉列表更改为 "**公用客户端（移动 & 桌面）**"，并将值设置为`graph-tutorial://react-native-auth`。</span><span class="sxs-lookup"><span data-stu-id="88fa3-128">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `graph-tutorial://react-native-auth`.</span></span>

    !["注册应用程序" 页的屏幕截图](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="88fa3-130">选择 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="88fa3-130">Select **Register**.</span></span> <span data-ttu-id="88fa3-131">在 "**响应本机图形教程**" 页上，复制**应用程序（客户端） ID**的值并保存它，下一步将需要它。</span><span class="sxs-lookup"><span data-stu-id="88fa3-131">On the **React Native Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新应用注册的应用程序 ID 的屏幕截图](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="88fa3-133">在 "**管理**" 下，选择 "**身份验证**"。</span><span class="sxs-lookup"><span data-stu-id="88fa3-133">Under **Manage**, select **Authentication**.</span></span> <span data-ttu-id="88fa3-134">在 "**重定向 uri** " 页上，使用 URI `urn:ietf:wg:oauth:2.0:oob`添加另一个类型为 "**公用客户端（移动 & 桌面）**" 的重定向 uri。</span><span class="sxs-lookup"><span data-stu-id="88fa3-134">On the **Redirect URIs** page, add another redirect URI of type **Public client (mobile & desktop)**, with the URI `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="88fa3-135">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="88fa3-135">Select **Save**.</span></span>

    !["重定向 Uri" 页的屏幕截图](/tutorial/images/aad-redirect-uris.png)

## <a name="configure-the-sample"></a><span data-ttu-id="88fa3-137">配置示例</span><span class="sxs-lookup"><span data-stu-id="88fa3-137">Configure the sample</span></span>

1. <span data-ttu-id="88fa3-138">将**GraphTutorial/auth/AuthConfig 示例**文件重命名为**AuthConfig**。</span><span class="sxs-lookup"><span data-stu-id="88fa3-138">Rename the **GraphTutorial/auth/AuthConfig.ts.example** file to **AuthConfig.ts**.</span></span>
1. <span data-ttu-id="88fa3-139">编辑**AuthConfig**文件并进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="88fa3-139">Edit the **AuthConfig.ts** file and make the following changes.</span></span>
    1. <span data-ttu-id="88fa3-140">将`YOUR_APP_ID_HERE`替换为你从应用注册门户获取的**应用程序 Id** 。</span><span class="sxs-lookup"><span data-stu-id="88fa3-140">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

1. <span data-ttu-id="88fa3-141">在命令行界面（CLI）中，导航到**GraphTutorial**目录并运行以下命令以安装要求。</span><span class="sxs-lookup"><span data-stu-id="88fa3-141">In your command-line interface (CLI), navigate to the **GraphTutorial** directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

1. <span data-ttu-id="88fa3-142">在命令行界面（CLI）中，导航到**GraphTutorial/ios**目录并运行以下命令以安装要求。</span><span class="sxs-lookup"><span data-stu-id="88fa3-142">In your command-line interface (CLI), navigate to the **GraphTutorial/ios** directory and run the following command to install requirements.</span></span>

    ```Shell
    pod install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="88fa3-143">运行示例</span><span class="sxs-lookup"><span data-stu-id="88fa3-143">Run the sample</span></span>

### <a name="run-on-ios-simulator"></a><span data-ttu-id="88fa3-144">在 iOS 模拟器上运行</span><span class="sxs-lookup"><span data-stu-id="88fa3-144">Run on iOS Simulator</span></span>

<span data-ttu-id="88fa3-145">在 CLI 中运行以下命令，以在 iOS 模拟器中启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="88fa3-145">Run the following command in your CLI to start the application in an iOS Simulator.</span></span>

```Shell
react-native run-ios
```

### <a name="run-on-android-emulator"></a><span data-ttu-id="88fa3-146">在 Android 模拟器上运行</span><span class="sxs-lookup"><span data-stu-id="88fa3-146">Run on Android emulator</span></span>

<span data-ttu-id="88fa3-147">启动和 Android 仿真程序实例，并在 CLI 中运行以下命令，以在 Android 模拟器中启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="88fa3-147">Launch and Android emulator instance and run the following command in your CLI to start the application in an Android emulator.</span></span>

```Shell
react-native run-android
```
