# Grid布局

## 传统的flex布局

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .layout {
        width: 1400px;
        min-height: 500px;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        margin: 0 auto;
      }
      .layout .box {
        width: 300px;
        height: 200px;
        background-color: #bababa;
        border: 1px solid #000;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 40px;
      }
    </style>
  </head>
  <body>
    <div class="layout">
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
    </div>
  </body>
</html>

```

![image-20250312163218423](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250312163218423.png)

布局如下，会发现最下面的方块不会紧挨着第一个方块排列。

## grid布局

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .layout {
        width: 90%;
        min-height: 500px;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        gap: 30px;
        flex-wrap: wrap;
        margin: 0 auto;
      }
      .layout .box {
        height: 200px;
        background-color: #bababa;
        border: 1px solid #000;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 40px;
      }
    </style>
  </head>
  <body>
    <div class="layout">
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
    </div>
  </body>
</html>

```

使用方式如下：

```
display: grid;  /* 使用网格布局 */
grid-template-columns: repeat(5, 1fr);  /* 布局方式，repeat的第一个参数表示分为几列，第二个参数是每一列的宽度，1fr就是给定的网格宽度 */
gap: 30px;  /* 每个网格的间距 */
```

![image-20250312164313106](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250312164313106.png)

### 响应式布局

```
grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
/* auto-fill表示自动填充，minmax中第一个参数是指网格的最小宽度，第二个参数是最大宽度*/
```

### 跨网格布局

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .layout {
        width: 90%;
        min-height: 500px;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        gap: 30px;
        flex-wrap: wrap;
        margin: 0 auto;
      }
      .layout .box {
        height: 200px;
        background-color: #bababa;
        border: 1px solid #000;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 40px;
      }

      .layout .box1 {
        grid-column: 1/3;
        grid-row: 1/3;

        background-color: #bababa;
        border: 1px solid #000;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 40px;
      }
    </style>
  </head>
  <body>
    <div class="layout">
      <div class="box1">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
      <div class="box">方块</div>
    </div>
  </body>
</html>

```

其中 ` grid-column: 1/3;grid-row: 1/3;`表示该网格列跨越两格，行跨越两格。`1/3` 表示从第一列的开始线到第三列的开始线之间的区域。

![image-20250312164836850](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250312164836850.png)