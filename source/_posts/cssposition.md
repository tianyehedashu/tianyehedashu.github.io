---
title: cssposition
date: 2018-07-16 14:47:42
tags:
---
* 绝对定位 相对定位 固定定位 https://blog.csdn.net/luyu13141314/article/details/53517313
* 浮动定位 https://www.cnblogs.com/zfquan/p/7793945.html
* CSS的负边距
* 双飞翼和圣杯布局 https://www.jianshu.com/p/f9bcddb0e8b4
* overflow:hidden
* 对于双飞翼布局中的margin-left:-100%的理解 https://blog.csdn.net/Night_Nine_Leaves/article/details/79660762 (双飞翼布局)
 https://blog.csdn.net/Night_Nine_Leaves/article/details/79660762
 * BFC http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html
 * css(float浮动和clear清除) https://www.cnblogs.com/zfquan/p/7793945.html


<div class="container2">
<div class="test4">
    <div class="main1">
    main
    </div>
    <div class="left1">
    left
    </div>
    <div class="right1">
    right
    </div>
</div>
</div>

<style type="text/css">
    .container2 {
      width:600;
      height:1200;
      background-color:teal;
    }
    .test4{
      margin:0;
      padding:0;
    }
    .main1, .left1,.right1 {
      float:left;
      padding:0;
      margin:0;
    }
    .main1 {
        height: 100px;
        width: 100%;
        background-color: blue;
    }
    .left1 {
        height: 400px;
        width: 100px;
        background-color: red;
        margin-left:-100%;
    }
    .right1 {
        height: 200px;
        width: 150px;
        margin-left：-150px;
        background-color: black;
    }
</style>
