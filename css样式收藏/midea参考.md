## 常用 midea

```css
/* 横屏 */
@media screen and (orientation:landscape){
     
}
/* 竖屏 */
@media screen and (orientation:portrait){
     
}
/* 窗口宽度<960,设计宽度=768 */
@media screen and (max-width:959px){
     
}
/* 窗口宽度<768,设计宽度=640 */
@media screen and (max-width:767px){
     
}
/* 窗口宽度<640,设计宽度=480 */
@media screen and (max-width:639px){
     
}
/* 窗口宽度<480,设计宽度=320 */
@media screen and (max-width:479px){
     
}
/* 设备像素比为2 */
/* 常用于1px边框，还应规定 3dppx 的情况 */
@media (min-resolution: 2dppx) {

}
/* windows UI 贴靠 */
@media screen and (-ms-view-state:snapped){
     
}
/* 打印 */
@media print{
     
}
```

    orientation 方向

    resolution 分辨率

    dpr === dppx

---

## 强制横屏

> 编写时以横屏布局即可

```css
.landscape-container {
  position: absolute;
  overflow: hidden;
}

// 竖屏
@media screen and (orientation: portrait) {
  .landscape-container {
    width: 100vh;
    height: 100vw;
    top: calc((100vh - 100vw) / 2);
    left: calc((100vw - 100vh) / 2);
    transform: rotate(90deg);
    transform-origin: 50% 50%;
  }
}

// 横屏
@media screen and (orientation: landscape) {
  .landscape-container {
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    transform: none;
    transform-origin: 50% 50%;
  }
}
```