## [Script] 粘贴 Markdown 文本 | Past Markdown

- 需求 | Require: `GetFocusedBlock`

> 读取剪贴板里的 markdown 内容，然后间隔 2 秒后将其作为内容插入到光标点击的块下（我经常粘贴 markdonw 到思源里失败，也不知道为什么……）


```js
const main = async (text) => {
    if (text === undefined || text === null || text === '') {
        siyuan.showMessage('剪贴板内无内容', 3000, 'error');
    }
    console.log(text);
    let ele = await plugin.call('GetFocusedBlock');
    if (ele === undefined || ele === null) {
        siyuan.showMessage('无法定位到光标', 2000, 'error');
        return;
    }
    let nodeId = ele.getAttribute('data-node-id')
    //let block = await api.getBlockByID(nodeId);
    api.insertBlock('markdown', text, null, nodeId, null);
    siyuan.showMessage('Insert done', 2000);
}

setTimeout(
    () => {navigator.clipboard.readText().then(main)},
    2500,
)
```
{: name="Past Markdown"}
