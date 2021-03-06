# mip-baobao-list 列表组件

可以渲染同步数据，或者异步请求数据后渲染。

标题|内容
----|----
类型|通用
支持布局|responsive, fixed-height, fill, container, fixed
所需脚本|<https://c.mipcdn.com/static/v2/mip-list/mip-list.js></br>
<https://c.mipcdn.com/static/v2/mip-mustache/mip-mustache.js>

## 示例

### 基本用法

> JSONP 异步请求的接口需要遵循规范 `callback` 为 `'callback'`。

```html
<mip-list src="https://raw.githubusercontent.com/mipengine/mip2-extensions/master/components/mip-list/example/data.js" preload>
  <template type="mip-mustache">
    <div>
      <li>name: {{ name }}</li>
      <li>alias: {{ alias }}</li>
    </div>
  </template>
</mip-list>
```

### 定制模板

```html
<mip-list
  template="mip-template-id1"
  src="https://raw.githubusercontent.com/mipengine/mip2-extensions/master/components/mip-list/example/data.js"
  preload
>
  <template type="mip-mustache" id="mip-template-id1">
    <div>
      <li>name: {{ name }}</li>
      <li>alias: {{ alias }}</li>
    </div>
  </template>
</mip-list>
```

### 同步数据

```html
<mip-list synchronous-data>
  <script type="application/json">
    {
      "items": [{
        "name": "lee",
        "alias": "xialong"
      }, {
        "name": "ruige",
        "alias": "ruimm"
      }, {
        "name": "langbo",
        "alias": "bobo"
      }]
    }
  </script>
  <template type="mip-mustache">
    <div>
      <li>name: {{ name }}</li>
      <li>alias: {{ alias }}</li>
    </div>
  </template>
</mip-list>
```

### 点击加载更多

> 有 `has-more` 属性时，`<mip-list>` 标签必须要有 `id` 属性，同时需要有点击按钮的 DOM 节点，并且此节点有 `on` 属性，属性值为：`tap:对应mip-list的id.more`

```html
<mip-list
  template="mip-template-id2"
  src="https://raw.githubusercontent.com/mipengine/mip2-extensions/master/components/mip-list/example/data-has-more.js"
  id="mip-list"
  has-more
  pn-name="pageNum"
  rn-name="rnNum"
  pn="2"
  rn="1"
  timeout="3000"
  preload
  end-text="数据加载完毕"
>
  <template type="mip-mustache" id="mip-template-id2">
    <div>
      <li>name: {{ name }}</li>
    </div>
  </template>
</mip-list>
<button on="tap:mip-list.more">点击查看更多</button>
```

## 属性

### load-src

说明：异步请求的数据接口，如果没有其他参数结尾请不要带 `？`(原src,为了避让mip-cache改写策略)

必选项：否

类型：字符串

取值范围：必须是 HTTPS 的

单位：无

默认值：无

### synchronous-data

说明：使用同步数据开关属性

必选项：否

类型：字符串

取值范围：无

单位：无

默认值：无

### id

说明：`<mip-list>` 组件 `id`

必选项：否

类型：字符串

取值范围：字符串

单位：无

默认值：无

### has-more

说明：是否有点击展开更多功能

必选项：否

类型：字符串

取值范围：无

单位：无

默认值：无

### pn-name

说明：翻页变量名

必选项：否

类型：字符串

取值范围：无

单位：无

默认值：pn

### pn

说明：翻页初始页码，每次请求会自动加 1

必选项：否

类型：整数

取值范围：无

单位：无

默认值：1

### rn-name

说明：步长变量名

必选项：否

类型：字符串

取值范围：无

单位：无

默认值：rn

### rn

说明：翻页步长值，每次加载条数

必选项：否

类型：整数

取值范围：无

单位：无

默认值：1 （默认加载更多是1条数据）

### preload

说明：异步加载数据，如果添加 `preload` 参数，则在初始化时加载第一页内容

必选项：否

### timeout

说明：fetch-jsonp 请求的超时时间

必选项：否

类型：整数

取值范围：无

单位：ms

默认值：5000

### end-text

说明：没有更多数据底部提示文字，特殊值empty，无文字提示

必选项：否

类型：字符串

取值范围：无

单位：无

默认值：已经加载完毕

### data-[XX]

说明：异步请求自定义参数，XX为请求key,无数量限制(data-xx可根据异步返回数据更新,data-xx与返回数据键相同时更新)

必选项：否

类型：无

取值范围：无

单位：无

默认值：无

## 注意事项

- 接口返回的数据格式需要是如下格式：
    - status：0 表示请求成功。
    - items：[] 是需要渲染的数序。
    - isEnd：表示是否是最后一页，非必须。

```
{
  status: 0,
  data: {
    items: [],
    isEnd: 1
  }
}
```
