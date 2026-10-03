# AI 隔空雾镜 · Fog Mirror

### ▶ **[点这里打开交互网站](https://luoluoluo312.github.io/ai-fog-mirror/)**

浏览器里的体感交互页：画面被一层起雾的玻璃镜片遮住，用大拇指和食指捏合模拟握笔，
在空中移动即可擦开雾气。

## 使用

1. 打开上面的链接（手机 / 平板 / 电脑都可以）
2. 浏览器询问摄像头权限时点「允许」
3. 把手放进画面，**捏合拇指与食指**，移动即可擦雾
4. 底部滑杆实时调整笔刷粗细，「重置雾气」重新起雾

> 必须通过 `https` 或 `localhost` 打开，浏览器才允许调用摄像头。

## 实现

单文件 `index.html`，无需构建、无需安装依赖：

- 手部关键点：[MediaPipe Hands](https://cdn.jsdelivr.net/npm/@mediapipe/hands/hands.js)（CDN 引入）
- 摄像头采集：[MediaPipe Camera Utils](https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/camera_utils.js)
- 画面结构：失焦视频 → 镜片反光层 → 可擦除的雾气 Canvas
- 擦除：`globalCompositeOperation = 'destination-out'`，用预渲染笔刷印章沿插值路径盖章
- 捏合判定：Landmark 4（拇指尖）与 8（食指尖）的归一化欧氏距离 + 滞回阈值
- 性能：手势识别 30fps、渲染 60fps，两者解耦

## 本地运行

```bash
python -m http.server 8000
```

然后访问 <http://localhost:8000>
