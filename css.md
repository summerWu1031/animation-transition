## 浏览器渲染原理
渲染步骤包括样式、布局、绘制，在某些情况下还包括合成。在解析步骤中创建的CSSOM树和DOM树组合成一个Render树，然后用于计算每个可见元素的布局，然后将其绘制到屏幕上。在某些情况下，可以将内容提升到它们自己的层并进行合成。
Style（样式）→Layout（布局）→Paint（绘制）→Compositing（合成）
![](1.png)
![](2.png)
每个标签的改动走的流程都不一样，可以通过下面这个网址查询到不同标签在不同浏览器上面的渲染流程
<br>
https://csstriggers.com/

<br>

## CSS 动画的两种做法（transition 和 animation）

1. transition
   
   transition: 属性 动画过程的秒数 变化的模式 几秒后开始动画
   
   *注意：不是所有的属性都能过渡
   display:none => block 不能过渡

   ~~~html
    transition: width 2s ease 3s;
   ~~~

    ![](3.png)
<br>

2. animation
   ![](4.png)

   ~~~html
   .heart{
            
            animation: heart .5s infinite alternate;
        }
        
        @keyframes heart{
            0%{
                transform: scale(1);
            }
            100%{
                transform: scale(1.2);
            }
    ~~~
<br>

## css常见的三种布局方式
![](5.png)
   
* ## float
  ~~~html
  <style>
        *{
            padding: 0;
            margin:0;
            box-sizing: border-box;
        }

        ul,ol,li{
            list-style: none;
        }

        .clearfix::after{
            content: '';
            display: block;
            clear: both;
        }

        .nav{
            border:1px solid red;
            display: inline-block;
            float: right;
            margin-right: 20px;
        }

        .nav>li{
            border: 1px solid black;
            padding: 4px 0.5em;
            float: left;
            line-height: 22px;
        }

        .logo>img{
            height: 30px;
            background-color: #555;
            vertical-align: top;
        }   

        .logo{
            border: 1px solid red;
            float: left;
            margin-left: 10px;
        } 

        header{
            border: 1px solid green;
            background-color: #555555;
            color: white;
            margin-bottom: 10px;
        }  

        .content{
            outline: 5px solid red;
            width: 800px;
            height: 300px;
            margin-left: auto;
            margin-right: auto;
        }  

        aside{
            width: 200px;
            outline: 1px solid black;
            height: 300px;
            float: left;
            background-color: #555;
        }

        main{
            width: 500px;
            outline: 1px solid green;
            height: 300px;
            float: left;
            background-color: #999;
        }

        .ad{
            width: 100px;
            outline: 1px solid pink;
            height: 300px;
            float: left;
            background-color: #333;
        }

        .image-list{
            /* border: 1px solid black; */
            width: 800px;
            margin-top: 20px;
            margin-left: auto;
            margin-right: auto;
        }

        .image-list>.x>div{
            width: 191px;
            height: 191px;
            /* border:1px solid red; */
            margin-right: 12px;
            float: left;
            background-color: #999999;
            margin-bottom: 10px;
        }

        .x{
            margin-right: -12px;
            /* border: 1px solid green; */
        }
    </style>

    <header class="clearfix">
        <ul class="nav clearfix">
            <li>首页</li>
            <li>课程</li>
            <li>优惠</li>
            <li>关于</li>
        </ul>

        <div class="logo">
            <img src="1.png" alt="">
        </div>
    </header>
    <div class="content clearfix">
        <aside></aside>
        <main></main>
        <div class="ad"></div>
    </div>
    <div class="image-list clearfix">
        <div class="x clearfix">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
        
    </div>
    ~~~

    ### 注意事项
    * 在浮动元素的父元素上一定要加.clearfix
        ~~~html
          .clearfix::after{
            content: '';
            display: block;
            clear: both;
        }
        ~~~

    * float布局不能用于手机上，只适合于网页布局
  

* ## flex
  ~~~html
  <style>
        *{
            padding: 0;
            margin:0;
            box-sizing: border-box;
        }

        ul,ol,li{
            list-style: none;
        }
        img{
            max-width: 100%;
        } 
        .logo>img{
            height: 20px;
            /* background-color: #555; */
            vertical-align: top;
        }   

        .logo{
            border: 1px solid red;
            margin-left: 10px;
            display: flex;
            
        } 

        .nav{
            display: flex;
            border: 1px solid black;
        
        }

        .nav>li{
            border: 1px solid red;
            padding: 4px 0.5em;
            font-size: 12px;
        }

        header{
            border: 1px solid red;
            display: flex;
            justify-content: space-between;
            background-color: #999;
            color: white;
            align-items: center;
           
        }

        .content{
            border: 1px solid back;
            max-width: 100%;
            margin-left: auto;
            margin-right: auto;
            display: flex;
            margin-bottom: 10px;
        }
        .content>aside{
            background-color: #333333;
            width: 100px;
            
        }
        .content>main{
            background-color: #999;
            height: 100px;
            flex-grow: 1;
        }
        .content>.ad{
            background-color: #666;
            width: 50px;
            
        }
        .imageList{
            outline: 1px solid red;
            
            min-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }
        .inner{
            display: flex;
            flex-wrap: wrap;
            margin-right: -12px;
        }
        .imageList>.inner>.image{
            width: 191px;
            height: 191px;
            border: 1px solid black;
            margin-right: 12px;
            margin-bottom: 10px;
        }
    </style>


    
        <div class="logo">
          <img src="1.png" alt="">
        </div>
        <ul class="nav">
            <li>首页</li>
            <li>课程</li>
            <li>优惠</li>
            <li>关于</li>
        </ul>
    
    <div class="content">
        <aside></aside>
        <main></main>
        <div class="ad"></div>
    </div>

    <div class="imageList">
        <div class="inner">
            <div class="image"></div>
            <div class="image"></div>
            <div class="image"></div>
            <div class="image"></div>
            <div class="image"></div>
            <div class="image"></div>
            <div class="image"></div>
        </div>
        
    </div>
    ~~~

    ### 常用的属性
    * display:flex;
    * flex-direction:row/row-reverse/column/column-reverse
    * flex-raw:nowrap/wrap
    * justify-content:center/space-between/space-around
    * align-items:center


<br>
声明：所有图片均来自饥人谷