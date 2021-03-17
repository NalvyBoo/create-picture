## Canvas 图片绘制组件
该组件提供了 Canvas 的 **图片绘制** 与 **文本绘制** 功能，使用同步的语法完成异步绘制，简化原生 canvas 绘制语法。

### 安装
使用 [npm](https://www.npmjs.com/package/create-picture) 安装：
```git
npm i create-picture --save
```

导入 `create-picture`
```javascript
import CreatePicture from 'create-picture';
```

### 使用

基础示例
```javascript
// 初始化
const cp = new CreatePicture();

// 绘制图片，参数1为图片路径，其他参数与 CanvasRenderingContext2D.drawImage() 参数相同
cp.drawImage(require('../assets/save_bg.jpg'),0,0);

// 绘制文本
cp.drawText({content:'文本'});

// 获取合成图
cp.getPicture().then((picture)=>{
    // picture 为合成的 base 64
});
```

## 方法

- `new CreatePicture();` - 初始化，可接受一个对象参数
- `drawImage()` - 绘制图片，第一个参数为图片路径，其他参数与 [CanvasRenderingContext2D.drawImage()](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/drawImage) 参数相同
- `drawRectImage()` - 绘制重复排列的图片
- `drawCirclePicture()` - 绘制头像等圆形图片，与 `drawImage` 参数相同
- `drawText()` - 绘制文本，返回文字宽度（可选）
- `getPicture().then((picture)=>{});` - 最终合成的图片

## 参数

### new CreatePicture() 可选参数

- `width` - 画布宽度，默认值 `750`
- `height` - 画布高度，默认值 `1448`

### drawImage() 可选参数

- 第一个参数为图片路径
- 其他参数与 [CanvasRenderingContext2D.drawImage()](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/drawImage) 参数相同

### drawRectImage() 参数

- 第一个参数为图片路径
- 第二、三参数为平铺文件的宽高
- 第四、五参数为要平铺的区域

### drawCirclePicture() 可选参数

- 第一个参数为图片路径
- 其他参数与 [CanvasRenderingContext2D.drawImage()](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/drawImage) 参数相同
- 如需指定图片宽高，可以使用 `9` 个参数的方式，传入图片宽高未知可以传入 `auto` 自动获取
- 示例
```javascript
cp.drawCirclePicture(headimgurl,0,0,'auto','auto',50,50,80,80);
```

### drawText() 可选参数

- `fontStyle` - 文字样式，默认 `normal`
- `fontVariant` - 文字变体，默认 `normal`
- `fontWeight` - 文字宽度，默认 `normal`
- `fontSize` - 文字宽度，默认 `30`
- `lineHeight` - 文字行高，默认 `normal`
- `fontFamily` - 字体，默认 `Arial`
- `left` - 左对齐，默认 `0`
- `top` - 上对齐，默认 `300`
- `maxWidth` - 文字最大宽度，默认 `undefined`
- `content` - 文本内容
- `textAlign` - 对齐方式，默认 `start`
- `textBaseline` - 文本基线，默认 `alphabetic`
- `direction` - 文字方向，默认 `inherit`
- `color` - 文字颜色，默认 `#000000`
- `rotation` - 文字旋转角度，默认 `0`
- `width` - 文字段落的宽度，超出自动换行，默认 `undefined`

### getPicture() 可选参数

- 与 [HTMLCanvasElement.toDataURL()](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement/toDataURL) 参数保持一致
- 默认为 `'image/png'`
- 示例
```javascript
// 图片格式：jpg ，图片质量：0.6
getPicture('image/jpeg',0.6).then((picture)=>{})

// 图片格式：webp ，图片质量：0.8
getPicture('image/webp',0.8).then((picture)=>{})
```

## 示例

-  示例代码
 ```javascript
import CreatePicture from 'create-picture';

// 初始化
const cp:CreatePicture = new CreatePicture();

// 初始化（传参）
const cp:CreatePicture = new CreatePicture({width:750,height:1448});

// 绘制图片，参数1为图片路径，其他参数与 CanvasRenderingContext2D.drawImage() 参数相同
cp.drawImage(require('../assets/save_bg.jpg'),0,0);

// 绘制文本
cp.drawText({content:'文本'});

// 绘制文本，获取文字宽度
const textWidth = cp.drawText({
    content:'文本',
    fontSize: 30,
    top: 300,
    color: '#ffffff',
});

// 获取合成图
cp.getPicture().then((picture)=>{
    // picture 为合成的 base 64
});
 ```
