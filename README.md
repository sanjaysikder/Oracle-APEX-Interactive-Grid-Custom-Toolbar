# Oracle APEX Interactive Grid Custom Toolbar

## Overview

This JavaScript customization enhances the Oracle APEX Interactive Grid (IG) toolbar by:

* Adding a **Delete Row** button
* Adding a **Refresh** button
* Adding a **Reset Report** button
* Adding a **Download** button
* Customizing the **Add Row** button
* Customizing the **Save** button
* Applying modern Font Awesome icons
* Highlighting important actions using the `hot` property

## Features

| Feature      | Description                        |
| ------------ | ---------------------------------- |
| Add Row      | Quickly add new records            |
| Delete Row   | Delete selected rows               |
| Save         | Save all pending changes           |
| Refresh      | Reload grid data                   |
| Reset Report | Restore report settings to default |
| Download     | Export grid data                   |

---

## JavaScript Code

```javascript
function(config) {

    var $ = apex.jQuery,
        toolbarData = $.apex.interactiveGrid.copyDefaultToolbar(),
        toolbarGroup = toolbarData.toolbarFind("actions3"),

        addrowAction = toolbarData.toolbarFind("selection-add-row"),
        saveAction   = toolbarData.toolbarFind("save");

    // Add Delete Button
    toolbarGroup.controls.push({
        type: "BUTTON",
        action: "selection-delete",
        icon: "fa fa-trash",
        iconBeforeLabel: true,
        hot: true
    });

    // Add Refresh Button
    toolbarGroup.controls.push({
        type: "BUTTON",
        action: "refresh",
        icon: "fa fa-refresh",
        iconBeforeLabel: true
    });

    // Add Reset Report Button
    toolbarGroup.controls.push({
        type: "BUTTON",
        action: "reset-report",
        icon: "fa fa-undo",
        iconBeforeLabel: true
    });

    // Add Download Button
    toolbarGroup.controls.push({
        type: "BUTTON",
        action: "show-download-dialog",
        icon: "fa fa-download",
        iconBeforeLabel: true
    });

    // Customize Add Row Button
    addrowAction.label = "Add Row";
    addrowAction.icon = "fa fa-plus";
    addrowAction.iconBeforeLabel = true;
    addrowAction.hot = true;

    // Customize Save Button
    saveAction.label = "Save";
    saveAction.icon = "fa fa-save";
    saveAction.iconBeforeLabel = true;
    saveAction.hot = true;

    config.toolbarData = toolbarData;

    return config;
}
```

---

## Installation

1. Open your Interactive Grid region.

2. Navigate to:

   **Attributes → Advanced → JavaScript Initialization Code**

3. Paste the JavaScript code above.

4. Save and run the page.

---

## Button Configuration

### Delete Button

```javascript
{
    type: "BUTTON",
    action: "selection-delete",
    icon: "fa fa-trash",
    iconBeforeLabel: true,
    hot: true
}
```

Deletes selected rows from the Interactive Grid.

### Refresh Button

```javascript
{
    type: "BUTTON",
    action: "refresh",
    icon: "fa fa-refresh"
}
```

Reloads data from the database.

### Reset Report Button

```javascript
{
    type: "BUTTON",
    action: "reset-report",
    icon: "fa fa-undo"
}
```

Restores the report to its default settings.

### Download Button

```javascript
{
    type: "BUTTON",
    action: "show-download-dialog",
    icon: "fa fa-download"
}
```

Opens the Interactive Grid download/export dialog.

---

## Compatibility

* Oracle APEX 22.2+
* Oracle APEX 23.x
* Oracle APEX 24.x

---

## Screenshot

After applying this customization, the toolbar will contain:

```text
[ Add Row ] [ Save ] [ Delete ] [ Refresh ] [ Reset ] [ Download ]
```

with modern Font Awesome icons.

---

## Thank you

**Sanjay Sikder**

💼 Connect with me on **[LinkedIn](https://www.linkedin.com/in/sanjay-sikder/)**.
