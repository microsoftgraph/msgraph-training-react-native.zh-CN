<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="09a47-101">在本节中，您将添加在用户日历上创建事件的功能。</span><span class="sxs-lookup"><span data-stu-id="09a47-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-the-new-event-screen"></a><span data-ttu-id="09a47-102">创建新的事件屏幕</span><span class="sxs-lookup"><span data-stu-id="09a47-102">Create the new event screen</span></span>

1. <span data-ttu-id="09a47-103">打开 **/graph/GraphManager.ts** ，并将以下函数添加到 `GraphManager` 类中。</span><span class="sxs-lookup"><span data-stu-id="09a47-103">Open **./graph/GraphManager.ts** and add the following function to the `GraphManager` class.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="CreateEventSnippet":::

    <span data-ttu-id="09a47-104">此函数使用 Graph SDK 创建新事件。</span><span class="sxs-lookup"><span data-stu-id="09a47-104">This function uses the Graph SDK to create a new event.</span></span>

1. <span data-ttu-id="09a47-105">在 **/screens** 中创建一个名为 **NewEventScreen** 的新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="09a47-105">Create a new file in the **./screens** named **NewEventScreen.tsx** and add the following code.</span></span>

    :::code language="typescript" source="../demo/GraphTutorial/screens/NewEventScreen.tsx" id="NewEventScreenSnippet":::

    <span data-ttu-id="09a47-106">考虑函数的功能 `createEvent` 。</span><span class="sxs-lookup"><span data-stu-id="09a47-106">Consider what the `createEvent` function does.</span></span> <span data-ttu-id="09a47-107">它 `MicrosoftGraph.Event` 使用表单中的值创建对象，然后将该对象传递给 `GraphManager.createEvent` 函数。</span><span class="sxs-lookup"><span data-stu-id="09a47-107">It creates a `MicrosoftGraph.Event` object using the values from the form, then passes that object to the `GraphManager.createEvent` function.</span></span>

1. <span data-ttu-id="09a47-108">打开 **./menus/DrawerMenu.tsx** 并将以下语句添加到 `import` 文件顶部。</span><span class="sxs-lookup"><span data-stu-id="09a47-108">Open **./menus/DrawerMenu.tsx** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import NewEventScreen from '../screens/NewEventScreen';
    ```

1. <span data-ttu-id="09a47-109">将下面的代码添加到 `<Drawer.Navigator>` 元素中，就在行的正上方 `</Drawer.Navigator>` 。</span><span class="sxs-lookup"><span data-stu-id="09a47-109">Add the following code inside the `<Drawer.Navigator>` element, just above the `</Drawer.Navigator>` line.</span></span>

    ```typescript
    { userLoaded &&
      <Drawer.Screen name='NewEvent'
        component={NewEventScreen}
        options={{drawerLabel: 'New event'}} />
    }
    ```

1. <span data-ttu-id="09a47-110">保存所做的更改，然后重新启动或刷新应用程序。</span><span class="sxs-lookup"><span data-stu-id="09a47-110">Save your changes and restart or refresh the app.</span></span> <span data-ttu-id="09a47-111">在菜单上选择 " **新建事件** " 选项，以转到新的事件窗体。</span><span class="sxs-lookup"><span data-stu-id="09a47-111">Select the **New event** option on the menu to get to the new event form.</span></span>

1. <span data-ttu-id="09a47-112">填写窗体，然后选择 " **创建** "。</span><span class="sxs-lookup"><span data-stu-id="09a47-112">Fill in the form and select **Create**.</span></span>

    ![新事件表单的屏幕截图](images/new-event-form.png)
