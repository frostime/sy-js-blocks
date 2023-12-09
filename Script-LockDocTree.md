## [Script] 锁定文档树 | Lock document tree

> 使用此代码，会将正在编辑的文档下属的所有文档全部锁定，变为「只读」


```js
async function getOffspring(blockId) {
  let sql = `
    select root_id from blocks where path like "%${blockId}/%" and type="d" order by created limit 999
  `;
  let blocks = api.sql(sql.trim());
  return blocks;
}
async function lockit(rootBlockId) {
  if (!rootBlockId) {
    siyuan.showMessage("没有找到打开中的文档");
  }
  console.log(client)
  let blocks = await getOffspring(rootBlockId);
  let ids = blocks.map((block) => block.root_id);
  ids = [rootBlockId, ...ids];
  let promises = [];
  ids.forEach((id) => {
    let p = client.setBlockAttrs({id: id, attrs: {"custom-sy-readonly": "true"}});
    promises.push(p);
  });
  let res = await Promise.all(promises);
  let N = res.length;
  siyuan.showMessage(`锁定共${N}个文档`);
  console.log(res);
}
plugin.call('GetActiveDoc').then((docId) => {
  if (docId) {
    lockit(docId);
  }
});
```
{: name="Lock Doc Tree"}

