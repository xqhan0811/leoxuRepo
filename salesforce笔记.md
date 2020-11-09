# Lightning

1.组件属性类型

```html
<aura:attribute name="data" type="Object" />
```

推荐使用 type="Map" 替代  type="Object"

2.<a> 标签 不推荐使用 


推荐使用 事件 force:navigateToSObject或者force:navigateToURL替代

3.导航服务

**lightning:navigation**
	Navigates to a page or component.
**lightning:isUrlAddressable**
	Enable a component to be navigated directly via a URL.

推荐使用 导航事件

**force:navigateToList**
	Navigates to a list view.
**force:navigateToObjectHome**
	Navigates to an object home.
**force:navigateToRelatedList**
	Navigates to a related list.
**force:navigateToSObject**
	Navigates to a record.
**force:navigateToURL**
	Navigates to a URL.

4.css样式

`.THIS` 表示顶层元素

5.检查变量类型

不推荐 `instanceof`  推荐 `typeof` or a standard JavaScript method instead