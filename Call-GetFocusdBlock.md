## [Callable] Get Focused Block | 获取正在编辑的块 ID

> 调用此代码, 可以获取当前光标聚焦的块的 ID
> Call this code block to get the current editing block's ID
> Copyright (c) 2023 Zuoqiu-Yingyi


```js
function isSiyuanBlock(element) {
    return !!(element
        && element instanceof HTMLElement
        && element.dataset.type
        && element.dataset.nodeId
        && /^\d{14}-[0-9a-z]{7}$/.test(element.dataset.nodeId)
    );
}

/**
 * Copyright (c) 2023 [Zuoqiu-Yingyi](https://github.com/Zuoqiu-Yingyi/siyuan-packages-monorepo)
 * 获取当前光标所在的块
 * @returns 当前光标所在的块的 HTML 元素
 */
function getFocusedBlock() {
    const selection = document.getSelection();
    let element = selection?.focusNode;
    while (element // 元素存在
        && (!(element instanceof HTMLElement) // 元素非 HTMLElement
            || !isSiyuanBlock(element) // 元素非思源块元素
        )
    ) {
        element = element.parentElement;
    }
    return element ?? null;
}

return getFocusedBlock();
```
{: name="GetFocusedBlock"}

