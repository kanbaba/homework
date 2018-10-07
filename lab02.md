# **以Construct 2制作平台游戏的新手指南**  

### 创建新的项目  
启动Construct 2点击File按钮，选择New选项，创建新的项目。  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzf3iz19jj305804iwev.jpg)  

### 设置背景  
再制作一个游戏的最开始，我们需要选定一个图片，把它固定不动，铺满整个布局，作为这个游戏背景。  
首先我们选定这张图片作为我们整个游戏的背景：  
![背景图](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzf6g1c76j30740740zk.jpg)  
然后双击界面中的任何地方，可以出现一个“Insert New Object”的对话框。  
从对话框中的“General”选项中选择“Tiled Background”的选项，就可以插入背景图片了。  
之后我们可以找到图片下载的位置，来插入这张图片：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfbyryh9j306c02sglq.jpg)  
然后我们可以对图片进行放缩来使图片铺满整个空白布局。  

### 锁定背景图层，添加活动图层  
接下来我们需要对图层进行操作，进一步完善我们的游戏。  
  首先我们找到“Layers”选项，找到其中的第0层，对其重命名，命名为 “背景层”，并且点击那个小锁图标，锁定背景层。  
  之后我们添加一个图层，命名为“活动层”，并选中活动层，以便我们在接下来的操作过程中对活动层进行加工。  
  完成该步骤后的结果应该是这个样子的：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfde7xnxj306x06rdfq.jpg)  

### 插入对象  
接下来我们需要在我们的活动层中插入我们的新对象。
  
  第一部分是鼠标和电脑。  
  同样双击空白部分，选择“Mouse”和“Keyboard”选项，这样我们就可以用我们的鼠标和键盘来对物体进行控制。  
  第二部分是各种游戏对象。  
  我们需要插入一个玩家的形象。如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfowxyv1j303002vdfw.jpg)  
  然后插入怪物的形象。如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfr7yt0qj304102s74h.jpg)  
  还需要插入子弹形象和爆炸形象。如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfs374fmj300p00g0jw.jpg)  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfsbydilj303a02tmx3.jpg)  

### 修改精灵属性  
我们把活动层中的各种游戏对象统称为精灵。接下来，我们需要逐步去修改它们的属性，以至于获得更好的游戏体验。  
  第一步需要修改名字。  
  我们分别点击每个游戏对象，找到它们的“Name”属性栏，进行修改。分别改为“玩家”，“怪物”，“子弹”，“爆炸”。以便于我们区分和进行下面的步骤。  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzfxxl4unj306y02jweb.jpg)  
  第二步需要添加行为。  
  我们需要让每个游戏对象都拥有自己的行动方式。  
    
    我们要让玩家可以自由移动，同时不能运动到布局外面，并且使屏幕随着玩家的移动而移动。  
    所以打开玩家属性栏中的行为属性，也就是“Behaviors”选项。  
    之后我们为他添加“8 Direction”，“ScrollTo”，“BoundToLayout”三种行为。  
    ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzg728b4dj30e006x3zw.jpg)   

    完成图如下：  
    ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzg7j1bplj308905aq38.jpg)  
    
    我们继续为子弹添加“Bullet movement”和“Destroy outside layout”两个行为。  
    为怪物添加“Bullet movement”这个行为，使怪物运动起来。  
    给爆炸添加“Fade”这个行为，让它在出现后消失，使我们获得更好的游戏体验。  
    
  第三步我们需要做一些细微的调整。  
  我们需要调整玩家，子弹，怪物的移动速度。我们在行为属性中找到带有“Speed”的选项，对其进行修改。  
  把玩家速度调为200，子弹速度调为600，怪物速度调为80。  
  我们在爆炸的行为属性中，选中“Fade out time”选项，把淡出时间调整为0.5s。  

  第四步我们增加怪物数量，增大游戏难度。  
  按住“ctrl”键，拖动怪物图标，就可以增加新的怪物了！  

### 添加事件  
事件由条件组成，测试是否满足某些条件。  
如果满足所有这些条件，则事件的所有操作都会运行。  
运行后，任何子事件也会运行，然后可以测试更多条件，然后运行更多操作，然后运行更多子事件。  
在这里我们以一个事件为例演示如何添加事件。  
填加事件的结构为：  
执行条件的对象--条件--执行活动1的对象--活动1（执行活动2的对象--活动2···）  
  我们要演示添加玩家在任何都要面向鼠标箭头的事件。  
  记住每次绘制屏幕时都会运行刻度线，因此如果我们让每个刻度线都让玩家面向鼠标，它们将始终面向鼠标。
  执行该条件的对象是系统，因此我们首先选择对象，如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzgwvk127j30bo0ajjrv.jpg)  
  之后我们可以选择条件，如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzgxukyhtj30cu0a7dg4.jpg)  
  然后我们添加子事件的对象，和它执行的活动，如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzgzc76usj30bo09y0t5.jpg)  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzgznp3guj30cy09yjro.jpg)  
  我们的活动是确定玩家的朝向，所以我们接下来需要在活动中添加玩家朝向的坐标。  
  由于我们是让玩家面向鼠标，我们可以直接添加鼠标的x，y坐标，如图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzh4h2l4sj30e007gq2r.jpg)  
  完成样图如下：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzh51x9aqj30f301ba9v.jpg)  
  
之后我们以同样方法还需要添加以下的几个事件：  
1.当玩家点击时，他们应该射击子弹。  
条件：鼠标--单击--左键单击  
操作：播放器--生成另一个对象--对于对象，选择Bullet对象。对于Layer，放1（“Main”层是第1层--记住Construct 2从零开始计数）。将图像点保留为0。  
  ps：我们需要让子弹从枪的末端射出，所以需要如下操作：  
  第一步，我们选定玩家对象，然后选择如下功能：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzhg24mp6j30g90d7js2.jpg)  
  第二步，我们要添加子弹射出点：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzhhemj4zj306607ea9z.jpg)  
  第三步，我们要定位子弹射出点在枪的末端：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzhiykidfj304o03tmxa.jpg)  
2.让子弹杀死怪物。  
条件：子弹--与另一个物体碰撞--选择怪物。  
动作：怪物--摧毁  
动作：子弹--生成另一个对象--爆炸，第1层  
动作：子弹--摧毁  
  ps：为了让爆炸更美观，我们把它的Blend mode 属性设置为Additive  
3.让怪物随机移动。  
条件：系统--开始布局  
动作：怪物--设置角度--随机（360）  
4.让怪物移动到布局外时，向布局内部移动。  
条件：怪物--外部布局  
动作：怪物--设置角度朝向位置--对于X，Player.X；对于Y，Player.Y  
5.为怪物添加血量。  
  ps：这需要添加新的属性。具体操作如下图：  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzhrgdj4lj30fa05h3zl.jpg)  
  ![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzhrwf69qj307r051jrr.jpg)  
6.修改怪物被摧毁的条件。  
找到事件：Bullet - 与Monster碰撞。请注意，我们有一个“摧毁怪物”动作。让我们用“从健康中减去1”来代替它。右键单击“destroy monster”操作，然后单击“ replace”。  
7.让怪物被摧毁。  
条件：怪物--比较实例变量--健康<=0  
动作：怪物--生成另一个对象--爆炸，第1层  
动作：怪物--摧毁  

### 添加得分系统  
第一步，右键单击事件表底部的空间，然后选择“Add global variable”。  
第二步，输入Score作为名称。其他字段默认值为OK，它将使其成为从0开始的数字。  
第三步，添加一个新的事件，使Score增加。  
在第7步的事件中增加得分事件：单击Add action，然后选择System--Add to--Score，value 1。  
效果如图：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzi2u0kykj30ea02j746.jpg)  

### 显示系统得分  
第一步，增添新的图层栏，命名为HUD.  
第二步，将Parallax属性设置为0,0（在X和Y轴上均为零）。  
第三步，双击空格以插入另一个对象。这次选择Text对象。将其放在布局的左上角。很难看出它是否是黑色的，所以在属性栏中，使其变为粗体，斜体，黄色，并选择稍大的字体大小。将其大小调整到足以容纳合理数量的文本。  
第四步，切换回活动表。让我们用播放器的分数更新文本。在我们之前添加的Every tick事件中，添加操作Text--Set text。  
第五步，文本输入---“Score：”&Score  

### 增添最后的事件  
1.创造怪物。  
条件：系统--每X秒--3  
动作：系统--创建对象--怪物，第1层，1400（对于X）；随机（1024）（对于Y）  
2.让怪物可以杀死玩家。  
条件：怪物--与另一个物体碰撞--玩家  
动作：玩家--摧毁  
  
附上一张所有事件的图片，方便对照错误的地方：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzib7rlqyj30yn0jg0uj.jpg)  
  
### 运行和保存  
运行你的游戏，通过“Run layout”选项。  
如果满意，请保存游戏，并为它起一个好听的名字结束你的游戏制作。  
  

附一张成品效果图：  
![](https://ws1.sinaimg.cn/large/007kRF1Jgy1fvzjcskveag30o90e77wz.jpg)