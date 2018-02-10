# d3 - 学习笔记

> 又开一个试水坑啦~~

### 选择器

和jq的选择器一样，select()和selectAll()

- select是取匹配到的第一个元素
- selectAll取得匹配到的所以元素

```javascript
//获取文档中body元素中的所有p元素
var pNodes = d3.select('body').selectAll('p');
```

### 绑定数据到dom上

两个方法绑定数据到select到的dom集合

- data() 是绑定个数组
- datum() 是绑定一个数据

```javascript
//上文已经获取了pNodes元素集 现在给它们绑定数据
var data = [{ name: '1', age: 11 },{ name: '2', age: 12 },{ name: '3', age: 13 }];
pNodes.data(data)
  .text(function(dom,index){
  return '姓名是'+dom.name +'第'+index+'个';
})
.style("color", function (dom, index) {
  return index % 2 === 1 ? '#000' : 'red'
});
//可以连写 style修改样式
```

### dom插入删除

- insert 在元素前面插入

  ```javascript
  // <p id="pid">111</p> 这个之前
  d3.select('body').insert('p','#pid').text("insert p dom");
  ```

- append 在select的元素集末尾插入

- remove

  ```javascript
  //select出来要删除的元素
  d3.select('body').select('#pid').remove();
  ```

### 开始画图表

```javascript
var svg = d3.select('#chart')         //文档中弄个div id是chart
        .append("svg")                //在chart中append一个svg元素
        .attr('width', '500px')       //设置宽高
        .attr('height', '400px');

var data = [250, 210, 170, 130, 90];  //数据数组 放的是长方形的宽
var rectHeight = 25;
//依据data数据来创建多个长方形
svg.selectAll("rect")
        .data(data)
        .enter()
        .append("rect")
        .attr("x", 0)
        .attr("y", function (d, i) {
            return i * rectHeight;
        })
        .attr("width", function (d, i) {
            return d;
        })
        .attr("height", rectHeight - 2)
        .attr("fill", "#ccc");    //svg中填充
```

实际运用中大部分的图都是这样，没有预先的dom，然后通过数据来对应创建的。