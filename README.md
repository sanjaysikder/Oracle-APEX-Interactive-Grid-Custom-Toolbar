# Oracle APEX Interactive Grid Custom Toolbar with Create, Delete Row, Refresh, Download, Save, Reset Report Button

## Overview

This JavaScript customization enhances the Oracle APEX Interactive Grid (IG) toolbar by:

* Adding a **Create** button
* Adding a **Delete Row** button
* Adding a **Refresh** button
* Adding a **Reset Report** button
* Adding a **Download** button
* Customizing the **Add Row** button
* Customizing the **Save** button
* Applying modern Font Awesome icons
* Highlighting important actions using the `hot` property

## Features

| Feature      | Description                              |
| ------------ | ---------------------------------------- |
| Create       | Open a modal dialog for creating records |
| Add Row      | Quickly add new records                  |
| Delete Row   | Delete selected rows                     |
| Save         | Save all pending changes                 |
| Refresh      | Reload grid data                         |
| Reset Report | Restore report settings to default       |
| Download     | Export grid data                         |

---

## Create Button Configuration

The Create button is added to the right side of the Interactive Grid toolbar and can be used to open a Modal Dialog page for data entry.

### JavaScript Configuration

```javascript
actions4.controls.push({
    type: "BUTTON",
    hot: true,
    icon: "fa fa-plus-circle",
    iconBeforeLabel: true,
    action: "create-record"
});
```

### Register Custom Action

The following code has been added inside the **JavaScript Initialization Code** sect্যেছ

```javascript
config.initActions = function(actions) {

    actions.add({
        name: "create-record",
        label: "Create",

        action: function(event, focusElement) {

            apex.theme42.dialog(
                apex.item("P5_CREATE_URL").getValue(),
                {
                    title: "Create Record",
                    h: "auto",
                    w: "720",
                    mxw: "960",
                    modal: true,
                    dlgCls: "t-Dialog-page--standard"
                },
                "",
                focusElement
            );

            return true;
        }
    });

};
```

### Hidden Page Item

Create a hidden page item:

```text
P5_CREATE_URL
```

#### Source Settings

| Property             | Value         |
| -------------------- | ------------- |
| Source Type          | Function Body |
| Language             | PL/SQL        |
| PL/SQL Function Body | See below     |

```plsql
BEGIN
    RETURN apex_page.get_url(
        p_page        => 27,
        p_clear_cache => '27',
        p_plain_url   => TRUE
    );
END;
```

> Replace page **27** with your Modal Dialog Form page number.

---

## Complete JavaScript Initialization Code

```javascript
function(config) {

    var $ = apex.jQuery,
        toolbarData = $.apex.interactiveGrid.copyDefaultToolbar(),
        actions3 = toolbarData.toolbarFind("actions3"),
        actions4 = toolbarData.toolbarFind("actions4"),

        addrowAction = toolbarData.toolbarFind("selection-add-row"),
        saveAction   = toolbarData.toolbarFind("save");

    actions3.controls.push({
        type: "BUTTON",
        action: "selection-delete",
        icon: "fa fa-trash",
        iconBeforeLabel: true,
        hot: true
    });

    actions3.controls.push({
        type: "BUTTON",
        action: "refresh",
        icon: "fa fa-refresh",
        iconBeforeLabel: true
    });

    actions3.controls.push({
        type: "BUTTON",
        action: "reset-report",
        icon: "fa fa-undo",
        iconBeforeLabel: true
    });

    actions3.controls.push({
        type: "BUTTON",
        action: "show-download-dialog",
        icon: "fa fa-download",
        iconBeforeLabel: true
    });

    actions4.controls.push({
        type: "BUTTON",
        action: "create-record",
        icon: "fa fa-plus-circle",
        iconBeforeLabel: true,
        hot: true
    });

    addrowAction.label = "Add Row";
    addrowAction.icon = "fa fa-plus";
    addrowAction.iconBeforeLabel = true;
    addrowAction.hot = true;

    saveAction.label = "Save";
    saveAction.icon = "fa fa-save";
    saveAction.iconBeforeLabel = true;
    saveAction.hot = true;

    config.initActions = function(actions) {

        actions.add({
            name: "create-record",
            label: "Create",

            action: function(event, focusElement) {

                apex.theme42.dialog(
                    apex.item("P5_CREATE_URL").getValue(),
                    {
                        title: "Create Record",
                        h: "auto",
                        w: "720",
                        mxw: "960",
                        modal: true,
                        dlgCls: "t-Dialog-page--standard"
                    },
                    "",
                    focusElement
                );

                return true;
            }
        });

    };

    config.toolbarData = toolbarData;

    return config;
}
```

---

## Installation

1. Open the Interactive Grid region.

2. Navigate to:

   **Attributes → Advanced → JavaScript Initialization Code**

3. Paste the JavaScript code.

4. Create the hidden item `P5_CREATE_URL`.

5. Create a Modal Dialog Form page.

6. Run the application.

---

## Screenshot

```text
[ Add Row ] [ Save ] [ Delete ] [ Refresh ] [ Reset ] [ Download ]                       [ Create ]
```

---

## Notes

* The target page should be configured as a **Modal Dialog**.
* If the target page contains an editable Interactive Grid, ensure a valid **Primary Key Column** is defined.
* Compatible with Universal Theme (Theme 42).
* Uses native Oracle APEX Interactive Grid actions.

---

## Compatibility

* Oracle APEX 22.2 or higher

---

## Author

**Sanjay Sikder**

### Contact

* LinkedIn: https://www.linkedin.com/in/sanjay-sikder/
* Email: [sanjaysikder71@gmail.com](mailto:sanjaysikder71@gmail.com)
* GitHub: https://github.com/SanjaySikder
