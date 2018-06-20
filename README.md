# leftMenu

leftMenu 是经典企业web应用左侧菜单插件。

列表数据通过 AJAX 获取，也可以自定义，数据内容使用 JSON 格式。


**版本：**

* jQuery v1.7+ | Zepto v1.0+

文档：https://github.com/vesung/leftMenu

## 使用方法
### 载入 JavaScript 文件
```html
<script src="jquery.js"></script>
```

### DOM 结构
```html
---
```

### 设置默认值
```html
<!--
方法一：使用 option 的 value 和 selected 属性
--> 

```

### 调用 leftMenu
``` javascript
$('#element_id').leftMenu({
  url: 'cityData.min.json',               // 提示：如果服务器不支持 .json 类型文件，请将文件改为 .js 文件
  selects: ['province', 'city', 'area'],  // selects 为数组形式，请注意顺序
  emptyStyle: 'none'
});
```

### 设置参数全局默认值
``` javascript
// 需在引入 <script src="jquery.leftMenu.js"></script> 之后，调用之前设置
$.leftMenu.defaults.url = 'cityData.min.json';
$.leftMenu.defaults.emptyStyle = 'none';
```

### API 接口
``` javascript
var leftMenuApi;

// 方法一：
leftMenuApi = $.leftMenu($('#element_id'), {
  selects: ['province', 'city', 'area']
});

// 方法二：
$('#element_id').leftMenu({
  selects: ['province', 'city', 'area']
}, function(api) {
  leftMenuApi = api;
});

leftMenuApi.attach();
leftMenuApi.detach();
leftMenuApi.clear();
leftMenuApi.setOptions();
```

## 参数说明
名称|默认值|说明
---|---|---
selects|[]|下拉选框组。<br>输入 select 的 className
url|null|整合数据接口地址（URL）；<br>每个选框的内容使用各自的接口地址，详见 [DEMO](http://code.ciaoca.com/jquery/leftMenu/demo/oneself.html)
data|null|自定义数据，类型为数组，使用 JSON 格式。[DEMO](http://code.ciaoca.com/jquery/leftMenu/demo/custom.html)
emptyStyle|null|子集无数据时 select 元素的显示状态。<br>可设置为：**"none"**(display:none), **"hidden"**(visibility:hidden)
required|false|是否为必选。<br>设为 `false` 时，会在列表头部添加 `<option value="firstValue">firstTitle</option>` 选项。
firstTitle|'请选择'|选框第一个项目的标题（仅在 `required` 为 `false` 时有效）
firstValue|''|选框第一个项目的值（仅在 `required` 为 `false` 时有效）
jsonSpace|''|数据命名空间
jsonName|'n'|数据标题字段名称（用于 option 的标题）
jsonValue|''|数据值字段名称（用于 option 的 value，没有值字段时使用标题作为 value）
jsonSub|'s'|子集数据字段名称


## data 属性参数
### 父元素的 data- 属性
```html
<div id="element_id" data-url="cityData.min.json" data-required="true"></select>
```

名称|说明
---|---
data-selects|下拉选框组。<br>输入 select 的 className，使用英文逗号分隔的字符串
data-url|列表数据接口地址
data-empty-style|子集无数据时 select 的显示状态
data-required|是否为必选
data-first-title|选框第一个项目的标题
data-first-value|选框第一个项目的值
data-json-space|数据命名空间
data-json-name|数据标题字段名称
data-json-value|数据值字段名称
data-json-sub|子集数据字段名称

### select 元素的 data- 属性
```html
<select class="province" data-value="浙江省" data-first-title="选择省"></select>
```

名称|说明
---|---
data-value|默认选中值
data-url|列表数据接口地址
data-required|是否为必选
data-query-name|传递上一个选框值的参数名称（默认使用上一个选框的 name 属性值）
data-first-title|选框第一个项目的标题
data-first-value|选框第一个项目的值
data-json-space|数据命名空间
data-json-name|数据标题字段名称
data-json-value|数据值字段名称

## API 接口

名称|说明
---|---
attach()|绑定。<br>调用时会自动进行绑定，用于使用detach解除绑定后，进行重新绑定。
detach()|解除绑定。<br>解除绑定后，不再具有联动效果。
clear(index)|清空选项。<br>清空第 index 个 select 自身及之后的 select 的选项。<br>`index`: select 的序号，从 0 开始
setOptions(settings)|重新设置参数。<br>`settings`: 与调用时参数一致

## 自定义数据及使用纯数组数据
可以使用任何类型的数据作为值，但最终都会被转化为文本。

[自定义数据 DEMO](http://code.ciaoca.com/jquery/leftMenu/demo/custom.html)


## 各选项数据接口独立
可以为每个```select```设置一个接口，根据接口返回的数据结构，设置```json-space```、```json-name```、```json-value```适应 JSON 结构（包括纯数组）。
当页面加载时，第一个选框已有选项数据，可以不设置第一个选框的接口。

[独立接口 DEMO](http://code.ciaoca.com/jquery/leftMenu/demo/oneself.html)
