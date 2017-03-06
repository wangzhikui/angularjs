# UI使用

这两个系统使用了一个付费的joli UI，joli模板基于Bootstrap，特别适合于管理系统的开发。

**使用**

joli UI没有使用文档，使用时参照其示例代码进行开发，其示例代码位于exam\/joli下。
1. 首先用浏览器打开joli的html文件，然后找到需要的组件，并定位到其HTML文件。
2. 用IDE打开HTML文件，找到相关的代码片段，将其拷贝到需要的地方。
3. 使用Angular指令等进行数据填充。

### 1. 表单数据

a. 表单数据使用表单Panel，样式文件位于 form-layouts-one-column.html 中。

b. 包含三部分内容（顶部填写标题，中间区域为表单内容，底部为按钮区域（清空和提交））。

![](/assets/屏幕快照 2016-07-19 下午3.35.47.png)

### 2.表格数据

### 2.1 使用

a. 表格数据使用表单Panel，文件位于table-basic.html 中。

b. 包含三部分内容（顶部填写标题，中间区域为表格数据内容，底部为分页信息\[如果需要分页\]）。

![](/assets/屏幕快照 2016-07-27 下午2.49.04.png)

### 2.2 表格样式

a. 所有的表格添加样式 &lt;table class="table table-bordered"&gt;

b. 表格整行可点击的，添加 &lt;table class="table-hover"&gt;；不可点击的添加隔行换色样式 &lt;table class="table-striped"&gt;

c. **图标：**使用图片按钮，图片样式样式可从joli的表格页面中拷贝。

![](/assets/屏幕快照 2016-07-27 下午2.54.49.png)

### 2.3 分页样式

a. 分页数据使用joli分页样式，样式在文件 table-datatables.html 中。

b. 不要添加 class="datatable"，分页样式直接引入HTML片段

**以下文字修改为中文：**

```
Show 10 entries --> 每页 10 条

Search  --> 搜索

Previous  -->  上一页

Next  -->  下一页

左下角内容(Showing 1 to 10 of 57 entries)  -->  共57条记录
```

![](/assets/屏幕快照 2016-07-19 下午3.38.41.png)

### 3. Panel操作区域

a. Panel操作区域样式使用图标按钮，如下图右上角操作区，样式文件位于 ui-panels.html 中。

b.使用场景：应用列表页的添加应用按钮。

![](/assets/屏幕快照 2016-07-19 下午4.06.24.png)

### 

