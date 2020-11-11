<!-- markdownlint-disable MD002 MD041 -->

在本节中，您将添加在用户日历上创建事件的功能。

## <a name="create-the-new-event-screen"></a>创建新的事件屏幕

1. 打开 **/graph/GraphManager.ts** ，并将以下函数添加到 `GraphManager` 类中。

    :::code language="typescript" source="../demo/GraphTutorial/graph/GraphManager.ts" id="CreateEventSnippet":::

    此函数使用 Graph SDK 创建新事件。

1. 在 **/screens** 中创建一个名为 **NewEventScreen** 的新文件，并添加以下代码。

    :::code language="typescript" source="../demo/GraphTutorial/screens/NewEventScreen.tsx" id="NewEventScreenSnippet":::

    考虑函数的功能 `createEvent` 。 它 `MicrosoftGraph.Event` 使用表单中的值创建对象，然后将该对象传递给 `GraphManager.createEvent` 函数。

1. 打开 **./menus/DrawerMenu.tsx** 并将以下语句添加到 `import` 文件顶部。

    ```typescript
    import NewEventScreen from '../screens/NewEventScreen';
    ```

1. 将下面的代码添加到 `<Drawer.Navigator>` 元素中，就在行的正上方 `</Drawer.Navigator>` 。

    ```typescript
    { userLoaded &&
      <Drawer.Screen name='NewEvent'
        component={NewEventScreen}
        options={{drawerLabel: 'New event'}} />
    }
    ```

1. 保存所做的更改，然后重新启动或刷新应用程序。 在菜单上选择 " **新建事件** " 选项，以转到新的事件窗体。

1. 填写窗体，然后选择 " **创建** "。

    ![新事件表单的屏幕截图](images/new-event-form.png)
