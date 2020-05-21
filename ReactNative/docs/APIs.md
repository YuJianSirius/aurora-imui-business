# API

[中文文档](./APIs_zh.md)

#### Usage

```javascript
import {
  NativeModules,
} from 'react-native';

import IMUI from 'aurora-imui-react-native';
var MessageList = IMUI.MessageList;
var ChatInput = IMUI.ChatInput;
const AuroraIMUIController = IMUI.AuroraIMUIController; // the IMUI controller, use it to operate  messageList and ChatInput.

// add MessageList and ChatInput in render() 
<MessageList />
<ChatInput />
```

Refer to iOS,Android example

> [Example usage](../sample/App.js)



- [AuroraIMUIController](#auroraimuicontroller)
  - [appendMessages](#appendmessages)
  - [updateMessage](#updatemessage)
  - [insertMessagesToTop](#insertmessagestotop)
  - [stopPlayVoice](#stopplayvoice)
  - [removeMessage](#removeMessage)
  - [removeAllMessage](#removeAllMessage)
  - [hidenFeatureView](#hidenfeatureview)
  - [Event](#auroraimuicontrollerevent)
    - [MessageListDidLoadListener](#messagelistdidloadlistener)


- [MessageList](#messagelist)
  - [Props Event]()
    - [onAvatarClick](#onavatarclick)
    - [onMsgClick](#onmsgclick)
    - [onStatusViewClick](#onstatusviewclick)
    - [onPullToRefresh](#onpulltorefresh)
    - [onTouchMsgList](#ontouchmsglist) 
  - [Props customizable style]()
    - [sendBubble](#sendbubble)
    - [receiveBubble](#receivebubble)
    - [sendBubbleTextColor](#sendbubbletextcolor)
    - [receiveBubbleTextColor](#receivebubbletextcolor)
    - [sendBubbleTextSize](#sendbubbletextsize)
    - [receiveBubbleTextSize](#receivebubbletextsize)
    - [sendBubblePadding](#sendbubblepadding)
    - [receiveBubblePadding](#receivebubblepadding)
    - [dateTextSize](#datetextsize)
    - [dateTextColor](#datetextcolor)
    - [datePadding](#datepadding)
    - [dateBackgroundColor](#dateBackgroundColor)
    - [dateCornerRadius](#dateCornerRadius)
    - [avatarSize](#avatarsize)
    - [avatarCornerRadius](#avatarcornerradius)
    - [isShowDisplayName](#isShowdisplayname)
    - [isShowIncomingDisplayName](#isShowIncomingDisplayName)
    - [isShowOutgoingDisplayName](#isShowOutgoingDisplayName)
    - [displayNameTextSize](#displayNameTextSize)
    - [displayNameTextColor](#displayNameTextColor)
    - [displayNamePadding](#displayNamePadding)
    - [eventTextColor](#eventTextColor)
    - [eventTextSize](#eventTextSize)
    - [eventTextPadding](#eventTextPadding)
    - [eventBackgroundColor](#eventBackgroundColor)
    - [eventCornerRadius](#eventCornerRadius)
    - [eventTextLineHeight](#eventTextLineHeight)
    - [messageListBackgroundColor](#messagelistbackgroundcolor)
    - [maxBubbleWidth](#maxBubbleWidth)
    - [messageTextLineHeight](#messageTextLineHeight)
    - [isAllowPullToRefresh](#isallowpulltorefresh)
- [ChatInput](#chatinput)
  - [Props customizable style]()
    - [customLayoutItems](#customlayoutitemsios-only)
    - [chatInputBackgroundColor](#chatInputBackgroundColor)
    - [showSelectAlbumBtn](#showselectalbumbtnandroid-only)
    - [showRecordVideoBtn](#showRecordVideoBtnandroid-only) 
    - [inputPadding](#inputPadding)
    - [inputTextColor](#inputTextColor)
    - [inputTextSize](#inputTextSize)
    - [inputTextLineHeight](#inputTextLineHeight)
  - [Props Event]()
    - [onSendText](#onsendtext)
    - [onSendGalleryFile](#onsendgalleryfile)
    - [onTakePicture](#ontakepicture)
    - [onStartRecordVideo](#onstartrecordvideo)
    - [onFinishRecordVideo](#onfinishrecordvideo)
    - [onCancelRecordVideo](#oncancelrecordvideo)
    - [onStartRecordVoice](#onstartrecordvoice)
    - [onFinishRecordVoice](#onfinishrecordvoice)
    - [onCancelRecordVoice](#oncancelrecordvoice)
    - [onSwitchToMicrophoneMode](#onswitchtomicrophonemode)
    - [onSwitchToGalleryMode](#onswitchtogallerymode)
    - [onSwitchToCameraMode](#onswitchtocameramode)
    - [onSwitchToEmojiMode](#onswitchtoemojimode)
    - [onSizeChange](#onsizechange)
    - [onFullScreen](#onfullscreen)
    - [onRecoverScreen](#onrecoverscreen)
    - [onTouchEditText](#ontouchedittext)
    - [onClickSelectAlbum](#onClickSelectAlbum)

## AuroraIMUIController

For append/update/insert message to MessageList, you will use `AuroraIMUIController`(Native Module) to send event to native.

#### appendMessages

param: [{[message](./Models.md#message)}]

Append message to bottom of the MessageList, the display order will be the same as the array of message's.

example:

```javascript
var messages = [{
	msgId: "1",
	status: "send_going",
	msgType: "text",
	text: "Hello world",
	isOutgoing: true,
	fromUser: {
		userId: "1",
		displayName: "Ken",
		avatarPath: "ironman"
	},
	timeString: "10:00"
}];
AuroraIMUIController.appendMessages(messages);
```

#### updateMessage

param: {[message](./Models.md#message)}

Update message, since the message status was changed, you should use this method to update your message.

example:

```javascript
var message = {
	msgId: "1",
	status: "send_going",
	msgType: "text",
	text: text,
	isOutgoing: true,
	fromUser: {
		userId: "1",
		displayName: "Ken",
		avatarPath: "ironman"
	},
	timeString: "10:00",
};
AuroraIMUIController.updateMessage(message);
```

#### insertMessagesToTop

param: [{[message](./Models.md#message)}]

Insert messages to the top of the MessageList, usually use this method to load history messages. **The messages to be inserted must be sorted chronologically.**

example:

```javascript
var messages = [{
    msgId: "1",
    status: "send_succeed",
    msgType: "text",
    text: "This",
    isOutgoing: true,
    fromUser: {
	  userId: "1",
	  displayName: "Ken",
	  avatarPath: "ironman"
    },
    timeString: "10:00",
  },{
    msgId: "2",
	status: "send_succeed",
	msgType: "text",
	text: "is",
	isOutgoing: true,
	fromUser: {
		userId: "1",
		displayName: "Ken",
		avatarPath: "ironman"
    },
    timeString: "10:10",
},{
    msgId: "3",
	status: "send_succeed",
	msgType: "text",
	text: "example",
	isOutgoing: true,
	fromUser: {
		userId: "1",
		displayName: "Ken",
		avatarPath: "ironman"
    },
    timeString: "10:20",
}];
AuroraIMUIController.insertMessagesToTop(messages);
```

#### stopPlayVoice

Stop playing voice, including media players in ChatInput and MessageList.

example:

```
AuroraIMUIController.stopPlayVoice()
```

#### removeMessage
param: string

Remove message by message id.

example:
```js
AuroraIMUIController.removeMessage("1")
```

#### removeAllMessage
Remove all messages.

example:
```js
AuroraIMUIController.removeAllMessage()
```

#### hidenFeatureView

hiden inputView's featureView.

example:

```
AuroraIMUIController.hidenFeatureView()
```

#### MessageListDidLoadListener

- addMessageListDidLoadListener(cb)

  The initialization of `AuroraIMUIController` will finish before `MessageListView` 's，If you need do something to `MessageListView` (such as append, insert, update and remove) you need to wait untill `MessageListDidLoad` has been called.

  example:

  ```javascript
  AuroraIMUIController.addMessageListDidLoadListener(()=> {
    // do something ex: insert message to top
  })
  ```

- removeMessageListDidLoadListener(cb)

  Remove listener of `MessageListDidLoad` 

  example:

  ```javascript
  AuroraIMUIController.removeMessageListDidLoadListener(cb)
  ```


## MessageList

#### MessageList Event Callback

------

#### onAvatarClick

**PropTypes.function:** ```( message ) => { }```

Fires when click avatar.

message param: { "message":  [message](./Models.md#message)  }

------

#### onMsgClick

**PropTypes.function:**  ```(message) => { } ```

Fires when click message bubble。

message param: { "message":  [message](./Models.md#message)  }

------

#### onStatusViewClick

**PropTypes.function:**  ```(message) => { } ```

Fires when click status view.

message param: { "message":  [message](./Models.md#message)  }

------

#### onPullToRefresh

**PropTypes.function:** ```() => { } ```

Fires when pull MessageList to top, example usage: please refer sample's onPullToRefresh method.

**In Android, you should put `onPullToRefresh` in `AndroidPtrLayout`, please refer sample/app/app.js for more detail.**

------

#### onTouchMsgList

**PropTypes.function:** ```() => { } ```

Fires when touch message list.

------

#### onBeginDragMessageList (iOS only)

**PropTypes.function**

------



#### MessageList custom style

**In android, if your want to define your chatting bubble, you need to put a drawable file in drawable folder, and that image file must be nine patch drawable file, see our example for detail.**

**In iOS, if your want to define your chatting bubble,you need to put a image file to you xcode,and specifies sendBubble.imageName or receiveBubble.imageName to image name.**

------

#### sendBubble

**PropTypes.object：**```{ imageName: string,  padding: { left: number,top: number,right: number,bottom: number}```

------

#### receiveBubble

**PropTypes.object：**```{ imageName: string,  padding: { left: number,top: number,right: number,bottom: number}```

------

#### sendBubbleTextColor

**PropTypes.string:** 

Set outgoing message's text color, ```sendBubbleTextColor="#000000"```.

------

#### receiveBubbleTextColor

**PropTypes.string**

Set incoming message's text color, ```sendBubbleTextColor="#000000"```.

------

#### sendBubbleTextSize

**PropTypes.number**

Set outgoing message's text size.

------

#### receiveBubbleTextSize

**PropTypes.number**

Set incoming message's text size.

------

#### sendBubblePadding

**PropTypes.object：** ```{ left: number, top: number, right: number, bottom: number }```

Set outgoing message's bubble padding.

------

#### receiveBubblePadding

**PropTypes.object:** ```{ left: number, top: number, right: number, bottom: number }```

Set incoming message's bubble padding.

------

#### dateTextSize

**PropTypes.number:** 

Set date text size of message.

------

#### dateTextColor

**PropTypes.string:**

Set date text color of message, ```dateTextColor="#000000"```。

------

#### datePadding

**PropTypes.object:** `{ left: number, top: number, right: number, bottom: number}` 

Set date padding.

Example: `datePadding={left: 5, top: 10, right: 5, bottom: 10}`

------

#### dateBackgroundColor

**PropTypes.string**

Set the background color of date.

Example: `dateBackgroundColor={"#cecece"}`

------

#### dateCornerRadius

**PropTypes.number**

Set the background corner radius of date.

Example: `dateCornerRadius={5}`

------

#### avatarSize

**PropTypes.object:**  ```{ width: number, height: number }```

This property including width and height.

Example: ```avatarSize = {width: 50, height: 50}```。

------

#### avatarCornerRadius

**PropTypes.number:** 

Set fillet radius of avatar.

Example: ```avatarCornerRadius = {6}```。

------

#### isShowDisplayName

**PropTypes.bool:**

Show display name or not.

Example: ```isShowDisplayName={ture}```。

------

#### isShowIncomingDisplayName

**PropTypes.bool:**

Set Show receiver's display name or not.

Example: `isShowIncomingDisplayName={true}`

------

#### isShowOutgoingDisplayName

**PropTypes.bool:**

Set show sender's display name or not.

Example: `isShowOutgoingDisplayName={false}`

------

#### displayNameTextSize

**PropTypes.number**

Set the text size of display name.

Example: `displayNameTextSize={14}`



------

#### displayNameTextColor

**PropTypes.string**

Set the color of display name.

Example: `displayNameTextColor={"#cecece"}`

------

#### displayNamePadding

**PropTypes.object** = {left: number, top: number, right: number, bottom: number}

Set padding of display name.

Example: `displayNamePadding={left: 5, top: 0, right: 0, bottom: 5}`

------

#### messageListBackgroundColor

**PropTypes.string:**

Set messageList' background  color.

Example: `messageListBackgroundColor={"#f3f3f3"}`

------

#### maxBubbleWidth

**PropTypes.number**

Set the max width of message bubble, the value is the percentage of mobile's width.

Example: `maxBubbleWidth={0.7}` means set the max bubble width to 70% of mobile width.

------

#### messageTextLineHeight

**PropTypes.number**

Set text message's line spacing.

Example: `messageTextLineHeight={5}`

------

#### isAllowPullToRefresh

**PropTypes.bool:**

Show pull-to-refresh or not.

Example: ```isAllowPullToRefresh={ture}```。

## ChatInput

### Props customizable style

***

#### customLayoutItems

**PropTypes.string:** 

Customize ChatInput feature and layout。

Eample: 

```
// You can put item into ChatInput's left/right/bottom part，(Can’t be repeated！)
customLayoutItems={{
            left: ['voice'],
            right: ['send'],
            bottom: ['gallery','emoji','camera']
		}} 
		

// if you don't put element in left/right/bottom ChatInput will hidden the part.
customLayoutItems={{
            left: ['voice'],
            right: ['send']
		}} 
```

#### chatInputBackgroundColor

**PropTypes.string:**

Set chatInput' background  color.

Example:  ```chatInputBackgroundColor="#000000"```

***

#### showSelectAlbumBtn(Android Only)
**PropTypes.bool:**

Set the visibility of the select album button.

Example: ```showSelectAlbumBtn={true}```

------

#### showRecordVideoBtn(Android Only)
**PropTypes.bool:**

Set the visibility of the record video button.

Example: ```showRecordVideoBtn={true}```

------
### inputPadding

**PropTypes.object:** {left: number, top: number, right: number, bottom: number}

Set the padding of TextInput.

Example: `inputPadding={left:5, top:0, right:5, bottom:0}`

***

### inputTextColor

**PropTypes.string:** {"#xxxxxx"}

Set the text color of TextInput.

Example: `inputTextColor={"#808080"}`

***

### inputTextSize

**PropTypes.numbser:** {numbser}

Set the text size of TextInput.

Example: `inputTextSize={14}`

***

### inputTextLineHeight

**PropTypes.number:**{numbser}

Set the text line spacing of TextInput.

Example: `inputTextLineHeight={2}`

------

### ChatInput Event Callback

------

#### onSendText

**PropTypes.function:** ```(text) => {}```

After inputting text, fires when click send button, the text is the sending string(`text: string`).

------

#### onSendGalleryFiles

**PropTypes.function:** ```(result) => {}```

After choosing picutres or videos, fires when click send button.

 Result's type is ```{mediaFiles: [string]}```, including choosing files' path.

------

#### onTakePicture

**PropTypes.function:** ```(result) => {}```

Fires when click take picture button, result's type is ```{mediaPath: string}```。

------

#### onStartRecordVideo

**PropTypes.function:** ``` () => {}```

Fires when click record video button.

------

#### onFinishRecordVideo

**PropTypes.function:**``` (result) => {}```

 Fires when finished recording video. 

Result's type is  ```{mediaPath: string, duration: number}```。

------

#### onCancelRecordVideo

**PropTypes.function:**

Fires when click cancel record video button.

------

#### onStartRecordVoice

**PropTypes.function:**```() => {} ```

 Fires when click record audio button.

------

#### onFinishRecordVoice

**PropTypes.function:**``` (result) => {}```

After finishing recording audio, fires when finger left from screen,

Result's type is ```{mediaPath: string, duration: number}```。

------

#### onCancelRecordVoice

**PropTypes.function:**```() => {} ```

 Fires when finger move to cancel record zone, and left from screen.

------

#### onSwitchToMicrophoneMode

**PropTypes.function:** ```() => {} ```

Fires when click microphone button in menu.

------

#### onSwitchToGalleryMode

**PropTypes.function:** ```() => {} ```

Fires when click picture button in menu.

------

#### onSwitchToCameraMode

**PropTypes.function:** ```() => {} ```

 Fires when click camera button in menu.

------

#### onSwitchToEmojiMode

**PropTypes.function:** ```() => {} ```

Fires when click emoji button in menu.

------

#### onSizeChange

**PropTypes.function:** `({width: number, height: number}) => {}`

Fires when ChantInput's size change。

***

#### onFullScreen

**PropTypes.function:** `() => {}`

Fires when camera switch into full screen mode.

***

#### onRecoverScreen

**PropTypes.function:** `() => {}`

Fires when camera cancel full screen mode.

***

#### onTouchEditText

**PropTypes.function:** （Android only）

Fires when click input view text input.

***

#### onClickSelectAlbum

**PropTypes.function:** `() => {}`（Android only）

Fires when click select album button(you can through [showSelectAlbumBtn](#showSelectAlbumBtn) change the visibility )

***