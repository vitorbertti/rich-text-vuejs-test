<template>
  <div class="editor-container">
    <h1>Rich Text</h1>
    <div class="options">
      <button class="button" id="boldButton" title="Bold">B</button>
      <button class="button" id="italicButton" title="Italic">
        <em>I</em>
      </button>
    </div>
    <div class="richtext">
      <iframe title="richtext" name="richtext" id="richtext" frameborder="0"></iframe>
    </div>
  </div>
</template>

<script>
const editor = document.getElementsByName("richtext");
console.log(editor);

export default {
  name: "HelloWorld",
  mounted() {
    window.addEventListener("load", () => {
      let frame = editor[0].contentDocument || editor[0].contentWindow.document;
      frame.designMode = "on";
    });
  }
};
</script>

<style scoped>
.editor-container {
  margin: 30px auto;
  width: 650px;
  height: 200px;
  background: #f0f0f5;
}

.editor-container h1 {
  font-size: 30px;
  text-align: center;
}

.editor-container .options {
  border-bottom: none;
  padding: 10px;
  background-color: #451846;
  color: #fff;
  border-radius: 8px 8px 0px 0px;
  width: 746px;
  margin-top: 10px;
}

.editor-container .options .button {
  color: #fff;
  border: none;
  outline: none;
  background-color: transparent;
  cursor: pointer;
  margin: 0 5px;
}

.editor-container .richtext {
  border: 2px solid rgb(16, 17, 17);
  height: 100%;
  width: 746px;
  background-color: #fff;
  align-items: center;
}

iframe#richtext {
  height: 100%;
  width: 100%;
}
</style>
