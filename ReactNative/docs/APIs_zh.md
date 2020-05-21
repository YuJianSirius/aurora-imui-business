# API

[English Document](./APIs.md)

#### 用法

```javascript
import {
  NativeModules,
} from 'react-native';

import IMUI from 'aurora-imui-react-native';
var MessageList = IMUI.MessageList;
var ChatInput = IMUI.ChatInput;
const AuroraIMUIController = IMUI.AuroraIMUIController; // the IMUI controller, use it to operate  messageList and ChatInput.

// render() 中加入视图标签
<MessageList />
<ChatInput />
```
详情可以参考 iOS Android 示例
> [Example 用法](../sample/App.js)



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

  - [Props 事件]()
    - [onAvatarClick](#onavatarclick)
    - [onMsgClick](#onmsgclick)
    - [onStatusViewClick](#onstatusviewclick)
    - [onPullToRefresh](#onpulltorefresh)
    - [onTouchMsgList](#ontouchmsglist) 
  - [Props 自定义样式]()
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
  - [Props 事件]()
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
    - [onTouchEditText](#ontouchedittext)
    - [onSizeChange](#onsizechange)
    - [onFullScreen](#onfullscreen)
    - [onRecoverScreen](#onrecoverscreen)
    - [onClickSelectAlbum](#onClickSelectAlbum)


## AuroraIMUIController

  插入，更新，增加消息到 MessageList, 你需要使用 AuroraIMUIController (Native Module) 来发送事件到 Native。

#### appendMessages

参数：[{[message](./Models.md#message)}]

添加消息到 MessageList 底部，顺序为数组顺序。

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

参数：{[message](./Models_zh.md#message)}

更新消息，可以使用该方法更新消息状态。

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

参数：[{[message](./Models_zh.md#message)}]

将消息列表插入到聊天列表顶部。**被插入的消息列表必须按照时间顺序排序。**

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



#### removeMessage
param: string

根据消息 id 删除消息

example:
```js
AuroraIMUIController.removeMessage("1")
```

#### removeAllMessage
清空所有消息

example:
```js
AuroraIMUIController.removeAllMessage()
```
#### hidenFeatureView

隐藏 inputView 的展开视图。

```
AuroraIMUIController.hidenFeatureView()
```

#### stopPlayVoice

停止正在播放的音频，这里会停止所有的声音，包括 ChatInput 和 MessageList 正在播放的声音。

example:

```
AuroraIMUIController.stopPlayVoice()
```

#### MessageListDidLoadListener

- addMessageListDidLoadListener(cb)

  `AuroraIMUIController` 初始化会先于 `MessageListView` 完成，如果需要调用对 `MessageListView` 的所有操作(添加消息，删除消息，更新消息)需要在 `MessageListDidLoad`事件触发后才会起作用。

  example:

  ```javascript
  AuroraIMUIController.addMessageListDidLoadListener(()=> {
    // do something ex: insert message to top
  })
  ```

- removeMessageListDidLoadListener(cb)

  取消对 `MessageListDidLoad` 事件的监听。

  example:

  ```javascript
  AuroraIMUIController.removeMessageListDidLoadListener(cb)
  ```




## MessageList

#### MessageList 事件回调

***

#### onAvatarClick 

**PropTypes.function:** ```( message ) => { }```

点击头像触发。

message 参数为：{ "message":  [message](./Models_zh.md#message))  }。

***

#### onMsgClick 

**PropTypes.function:**  ```(message) => { } ```

点击消息气泡触发。

message 参数为：{ "message":  [message](./Models_zh.md#message)  }。

***

#### onStatusViewClick

**PropTypes.function:**  ```(message) => { } ```

点击消息状态按钮触发。

message 参数为：{ "message":  [message](./Models_zh.md#message)  }。

***

#### onPullToRefresh

**PropTypes.function:** ```() => { } ```

滚动 MessageList 到顶部时，下拉触发, 案例用法: 参考 sample 中的聊天组件中的 onPullToRefresh  方法。

**Android 中，需要把该事件放到 `AndroidPtrLayout` 下，可以参考 sample/app/app.js **

***

#### onTouchMsgList

**PropTypes.function:** ```() => { } ```

点击消息列表触发。

***

#### onBeginDragMessageList (iOS only)

**PropTypes.function**

开始滑动消息列表的时候触发，用于调整布局。

***

#### MessageList 自定义样式

**在 Android 中，如果你想要自定义消息气泡，你需要将一张点九图放在 drawable 文件夹下。 [点九图介绍](https://developer.android.com/reference/android/graphics/drawable/NinePatchDrawable.html)，sample 项目的 drawable-xhdpi 文件夹下有示例。**
**在 iOS 中，如果想自定义消息气泡，需要把消息气泡图片加入到工程中，然后再 sendBubble.imageName 指定图片名字。**

***

#### sendBubble 

**PropTypes.object：**```{ imageName: string,  padding: { left: number,top: number,right: number,bottom: number}```

设置发送方的气泡样式。

***

#### receiveBubble 

**PropTypes.object：**```{ imageName: string,  padding: { left: number,top: number,right: number,bottom: number}```

设置接收方的气泡样式。

***

#### sendBubbleTextColor

**PropTypes.string:** 

设置发送消息的文本颜色，```sendBubbleTextColor="#000000"```。

***

#### receiveBubbleTextColor

**PropTypes.string**

设置接收消息的文本颜色，```sendBubbleTextColor="#000000"```。

***

#### sendBubbleTextSize

**PropTypes.number**

设置发送消息的文本大小，单位点。

***

#### receiveBubbleTextSize

**PropTypes.number**

设置接收消息的文本大小，单位点。

***

#### sendBubblePadding

**PropTypes.object：** ```{ left: number, top: number, right: number, bottom: number }```

发送消息泡泡的内边距。

***

#### receiveBubblePadding

**PropTypes.object:** ```{ left: number, top: number, right: number, bottom: number }```

接收消息泡泡的内边距。

***

#### dateTextSize

**PropTypes.number:** 

消息时间文字的尺寸大小，单位点。

***

#### dateTextColor

**PropTypes.string:**

消息时间文字的颜色, ```dateTextColor="#000000"```。

***

#### datePadding

**PropTypes.object:** =  `{ left: number, top: number, right: number, bottom: number}` 

设置时间的内边距。

Example: `datePadding={left: 5, top: 10, right: 5, bottom: 10}` 

***

#### dateBackgroundColor

**PropTypes.string**

设置时间的背景颜色。

Example: `dateBackgroundColor={"#cecece"}`

------

#### dateCornerRadius

**PropTypes.number**

设置时间的背景圆角大小。

Example: `dateCornerRadius={5}`

------

#### avatarSize

**PropTypes.object:**  ```{ width: number, height: number }```

这个对象有宽高两个属性，Example: ```avatarSize = {width: 50, height: 50}```。

***

#### avatarCornerRadius

**PropTypes.number:** 

设置头像圆角半径。

 Example: ```avatarCornerRadius = {6}```。

***

#### isShowDisplayName

**PropTypes.bool:**

是否显示昵称（包括接收方和发送方），Example: ```isShowDisplayName={ture}```。

------

#### isShowIncomingDisplayName

**PropTypes.bool:**

设置是否显示接收方昵称。

Example: `isShowIncomingDisplayName={true}`

------

#### isShowOutgoingDisplayName

**PropTypes.bool:**

设置是否显示发送方昵称。

Example: `isShowOutgoingDisplayName={false}`

------

#### displayNameTextSize

**PropTypes.number**

设置昵称文字大小。

Example: `displayNameTextSize={14}`

------

#### displayNameTextColor

**PropTypes.string**

设置昵称的文字颜色。

Example: `displayNameTextColor={"#cecece"}`

------

#### displayNamePadding

**PropTypes.object** = {left: number, top: number, right: number, bottom: number}

设置昵称内边距。

Example: `displayNamePadding={left: 5, top: 0, right: 0, bottom: 5}`

------

#### messageListBackgroundColor

**PropTypes.string:**

设置消息列表背景颜色。

Example: `messageListBackgroundColor={"#f3f3f3"}`

------

#### maxBubbleWidth

**PropTypes.number**

设置气泡的最大宽度。值为屏幕宽度的百分比。

Example: `maxBubbleWidth={0.7}`  表示设置气泡的最大宽度为屏幕宽度的 70%。

------

#### messageTextLineHeight

**PropTypes.number**

设置文字消息的行间距。

Example: `messageTextLineHeight={5}`

------

#### isAllowPullToRefresh

**PropTypes.bool:**

是否开启下拉刷新功能，Example: ```isAllowPullToRefresh={ture}```。

***



## ChatInput

### Props customizable style

------
#### customLayoutItems

**PropTypes.string:** 

自定义 ChatInput 组件和布局。

Eample: 

```
// 可以在 ChatInput 的 left/right/bottom 放置各功能 item，(不可以重复)
customLayoutItems={{
            left: ['voice'],
            right: ['send'],
            bottom: ['gallery','emoji','camera']
		}} 
		

// 如果 left/right/bottom 没有提供则不会显示，直接隐藏。
customLayoutItems={{
            left: ['voice'],
            right: ['send']
		}} 
```

#### chatInputBackgroundColor

**PropTypes.string:**

设置输入组件背景颜色。

Example:  ```chatInputBackgroundColor="#000000"```

------

#### showSelectAlbumBtn(Android Only)
**PropTypes.bool:**

设置选择相册按钮的可见性。

Example: ```showSelectAlbumBtn={true}```

------

#### showRecordVideoBtn(Android Only)
**PropTypes.bool:**

设置视频录制按钮的可见性。

Example: ```showRecordVideoBtn={true}```

------
### inputPadding

**PropTypes.object:** {left: number, top: number, right: number, bottom: number}

设置输入框内边距。

Example: `inputPadding={left:5, top:0, right:5, bottom:0}`

------

### inputTextColor

**PropTypes.string:** {"#xxxxxx"}

设置输入框文字颜色。

Example: `inputTextColor={"#808080"}`

------

### inputTextSize

**PropTypes.numbser:** {numbser}

设置输入框文字大小。

Example: `inputTextSize={14}`

------

### inputTextLineHeight

**PropTypes.number:**{numbser}

设置输入框行间距。

Example: `inputTextLineHeight={2}`

------

#### ChatInput 事件回调

***

#### onSendText

**PropTypes.function:** ```(result) => {}```

输入文字后点击发送按钮触发，result 参数为 ```{text: string}```。

***

#### onSendGalleryFiles

**PropTypes.function:** ```(result) => {}```

 选中视频或图片后点击发送按钮触发，result 参数为 ```{mediaFiles: [string]}```, 图片路径数组。

***

#### onTakePicture

**PropTypes.function:** ```(result) => {}```

 点击拍照按钮触发， result 参数为 ```{mediaPath: string}```。

***

#### onStartRecordVideo

**PropTypes.function:** ``` () => {}```

 点击录制视频按钮触发。

***

#### onFinishRecordVideo

**PropTypes.function:**``` (result) => {}```

 完成录制视频触发，result 参数为 ```{mediaPath: string, duration: number}```。

***

#### onCancelRecordVideo

**PropTypes.function:**

 取消录制视频触发。

***

#### onStartRecordVoice

**PropTypes.function:**```() => {} ```

 点击录音按钮触发。

***

#### onFinishRecordVoice

**PropTypes.function:**``` (result) => {}```

录音完成后松开手指触发，result 参数为 ```{mediaPath: string, duration: number}```。

***

#### onCancelRecordVoice

**PropTypes.function:**```() => {} ```

 手指移动到取消录音区域后，抬起手指触发。

***

#### onSwitchToMicrophoneMode

**PropTypes.function:** ```() => {} ```

 点击菜单栏麦克风按钮触发。

***

#### onSwitchToGalleryMode

**PropTypes.function:** ```() => {} ```

 点击菜单栏图片按钮触发。

***

#### onSwitchToCameraMode

**PropTypes.function:** ```() => {} ```

 点击菜单栏拍照按钮触发。

***

#### onSwitchToEmojiMode

**PropTypes.function:** ```() => {} ```

 点击菜单栏表情按钮触发。

***

#### onSizeChange

**PropTypes.function:** `({width: number, height: number}) => {}`

输入组件尺寸变更时触发 (建议使用这个方法来处理 inputView 的尺寸变化)。

***

#### onFullScreen

**PropTypes.function:** `() => {}`

当摄像机全屏的时候触发这个回调（例如：可以在摄像机全屏的时候隐藏系统状态栏）。

***

#### onRecoverScreen

**PropTypes.function:** `() => {}`

摄像机取消全屏的时候触发这个回调

***

#### onClickSelectAlbum

**PropTypes.function:** `() => {}` (Android only)

点击选择相册按钮触发(选择相册按钮默认是可见的，可以通过 [showSelectAlbumBtn](#showSelectAlbumBtn) 改变 )

***

#### onTouchEditText

**PropTypes.function:** （Android only）

点击输入框触发。