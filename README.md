# Live2D 看板娘

一个基于 Live2D 技术的交互式网页看板娘项目，支持多种模型切换、拖拽移动、自定义消息等功能。

## 项目介绍

本项目基于 [galnetwen/Live2D](https://github.com/galnetwen/Live2D) 修改而来，添加了模型切换按钮和可拖拽看板娘功能，并调整了模型的初始位置和画布大小，使得模型能够完整显示。

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
- 包含多种角色和风格（如：HK416、黑白猫、血小板、Rem等）

### 🖱️ 拖拽功能
- 支持鼠标拖拽移动看板娘位置
- 拖动时自动暂停动画，提升性能
- 可拖动至页面任意位置

### 💬 交互消息
- 支持鼠标悬停和点击交互
- 可自定义各种场景下的对话内容
- 集成一言API，自动显示随机名言

### ⚙️ 灵活配置
- 可调整画布尺寸和初始位置
- 可自定义模型大小和位置
- 可修改消息显示频率

### 🔄 自动动画
- 模型自带多种动画效果
- 支持触摸和点击触发特殊动作
- 平滑的过渡效果

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
│   │   ├── HK416-1-normal/      
│   │   ├── HK416-2-destroy/     
│   │   ├── cat-black/           
│   │   ├── cat-white/           
│   │   ├── date/                
│   │   ├── hallo/              
│   │   ├── kobayaxi/            
│   │   ├── kp31/               
│   │   ├── platelet/          
│   │   ├── rem_2/              
│   │   ├── terisa/              
│   │   └── wed_16/             
│   └── message.json             # 交互消息配置
├── demo.html                    # 示例页面
└── README.md                    # 项目文档
```

## 配置说明

### 1. 模型配置

在 `live2d/js/start.js` 文件中可以配置可用模型列表：

```javascript
// 模型列表，包含所有可用模型
var models = [
    "/live2d/model/hallo/model.json",
    "/live2d/model/date/model.json",
    "/live2d/model/cat-black/model.json",
    // 添加更多模型...
];
```

### 2. 消息配置

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

### 3. 画布尺寸

在 HTML 文件中修改 canvas 标签的 width 和 height 属性：

```html
<canvas id="live2d" width="340" height="850" class="live2d"></canvas>
```

### 4. 初始位置

编辑 `live2d/css/live2d.css` 文件，调整看板娘初始位置：

```css
#landlord {
    position: fixed;
    left: 0;
    top: calc(50% - 280px);
}
```

### 5. 消息显示间隔

编辑 `live2d/js/message.js` 文件，修改一言API调用间隔：

```javascript
// 15秒输出一次
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
    <canvas id="live2d" width="340" height="850" class="live2d"></canvas>
    <div class="hide-button">隐藏</div>
    <div class="switch-button">切换</div>
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

## 注意事项

1. 确保你的网站使用 HTTP/HTTPS 协议访问，本地文件 `file://` 协议可能无法正常加载模型
2. 部分模型可能较大，首次加载需要一定时间
3. 建议使用现代浏览器以获得最佳体验
4. 移动端浏览器可能存在兼容性问题
5. **路径配置注意事项**：在 `live2d/js/message.js` 文件的第38行，有一个message.json的路径设置：
   ```javascript
   url: `/live2d/message.json`,
   ```
   这个路径是相对于网站根目录的绝对路径。当将live2d文件夹复制到其他项目时，需要确保项目的根目录结构和这个路径匹配，或者根据新项目的结构修改这个路径为正确的相对路径或绝对路径。

## 模型来源

Live2D 模型来源：[oh-my-live2d/live2d-models](https://github.com/oh-my-live2d/live2d-models)


## 原项目

原项目出自：恶魔萝莉控 [阅读原文](https://nocilol.me/archives/lab/add-dynamic-poster-girl-with-live2d-to-your-blog-02/)


---

**享受 Live2D 看板娘带来的乐趣吧！** 🎉