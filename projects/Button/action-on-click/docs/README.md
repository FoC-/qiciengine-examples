# 按钮的事件

* 实例演示按钮的事件：点击、按下、松开、鼠标进入和移出。效果图如下：<br>
![ActionOnClick](images\UI.gif)

# UI

* 在新建场景中创建一个UIImage，作为background，设置RectTransform中x、y轴方向上的stretch模式。
* 在根节点下创建一个Button，用来表现按钮的点击、按下、松开、鼠标进入和移出的效果。
* 创建脚本UI.js，负责按钮的事件响应。脚本挂在button节点上，将background设置到Background的属性上。如下图：<br>
![script](images\script.png)<br>
代码如下：<br>

```javascript
var UI = qc.defineBehaviour('qc.demo.UI', qc.Behaviour, function() {
}, {
    background: qc.Serializer.NODE
});

UI.prototype.awake = function() {
    var self = this;
    this.addListener(self.gameObject.onEnter, function() {
        self._isEnter = true;
        self.gameObject.frame = 'button_sprite_sheet_03.png';
    });
    this.addListener(self.gameObject.onExit, function() {
        self._isEnter = false;
        self.gameObject.frame = 'button_sprite_sheet_02.png';
    });
};

UI.prototype.onDown = function() {
    this.gameObject.frame = 'button_sprite_sheet_01.png';
};

UI.prototype.onUp = function() {
    if (this._isEnter) {
        this.gameObject.frame = 'button_sprite_sheet_03.png';
    }  
    else {
        this.gameObject.frame = 'button_sprite_sheet_02.png';
    }
};

UI.prototype.onClick = function() {
    this.background.visible = !this.background.visible;
};

```