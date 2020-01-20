## 斗鱼骆歆直播间插件

### 目标
1. 旨在扩展增强原版功能，优化用户体验
2. 不过分影响本来的网页功能
3. 不污染页面的结构
4. 使用简单，架构轻量，功能实用，交互友好
5. 集合移动端、客户端、web端特色功能
6. 开发架构易扩展，易维护

### 使用说明
- 安装后，在礼物栏下方/鱼丸鱼翅左方会出现一个精灵球图标，点击显示功能条。
- 插件基于TamperMonkey V4.9开发，若插件有无法使用的情况，请尝试升级油猴脚本版本
- 若出现提示是否允许跨域访问的页面，一律选择**允许**即可。

### 声明
- 本插件是本人课余兴趣开发，代码质量请勿吐槽
- 代码可供互联网的同好们参考研究，**引用请注明出处**
- 制作契机源于斗鱼用户@阿拆家的MilkGirl
- 本插件归属：[斗鱼直播间5189167](https://www.douyu.com/5189167)

### 功能
#### 弹幕自动变色循环发送 
- 自动可调速发送弹幕
- 可自动改变弹幕颜色，让弹幕不再单调

#### 一键续牌
- 给所有有粉丝牌的直播间赠送一根荧光棒

#### 查看真实人数 + 已播时长
- 数据来源：播酱
- 数据将显示在原公告栏处（弹幕框上方）
- 显示观看人数，弹幕人数，送礼人数
- 显示已播时长

#### 一键签到
- 所有已关注的直播间签到
- 所有鱼吧签到
- 车队签到(由于斗鱼本身接口问题，车队签到会自动打开新的页面，签到完毕后会自动关闭这个页面，本功能参考了@lvlanxingapp的程序，在此感谢)
- pc客户端签到

#### 一键领取鱼粮
- 自动领取pc客户端旧版鱼塘宝箱
- 自动领取web端新版鱼塘气泡
- 自动领取每日/每周任务
- 有可领取的鱼粮将自动提示

#### 一键寻宝
- 一键参与鱼塘寻宝，不再需要等转圈圈了

#### 送出指定数量的礼物
- 用于送出无法指定数量的礼物
- 可用于打榜，例如一次性送出999个飞机
- 本功能未经测试（贫穷

#### 屏蔽基础广告

#### 调节弹幕大小
- 调节的是基础弹幕的大小（不算爵位弹幕等）
- 无大小限制调节

#### 自动更新
- 插件有新版本将自动提示更新

#### 获取真实直播流地址
- 可绕过斗鱼直接在本地播放器内播放
- 可直接下载(录屏)
- 该方式播放延迟极低，速度很快

#### 同屏播放
- 可在一个直播间内同时播放多个任意直播间画面（无弹幕）
- 画面可拖动可拉伸大小
- 可选择清晰度
- 可选择线路
- 点击复制直播流地址


--------------------------------------------------

## 更新内容

### 2020年1月13日22:56:47
1. 新增获取真实直播流地址
2. 新增多屏播放，可在一直播间同时观看多个直播间画面（无弹幕）
3. 重写优化真实人数显示，现在可以保留原来的公告，且资源占用更低。
4. 修复寻宝无法一次性寻完的BUG 
5. 弹幕循环发送新增发送速度区间防止系统检测，本功能需求来源greasyfork的网友
6. 弹幕循环发送新增停止时间防止忘记关闭
7. 新增今日礼物价值，显示鱼翅礼物，鼠标悬停显示背包+总礼物价值

### 2020.01.12.01
1. 重构版本发布



--------------------------------------------------

## 如何维护与编译
[项目地址](https://github.com/qianjiachun/douyuEx)
### 结构
- 本脚本将各个功能分为单独的模块，每个模块互相独立，在"编译"的时候将模块内的代码复制到main.js的相应位置即可
- 使用子模块需在父模块中注册，形式通常为`initPkg_父模块名_子模块名()`
- main.js中默认插入了一个图标，点击图标后展开功能面板。此处为底层设计好的，请慎改
- common.js为一些公共函数，是每个模块都可能会用到的。

### 维护（增加新功能）
1. 在packages内新建一个新的目录作为模块名（大驼峰）
2. 目录下新建相应的js与css文件
3. 每个模块应该有相应的入口函数（初始化函数）提供给main.js引用注册。
- 入口函数形式【initPkg_模块名】
- 每个模块向外暴露的变量需要写好注释并放在最前面
- **新增功能的icon的svg的style必须有display:block;父元素a的class要带上ex-panel__icon**
- 例如`<a class="ex-panel__icon"><svg style="display:block;"></svg></a>`或者`<a class="ex-panel__icon"><img/></a>`
- 每个模块保存的数据名字以 ExSave_ 开头 例如ExSave_BarrageLoop
4. 编写时注意不要污染其他模块或对其他模块有所影响
5. 模块中的子模块处理方式同主模块。
- **详细可参考模仿已经编写好的模块包**

### 编译
1. 将所有package的css内容依次复制到main.js的initStyle里
2. 在main.js下的initPkg函数中依次注册所有的模块，例如`initPkg_BarrageLoop();`
3. 将package下所有模块的js代码复制到main.js下
4. 全部完成后保存，复制到油猴脚本中去。
- **可以使用文件夹中自带的编译器，编译器将依据上述规则自动生成main.js**

