<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="a043b-101">本教程向您介绍如何构建使用 Microsoft Graph API 来检索用户的日历信息的响应本机应用程序。</span><span class="sxs-lookup"><span data-stu-id="a043b-101">This tutorial teaches you how to build an React Native app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="a043b-102">如果您只想下载已完成的教程，可以下载或克隆[GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-react-native)。</span><span class="sxs-lookup"><span data-stu-id="a043b-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a043b-103">先决条件</span><span class="sxs-lookup"><span data-stu-id="a043b-103">Prerequisites</span></span>

<span data-ttu-id="a043b-104">在开始本教程之前，您应在开发计算机上安装以下程序。</span><span class="sxs-lookup"><span data-stu-id="a043b-104">Before you start this tutorial, you should have the following installed on your development machine.</span></span>

- <span data-ttu-id="a043b-105">至少以下之一：</span><span class="sxs-lookup"><span data-stu-id="a043b-105">At least one of the following:</span></span>
  - <span data-ttu-id="a043b-106">[Android Studio](https://developer.android.com/studio/) **和** [Java 开发工具包](https://jdk.java.net)（在 Android 上运行示例所必需）</span><span class="sxs-lookup"><span data-stu-id="a043b-106">[Android Studio](https://developer.android.com/studio/) **and** [Java Development Kit](https://jdk.java.net) (required to run the sample on Android)</span></span>
  - <span data-ttu-id="a043b-107">[Xcode](https://developer.apple.com/xcode/) （在 iOS 上运行示例所必需）</span><span class="sxs-lookup"><span data-stu-id="a043b-107">[Xcode](https://developer.apple.com/xcode/) (required to run the sample on iOS)</span></span>
- [<span data-ttu-id="a043b-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="a043b-108">Node.js</span></span>](https://nodejs.org)

> [!NOTE]
> <span data-ttu-id="a043b-109">本教程是使用响应本机 CLI 编写的，其中包含特定的先决条件，具体取决于您的操作系统和目标平台。</span><span class="sxs-lookup"><span data-stu-id="a043b-109">This tutorial was written using the React Native CLI, which has specific prerequisites depending on your operating system and target platforms.</span></span> <span data-ttu-id="a043b-110">有关配置开发计算机的说明，请参阅[响应原生入门](https://facebook.github.io/react-native/docs/getting-started)。</span><span class="sxs-lookup"><span data-stu-id="a043b-110">See [React Native Getting Started](https://facebook.github.io/react-native/docs/getting-started) for instructions on configuring your development machine.</span></span> <span data-ttu-id="a043b-111">下面列出了用于本教程的版本。</span><span class="sxs-lookup"><span data-stu-id="a043b-111">The versions used for this tutorial are listed below.</span></span> <span data-ttu-id="a043b-112">本指南中的步骤可能适用于其他版本，但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="a043b-112">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="a043b-113">Android Studio 版本3.4.2 与 1.8.0 JRE 和 Android 9.0 SDK</span><span class="sxs-lookup"><span data-stu-id="a043b-113">Android Studio version 3.4.2 with the 1.8.0 JRE and the Android 9.0 SDK</span></span>
> - <span data-ttu-id="a043b-114">Java 开发工具包版本12.0。2</span><span class="sxs-lookup"><span data-stu-id="a043b-114">Java Development Kit version 12.0.2</span></span>
> - <span data-ttu-id="a043b-115">Xcode 版本10。3</span><span class="sxs-lookup"><span data-stu-id="a043b-115">Xcode version 10.3</span></span>
> - <span data-ttu-id="a043b-116">Node.js 版本10.16。0</span><span class="sxs-lookup"><span data-stu-id="a043b-116">Node.js version 10.16.0</span></span>

## <a name="feedback"></a><span data-ttu-id="a043b-117">反馈</span><span class="sxs-lookup"><span data-stu-id="a043b-117">Feedback</span></span>

<span data-ttu-id="a043b-118">请在[GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-react-native)中提供有关本教程的任何反馈。</span><span class="sxs-lookup"><span data-stu-id="a043b-118">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-react-native).</span></span>
