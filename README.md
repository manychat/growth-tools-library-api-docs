# ManyChat growth tools library API docs

This library provides additional opportunities when using ManyChat Growth Tools:
- Functionality for using headless checkbox widget
- Opportunity to initialize widgets for dynamically created elements

## Initialization

Loading of the library is done by using a script. The link to this script can be found in “Growth Tools” section (Setup tab, Install JavaScript Snippet). Loading is performed asynchronously, this is why before calling the library’s methods it’s necessary to wait for the library to load. This is what the purpose of `mcAsyncInit` callback is. After loading, global MC variable becomes available and  provides access to functionality. 

```html
<script src="//widget.manychat.com/YOUR_PAGE_ID.js" async="async"></script>
<script>
  window.mcAsyncInit = function() {
    // MC variable is available now
    console.log(MC);
  };
</script>
```

## Core Methods

| Method  | Description |
| ------------- | ------------- |
| `MC.parse()`  | Finds widget elements on a page (e.g. `<div class="mcwidget-checkbox" data-widget-id="420"></div>`) and renders them. This functions is called on the library’s loading. It can be useful if you need to render an element that was added to the DOM after the library has loaded.   |
| `MC.getWidget(widgetId)`  | Returns the widget’s object by ID. With this object you can listen to the widget’s events and call methods. Widget’s ID can be obtained from the snippet in Growth Tools.   |

## Checkbox Widget Methods
_All methods and properties listed below are available only for “Checkbox” widget type._

| Method  | Description |
| ------------- | ------------- |
| `.on(eventName, callback)`  | Subscribe to an event eventName. Available values for `eventName`: <ul><li>`checked` - change of checked checkbox status</li><li>`submitted` - widget submitting</li></ul> |
| `.off(event[, callback])`  | Unsubscribe from an event or all events. If no callback is provided, it unsubscribes you from all events  |
| `.submit()`  | Method for sending a checkbox confirmation. Has to be called upon a button click for opt-in confirmation. |
| `.checked`  | This property allows to check current status of a widget.  |
| `.ref`  | Ref string is used when the widget was submitted, available only after the submitting.|
| `.userRef	`  | User identifier is used when the widget was submitted, available only after the submitting.  |

## Overlay Widget Methods
_All methods and properties listed below are available only for “Bar”, "Slide-In", "Modal" and "Page Takeover" widget types._

| Method  | Description |
| ------------- | ------------- |
| `.open()`  | Open widget.  |
| `.close()`  | Close widget.  |
