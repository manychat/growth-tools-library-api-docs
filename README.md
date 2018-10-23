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

## Embed Widgets Initialization

To initialize an embed widget (button or box), you need to add an additional code into your page where you want the widget to appear.
In general, this code looks like this:

```html
<div class="mcwidget-embed" data-widget-id="YOUR_WIDGET_ID" data-widget-payload="OPTIONAL_PAYLOAD"></div>
```
You can place the code in several places on the same page. An instance of the widget will be initialized at each place. 
For each instance of the widget, you can set an optional payload - this is the data that will be saved in the Custom User Field specified in the settings of the widget.
To set the payload for the widget instance, set `data-widget-payload` attribute for an element or use the` setPayload` method described below.
 

## Core Methods

| Method  | Description |
| ------------- | ------------- |
| `MC.parse()`  | Finds widget elements on a page (e.g. `<div class="mcwidget-checkbox" data-widget-id="420"></div>`) and renders them. This functions is called on the library’s loading. It can be useful if you need to render an element that was added to the DOM after the library has loaded.   |
| `MC.getWidget(widgetId or DOM Element)`  | Returns the widget’s object by widget ID or by DOM Element of Embed widget instance. With this object you can listen to the widget’s events and call methods. Widget’s ID can be obtained from the snippet in Growth Tools.   |
| `MC.getWidgetList()`  | Returns a list of all active widgets.   |

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
| `.setPayload(refPayload)`  | Set the ref payload for the widget. Value must be a string. Max 200 characters. Valid characters are `a-z A-Z 0-9 +/=-._`  |

## Customer Chat Widget Methods
_All methods and properties listed below are available only for “Customer Chat” widget type._

### Rate Limit
Each Customer Chat method is limited to 1 call per 5 seconds.

| Method  | Description |
| ------------- | ------------- |
| `.open(shouldOpenDialog)`  | Open widget. You can use the `shouldOpenDialog` parameter to decide if the dialog should also be opened.  |
| `.close()`  | Close entire widget.  |
| `.openDialog()`  | Open widget dialog.  |
| `.closeDialog()`  | Close widget dialog.  |
| `.setLoggedInGreeting(text)`  | Set the greeting text for logged in user.  |
| `.setLoggedOutGreeting(text)`  | Set the greeting text for logged out user.  |
| `.setPayload(refPayload)`  | Set the ref payload for the widget. Value must be a string  |
| `.set(changes)` | Set the greeting text and/or the ref payload params. `changes` is a JSON object with the new values. Available param names: `loggedInGreeting`, `loggedOutGreeting`, `refPayload` |


## Embed Widget Methods
_All methods and properties listed below are available only for “Button” and "Box" widget types._

To execute methods on a widget, you need to get a widget instance object.
You can’t get it by passing the `widgetId` to the method `MC.getWidget` because there can be several instances of the widget on the page at the same time.
Therefore, to get an instance object, you should pass the Widget DOM Element as parameter when calling `MC.getWidget`, for example

```html
<!-- your code snippet -->
<div id="test-widget" class="mcwidget-embed" data-widget-id="420"></div>
```

```javascript
const widgetInstanceElement = document.getElementById('test-widget')
const widget = MC.getWidget(widgetInstanceElement)
widget.setPayload('custom_payload')
```

| Method  | Description |
| ------------- | ------------- |
| `.setPayload(refPayload)`  | Set the ref payload for the widget. Value must be a string. Max 200 characters. Valid characters are `a-z A-Z 0-9 +/=-._`  |


## Links
- [Example of using Checkbox widget](https://github.com/manychat/checkbox-growth-tools-example)
- [Example of using Customer Chat widget](https://github.com/manychat/customer-chat-growth-tools-example)