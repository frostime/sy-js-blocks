## [Script] 转义 SQL | Escape SQL

> 读取剪贴板当中的 SQL 代码，然后把换行符 `\n` 转换成 `_esc_newline_` 再写回剪贴板; 主要是方便写模板

```js
const escape = (sql) => {
  return sql.replaceAll(/\r?\n/g, '_esc_newline_');
}

navigator.clipboard.readText().then((text) => {
  if (text === undefined || text === null || text === '') {
      siyuan.showMessage('Nothing in clipboard', 3000, 'error');
  }
  text = escape(text)
  console.log(text);
  navigator.clipboard.writeText(text).then(
      function () {
        siyuan.showMessage('Done', 3000);
      },
      function () {
        /* clipboard write failed */
      },
   );
});
```
{: name="Escape SQL"}