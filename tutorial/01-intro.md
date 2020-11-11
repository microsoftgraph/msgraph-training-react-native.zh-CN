<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="52c19-101">本教程向您介绍如何构建使用 Microsoft Graph API 来检索用户的日历信息的响应本机应用程序。</span><span class="sxs-lookup"><span data-stu-id="52c19-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="52c19-102">如果您只想下载已完成的教程，可以下载或克隆 [GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-react-native)。</span><span class="sxs-lookup"><span data-stu-id="52c19-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52c19-103">先决条件</span><span class="sxs-lookup"><span data-stu-id="52c19-103">Prerequisites</span></span>

<span data-ttu-id="52c19-104">在开始本教程之前，您应在开发计算机上安装以下程序。</span><span class="sxs-lookup"><span data-stu-id="52c19-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="52c19-105">至少以下之一：</span><span class="sxs-lookup"><span data-stu-id="52c19-105">At least one of the following:</span></span>
  - <span data-ttu-id="52c19-106">需要 [Android Studio](https://developer.android.com/studio/) **和** [Java 开发工具包](https://jdk.java.net) (运行 android 版的示例) </span><span class="sxs-lookup"><span data-stu-id="52c19-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="52c19-107">运行 iOS) 上的示例所需的[Xcode](https://developer.apple.com/xcode/) (</span><span class="sxs-lookup"><span data-stu-id="52c19-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="52c19-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="52c19-108">Node.js</span></span>](https://nodejs.org)

<span data-ttu-id="52c19-109">您还应具有一个个人的 Microsoft 帐户，其中包含 Outlook.com 上的邮箱，或 Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="52c19-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="52c19-110">如果你没有 Microsoft 帐户，可以使用以下几种方法获取免费帐户：</span><span class="sxs-lookup"><span data-stu-id="52c19-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="52c19-111">你可以 [注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="52c19-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="52c19-112">你可以 [注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) 以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="52c19-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="52c19-113">本教程是使用响应本机 CLI 编写的，其中包含特定的先决条件，具体取决于您的操作系统和目标平台。</span><span class="sxs-lookup"><span data-stu-id="52c19-113">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="52c19-114">有关配置开发计算机的说明，请参阅 [响应原生入门](https://reactnative.dev/docs/environment-setup) 。</span><span class="sxs-lookup"><span data-stu-id="52c19-114">See [React Native Getting Started](https://reactnative.dev/docs/environment-setup) for instructions on configuring your development machine.</span></span> <span data-ttu-id="52c19-115">下面列出了用于本教程的版本。</span><span class="sxs-lookup"><span data-stu-id="52c19-115">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="52c19-116">本指南中的步骤可能适用于其他版本，但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="52c19-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="52c19-117">Android Studio 4.1 版与 Android 9.0 SDK</span><span class="sxs-lookup"><span data-stu-id="52c19-117">Android Studio version 4.1 with the Android 9.0 SDK</span></span>
> - <span data-ttu-id="52c19-118">Java 开发工具包版本12.0。2</span><span class="sxs-lookup"><span data-stu-id="52c19-118">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="52c19-119">Xcode 版本12。1</span><span class="sxs-lookup"><span data-stu-id="52c19-119">Xcode version 12.1</span></span>
> - <span data-ttu-id="52c19-120">Node.js 版本14.15。0</span><span class="sxs-lookup"><span data-stu-id="52c19-120">Node.js version 14.15.0</span></span>

## <a name="feedback"></a><span data-ttu-id="52c19-121">反馈</span><span class="sxs-lookup"><span data-stu-id="52c19-121">Feedback</span></span>

<span data-ttu-id="52c19-122">请在 [GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-react-native)中提供有关本教程的任何反馈。</span><span class="sxs-lookup"><span data-stu-id="52c19-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
