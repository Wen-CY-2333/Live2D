# Live2D 看板娘

一个基于 Live2D 技术的交互式网页看板娘项目，支持多种模型切换、拖拽移动、换装功能、自定义消息等功能。

## 项目介绍

本项目基于 [galnetwen/Live2D](https://github.com/galnetwen/Live2D) 修改而来，添加了模型切换按钮、换装功能和可拖拽看板娘功能，并调整了模型的初始位置和画布大小，使得模型能够完整显示。项目支持状态缓存，刷新页面后会记住上次选择的模型和服装。

## 快速开始

### 1. 克隆或下载项目

将项目文件下载到本地或服务器上。

### 2. 启动本地服务器

使用任意方式启动本地服务器，例如：

```bash
# 使用 Python 3
python -m http.server 8000

# 使用 Node.js
npx http-server -p 8000
```

### 3. 访问示例页面

在浏览器中访问：
```
http://localhost:8000/demo.html
```

即可看到运行中的 Live2D 看板娘。

## 功能特性

### 🎨 多模型支持
- 内置多种 Live2D 模型可供选择
- 支持一键切换不同模型
- 包含多种角色和风格（如：Miku、初音未来、Rem、B站22和33娘等）

### � 换装功能
- 部分模型支持多种服装切换
- B站22娘和33娘支持20+种不同风格的服装
- 包括节日服装、校服、夏装等多种风格

### �️ 拖拽功能
- 支持鼠标拖拽移动看板娘位置
- 拖动时自动暂停动画，提升性能
- 可拖动至页面任意位置

### 💬 交互消息
- 支持鼠标悬停和点击交互
- 可自定义各种场景下的对话内容
- 集成一言API，自动显示随机名言
- 根据时间段显示不同的问候语

### ⚙️ 灵活配置
- 可调整画布尺寸和初始位置
- 可自定义模型大小和位置
- 可修改消息显示频率

### 🔄 自动动画
- 模型自带多种动画效果
- 支持触摸和点击触发特殊动作
- 平滑的过渡效果

### 💾 状态缓存
- 自动记住当前选择的模型
- 记住每个角色的当前服装状态
- 刷新页面后状态保持不变
- 支持快捷键清除缓存（Shift+Ctrl+Alt+Enter）

## 目录结构

```
Live2D/
├── live2d/
│   ├── css/
│   │   └── live2d.css           # 样式文件
│   ├── js/
│   │   ├── jquery-ui.min.js     # jQuery UI 库（用于拖拽功能）
│   │   ├── live2d.js            # Live2D 核心库
│   │   ├── message.js           # 消息处理脚本
│   │   └── start.js             # 初始化脚本
│   ├── model/                   # 模型目录
│   │   ├── 22/                  # B站22娘模型（含20+种服装）
│   │   ├── 33/                  # B站33娘模型（含20+种服装）
│   │   ├── miku/                # 初音未来模型
│   │   ├── snow_miku/           # 雪初音模型
│   │   ├── rem/                 # 拉姆模型
│   │   ├── HK416-1-normal/      # HK416普通版
│   │   ├── HK416-2-destroy/     # HK416破坏版
│   │   ├── cat-black/           # 黑猫模型
│   │   ├── cat-white/           # 白猫模型
│   │   ├── date/                # 德丽莎模型
│   │   ├── hallo/               # 哈喽模型
│   │   ├── kobayaxi/            # 小林模型
│   │   ├── kp31/                # KP31模型
│   │   ├── platelet/            # 血小板模型
│   │   ├── rem_2/               # 拉姆第二版
│   │   ├── terisa/              # 特丽莎模型
│   │   └── wed_16/              # 婚纱模型
│   └── message.json             # 交互消息配置
├── demo.html                    # 示例页面
├── README.md                    # 项目文档
└── 138006428_p1.png             # 示例图标
```

## 配置说明

### 1. 模型配置

在 `live2d/js/start.js` 文件中可以配置可用模型列表：

```javascript
// 模型列表，包含所有可用模型
var models = [
    "/live2d/model/miku/miku.model.json",
    "/live2d/model/snow_miku/model.json",
    "/live2d/model/rem/model.json",
    "/live2d/model/22/model.default.json",
    "/live2d/model/33/model.default.json"
];
```

### 2. 换装配置

在 `live2d/js/start.js` 文件中可以配置角色换装：

```javascript
// 角色换装配置
var characterOutfits = {
    "22": [
        "/live2d/model/22/model.default.json",
        "/live2d/model/22/model.2016.xmas.1.json",
        // 更多服装...
    ],
    "33": [
        "/live2d/model/33/model.default.json",
        "/live2d/model/33/model.2016.xmas.1.json",
        // 更多服装...
    ]
};
```

### 3. 消息配置

编辑 `live2d/message.json` 文件，自定义交互消息：

```json
{
    "mouseover": [
        {
            "selector": ".title a",
            "text": ["要看看 {text} 么？"]
        }
    ],
    "click": [
        {
            "selector": "#landlord #live2d",
            "text": ["不要动手动脚的！", "真…真的是不知羞耻！"]
        }
    ]
}
```

### 4. 画布尺寸

在 HTML 文件中修改 canvas 标签的 width 和 height 属性：

```html
<canvas id="live2d" width="340" height="850" class="live2d"></canvas>
```

### 5. 初始位置

编辑 `live2d/css/live2d.css` 文件，调整看板娘初始位置：

```css
#landlord {
    position: fixed;
    left: 0;
    top: calc(50% - 280px);
}
```

### 6. 消息显示间隔

编辑 `live2d/js/message.js` 文件，修改一言API调用间隔：

```javascript
// 15秒输出一次
window.setInterval(showHitokoto, 15000);
```

## 高级功能

### 状态缓存
项目支持状态缓存功能，会自动记住：
- 当前选择的模型
- 每个角色的当前服装状态

刷新页面后状态保持不变，无需重新设置。

### 清除缓存
如需清除缓存状态，可以：
1. 使用快捷键：`Shift+Ctrl+Alt+Enter`
2. 在浏览器控制台中执行：
   ```javascript
   localStorage.removeItem('live2d_current_model_index');
   localStorage.removeItem('live2d_outfit_indices');
   location.reload();
   ```

### 时间段问候
看板娘会根据当前时间显示不同的问候语：
- 23:00-05:00：夜猫子提醒
- 05:00-07:00：早上好
- 07:00-11:00：上午好
- 11:00-14:00：午餐时间
- 14:00-17:00：午后提醒
- 17:00-19:00：傍晚问候
- 19:00-21:00：晚上好
- 21:00-23:00：晚安提醒

### 一言API
项目集成了一言API，每15秒自动显示一条随机名言。可以在 `live2d/js/message.js` 中修改间隔时间：
```javascript
// 修改为一言显示间隔（毫秒）
window.setInterval(showHitokoto, 15000);
```

## 使用方法

### 在自己的网站中使用

1. 将 `live2d` 文件夹复制到你的网站根目录

2. 在你的 HTML 页面中添加以下代码：

```html
<!-- 引入必要的 CSS -->
<link rel="stylesheet" href="/live2d/css/live2d.css" />

<!-- 引入必要的 JavaScript 库 -->
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/2.2.4/jquery.min.js"></script>
<script src="/live2d/js/jquery-ui.min.js"></script>
<script src="/live2d/js/live2d.js"></script>

<!-- 添加看板娘容器 -->
<div id="landlord">
    <div class="message"></div>
    <canvas id="live2d" width="340" height="750" class="live2d"></canvas>
    <div class="hide-button">隐藏</div>
    <div class="switch-button">切换</div>
    <div class="outfit-button">换装</div>
</div>

<!-- 引入核心功能脚本 -->
<script src="/live2d/js/message.js"></script>
<script src="/live2d/js/start.js"></script>
```

### 自定义模型

1. 将新的 Live2D 模型文件夹放入 `live2d/model/` 目录

2. 在 `live2d/js/start.js` 文件的 `models` 数组中添加新模型路径：

```javascript
var models = [
    "/live2d/model/existing-model/model.json",
    "/live2d/model/your-new-model/model.json"  // 新模型
];
```

### 调整模型大小和位置

通过修改模型目录下的 `model.json` 文件中的 `layout` 参数，调整模型在画布中的位置和大小：

```json
{
    "layout": {
        "center_x": 0.0,      // 模型中心x轴位置
        "center_y": -0.6,     // 模型中心y轴位置
        "width": 2.5          // 模型宽度
    }
}
```

## 浏览器支持

- Chrome (推荐)
- Firefox
- Safari
- Edge
- Internet Explorer 11+

## 常见问题

### 1. 模型无法加载
- 确保使用 HTTP/HTTPS 协议访问，`file://` 协议可能无法正常加载模型
- 检查模型路径是否正确
- 查看浏览器控制台是否有错误信息

### 2. 按钮不显示
- 确保已正确引入 jQuery 和 jQuery UI
- 检查 CSS 文件是否正确加载
- 尝试清除浏览器缓存

### 3. 换装功能无效
- 确保当前模型支持换装（目前仅B站22娘和33娘支持）
- 检查 `start.js` 中的 `characterOutfits` 配置是否正确
- 确认模型文件路径是否正确

### 4. 移动端不显示
- 默认在屏幕宽度小于860px时隐藏看板娘
- 可在 `live2d/css/live2d.css` 中修改媒体查询条件

### 5. 消息不显示
- 检查 `message.json` 文件是否正确加载
- 确认选择器是否与页面元素匹配
- 检查控制台是否有错误信息

## 注意事项

1. 确保你的网站使用 HTTP/HTTPS 协议访问，本地文件 `file://` 协议可能无法正常加载模型
2. 部分模型可能较大，首次加载需要一定时间
3. 建议使用现代浏览器以获得最佳体验
4. 移动端浏览器可能存在兼容性问题
5. **路径配置注意事项**：在 `live2d/js/message.js` 文件的第30行，有一个message.json的路径设置：
   ```javascript
   url: `/live2d/message.json`,
   ```
   这个路径是相对于网站根目录的绝对路径。当将live2d文件夹复制到其他项目时，需要确保项目的根目录结构和这个路径匹配，或者根据新项目的结构修改这个路径为正确的相对路径或绝对路径。

## 模型来源

Live2D 模型主要来源：
- [imuncle/live2d](https://github.com/imuncle/live2d) - live2d模型收集+展示，包含128个模型
- [oh-my-live2d/live2d-models](https://github.com/oh-my-live2d/live2d-models)

**版权须知**：所有模型均收集自互联网，版权均归原公司/个人所有。您可将资源用于学习、非营利性的网站或项目，不得用于商业使用（付费分发售卖资源、二次修改用于盈利等）。


## 原项目

原项目出自：恶魔萝莉控 [阅读原文](https://nocilol.me/archives/lab/add-dynamic-poster-girl-with-live2d-to-your-blog-02/)


---

**享受 Live2D 看板娘带来的乐趣吧！** 🎉