# 任务三：零基础JavaScript编码（三）
[demo](https://zhouxiaoyu1994.github.io/2017-IFEbinbin/task-3/index.html)
## 任务目的
- 在上一任务基础上继续JavaScript的体验
- 接触一下JavaScript中的高级选择器
- 学习JavaScript中的数组对象遍历、读写、排序等操作
- 学习简单的字符串处理操作
## 任务描述
- 参考以下示例代码，读取页面上已有的source列表，从中提取出城市以及对应的空气质量
- 将数据按照某种顺序排序后，在resort列表中按照顺序显示出来

```
<!DOCTYPE>
<html>
  <head>
    <meta charset="utf-8">
    <title>IFE JavaScript Task 01</title>
  </head>
<body>

  <ul id="source">
    <li>北京空气质量：<b>90</b></li>
    <li>上海空气质量：<b>70</b></li>
    <li>天津空气质量：<b>80</b></li>
    <li>广州空气质量：<b>50</b></li>
    <li>深圳空气质量：<b>40</b></li>
    <li>福州空气质量：<b>32</b></li>
    <li>成都空气质量：<b>90</b></li>
  </ul>

  <ul id="resort">
    <!-- 
    <li>第一名：北京空气质量：<b>90</b></li>
    <li>第二名：北京空气质量：<b>90</b></li>
    <li>第三名：北京空气质量：<b>90</b></li>
     -->

  </ul>

  <button id="sort-btn">排序</button>

<script type="text/javascript">

/**
 * getData方法
 * 读取id为source的列表，获取其中城市名字及城市对应的空气质量
 * 返回一个数组，格式见函数中示例
 */
function getData() {
  /*
  coding here
  */

  /*
  data = [
    ["北京", 90],
    ["北京", 90]
    ……
  ]
  */

  return data;

}

/**
 * sortAqiData
 * 按空气质量对data进行从小到大的排序
 * 返回一个排序后的数组
 */
function sortAqiData(data) {

}

/**
 * render
 * 将排好序的城市及空气质量指数，输出显示到id位resort的列表中
 * 格式见ul中的注释的部分
 */
function render(data) {

}

function btnHandle() {
  var aqiData = getData();
  aqiData = sortAqiData(aqiData);
  render(aqiData);
}

function init() {

  // 在这下面给sort-btn绑定一个点击事件，点击时触发btnHandle函数

}

init();

</script>
</body>
</html>
```

## 任务注意事项
- 实现简单功能的同时，请仔细学习JavaScript基本语法、事件、DOM相关的知识
- 请注意代码风格的整齐、优雅
- 代码中含有必要的注释
- 建议不使用任何第三方库、框架
- 示例代码仅为示例，可以直接使用，也可以完全自己重写
## 解题思路
- 按照任务描述来看，可知其主要思路为：提取 ——— 排序 ——— 打印。下面对思路的三个阶段依次进行分析。
- 提取
 - 首先获取source列表，需要注意的是，这里我们要获取的是source列表中的li标签，而不是ul标签。所以不能直接用 getElementById() 方法，可以通过 nodeObject.children 语法来帮助获取元素的子节点。
  `var city = document.getElementById('source').children;`
  另外还可以使用HTML5新增的选择器 querySelectorAll：根据选择器规则返回所有符合要求的元素，使用方便（可以使用css选择符来查找节点）、兼容性好（IE 8+、FireFox 3.5+、Safari 3.2+、Chrome 4.0+、Oprea 10.1+ ），缺点是速率远远没有前者高。
  `var city = document.querySelectorAll('#source>li');`
 - 创建新数组，用于存放提取的数据。
 - 创建for循环，用于对全部的li标签进行提取。
 - 获取li标签中的文本，获取节点及其后代节点文本的语法有 textContent（可以获取所有元素的内容，包括<script>和<style>） 和 innerText（可以感知样式，不会返隐隐藏元素的文本内容），因为要忽视li标签中的css样式，所以这里选择 innerText 方法。
 - 提取关键字，并放入数组中。这里使用 substr(start,length) 方法，第一个参数是要抽取的子串的起始下标，负数则从末尾算起。第二个参数为抽取的子串的长度。然后再用 push() 方法，依次放入数组。
  `var node = [text.substr(0, 2), text.substr(-2, 2)];`
- 排序
 使用sort()方法进行排序。
 `data.sort(function(a,b){ return a[1] - b[1];});`
- 打印
 - 首先获取resort列表。
 - 创建for循环。
 - 创建新的li标签。
  - 使用createElement()方法创建分别创建li标签和b标签。
   `var oLi = document.createElement('li');`
   `var oB = document.createElement('b');`
  - 按照任务描述，创建一个字符串变量。
   `var arr = ["一","二","三","四","五","六","七"];`
   `var liText = '第' + arr[i] + '名：' + data[i][0] +"，" + '空气质量：';`
  - 用appendChild()方法，将字符串变量，赋值给li标签。

   ```
   oLi.innerText = liText;
   oB.innerText = data[i][1];
   oLi.appendChild(oB);
   resort.appendChild(oLi);
   ```
## 完整代码

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>任务三：零基础JavaScript编码（三）</title>
</head>
<body>
<ul id="source">
    <li>北京空气质量：<b>90</b></li>
    <li>上海空气质量：<b>70</b></li>
    <li>天津空气质量：<b>80</b></li>
    <li>广州空气质量：<b>50</b></li>
    <li>深圳空气质量：<b>40</b></li>
    <li>福州空气质量：<b>32</b></li>
    <li>成都空气质量：<b>90</b></li>
</ul>
<ul id="resort">
    <!--
    <li>第一名：北京空气质量：<b>90</b></li>
    <li>第二名：北京空气质量：<b>90</b></li>
    <li>第三名：北京空气质量：<b>90</b></li>
     -->

</ul>
<button id="sort-btn">排序</button>
<script type="text/javascript">
    /**
     * getData方法
     * 读取id为source的列表，获取其中城市名字及城市对应的空气质量
     * 返回一个数组，格式见函数中示例
     */
    function getData() {
        /*
         coding here
         */
        var city = document.querySelectorAll('#source>li');
        var data = [];
        //提取城市名和空气质量的关键字
        for(var i = 0; i < city.length; i++) {
            var text = city[i].innerText;
            var node = [text.substr(0, 2), text.substr(-2, 2)];
            data.push(node);
        }
        return data;
        /*
         data = [
         ["北京", 90],
         ["北京", 90]
         ……
         ]
         */
    }
    /**
     * sortAqiData
     * 按空气质量对data进行从小到大的排序
     * 返回一个排序后的数组
     */
    function sortAqiData(data) {
        data.sort(function(a, b) {
            return a[1] - b[1];
        });
        return data;
    }
    /**
     * render
     * 将排好序的城市及空气质量指数，输出显示到id位resort的列表中
     * 格式见ul中的注释的部分
     */
    function render(data) {
        var arr = ["一","二","三","四","五","六","七"];
        var resort = document.getElementById('resort');
        for(var i = 0; i < data.length; i++) {
            var liText = '第' + arr[i] + '名：' + data[i][0] +"，" + '空气质量：';
            var oLi = document.createElement('li');
            var oB = document.createElement('b');
            oLi.innerText = liText;
            oB.innerText = data[i][1];
            oLi.appendChild(oB);
            resort.appendChild(oLi);
        }
    }
    function btnHandle() {
        var aqiData = getData();
        aqiData = sortAqiData(aqiData);
        render(aqiData);
    }
    function init() {
        // 在这下面给sort-btn绑定一个点击事件，点击时触发btnHandle函数
        var btn = document.getElementById('sort-btn');
        btn.onclick = function() {
            btnHandle();
        };
    }
    init();
</script>
</body>
</html>
```

## 参考资料
[querySelectorAll 方法相比 getElementsBy 系列方法有什么区别？](https://www.zhihu.com/question/24702250)
[HTML5的JavaScript选择器介绍](http://www.cnblogs.com/iyitong/p/4229355.html)
[Javascript获取子节点](http://www.itxueyuan.org/view/6349.html)
[innerText，textContent和innerHTML](http://openwares.net/js/innertext_textcontent_innerhtml.html)


























