```js
const inputDialog = (title, confirm=null, cancel=null) => {
    const dialog = new siyuan.Dialog({
        title,
        content: `<div class="b3-dialog__content">
    <div class="ft__breakword"><textarea class="b3-text-field fn__block" style="height: 100%;"></textarea></div>
</div>
<div class="b3-dialog__action">
    <button class="b3-button b3-button--cancel">${window.siyuan.languages.cancel}</button><div class="fn__space"></div>
    <button class="b3-button b3-button--text" id="confirmDialogConfirmBtn">${window.siyuan.languages.confirm}</button>
</div>`,
        width: "520px",
    });
    const target = dialog.element.querySelector(".b3-dialog__content>div.ft__breakword>textarea");
    const btnsElement = dialog.element.querySelectorAll(".b3-button");
    btnsElement[0].addEventListener("click", () => {
        if (cancel) {
            cancel();
        }
        dialog.destroy();
    });
    btnsElement[1].addEventListener("click", () => {
        if (confirm) {
            confirm(target.value);
        }
        dialog.destroy();
    });
};
let title = "Input";
if (args.length > 0) {
  title = args[0];
}
return new Promise((resolve, reject) => {
  inputDialog(title, resolve, reject);
});
```