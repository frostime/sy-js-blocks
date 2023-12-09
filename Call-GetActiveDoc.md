## [Callable] GetActive Doc | 获取正在编辑的文档

> Call this code block to get the current editing document's ID
> 调用此代码, 可以获取当前正在编辑的文档的 ID

```js
function getActiveDoc() {
    let tab = document.querySelector("div.layout__wnd--active ul.layout-tab-bar>li.item--focus");
    let dataId= tab?.getAttribute("data-id");
    if (!dataId) {
        return null;
    }
    const activeTab = document.querySelector(
        `.layout-tab-container.fn__flex-1>div.protyle[data-id="${dataId}"]`
    );
    const eleTitle = activeTab.querySelector(".protyle-title");
    let docId = eleTitle.getAttribute("data-node-id");
    return docId;
}
return getActiveDoc();
```
{: name="GetActiveDoc"}

