<template>
  <div class="">
    <div class="container">
      <div class="">
        <input
            v-model="currentText"
            @keypress.enter="addText"
            placeholder="Введите текст"
            class="input"
        />
        <button @click="addText" class="input-btn">+</button>
      </div>
      <div class="">
        <input
            v-model="imageUrl"
            @keypress.enter="addImage"
            placeholder="Введите URL изображения"
            class="input"
        />
        <button @click="addImage" class="input-btn">+</button>
      </div>
    </div>
    <div class="controls">
      <button @click="undo" :disabled="!canUndo" class="control-btn">
        <svg width="22" height="20" viewBox="0 0 22 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M18.6358 19.5824C18.3582 19.86 17.9929 20 17.6299 20C17.2645 20 16.8992 19.86 16.6216 19.5824C16.0664 19.0249 16.0664 18.1257 16.6216 17.5682C19.7604 14.4294 19.7604 9.32384 16.6216 6.18505C13.4852 3.04864 8.37722 3.04864 5.24081 6.18505L4.72598 6.69988H8.12337C8.90866 6.69988 9.54686 7.33808 9.54686 8.12337C9.54686 8.91103 8.90866 9.54686 8.12337 9.54686H1.42349C0.638197 9.54686 0 8.91103 0 8.12337V1.42349C0 0.638197 0.638197 0 1.42349 0C2.20878 0 2.84697 0.638197 2.84697 1.42349V4.55279L3.22657 4.17319C7.47568 -0.0759193 14.3867 -0.0759193 18.6358 4.17319C22.8849 8.4223 22.8849 15.3333 18.6358 19.5824Z" fill="#639EFF"/>
        </svg>
      </button>
      <button @click="redo" :disabled="!canRedo" class="control-btn">
        <svg width="22" height="20" viewBox="0 0 22 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M3.18684 19.5824C3.46442 19.86 3.82978 20 4.19277 20C4.55813 20 4.92349 19.86 5.20107 19.5824C5.75624 19.0249 5.75624 18.1257 5.20107 17.5682C2.06229 14.4294 2.06229 9.32384 5.20107 6.18505C8.33749 3.04864 13.4454 3.04864 16.5819 6.18505L17.0967 6.69988H13.6993C12.914 6.69988 12.2758 7.33808 12.2758 8.12337C12.2758 8.91103 12.914 9.54686 13.6993 9.54686H20.3992C21.1845 9.54686 21.8227 8.91103 21.8227 8.12337V1.42349C21.8227 0.638197 21.1845 0 20.3992 0C19.6139 0 18.9757 0.638197 18.9757 1.42349V4.55279L18.5961 4.17319C14.347 -0.0759193 7.43595 -0.0759193 3.18684 4.17319C-1.06227 8.4223 -1.06227 15.3333 3.18684 19.5824Z" fill="#639EFF"/>
        </svg>
      </button>
      <button @click="splitSelectedText" :disabled="!hasSelection" class="control-btn">
        <svg width="20" height="23" viewBox="0 0 20 23" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M20 1.5V4.0075C20 4.8375 19.3317 5.5075 18.5037 5.5075C17.6783 5.5075 17.0075 4.8375 17.0075 4.0075V3H11.4963V20H12.8454C13.6733 20 14.3416 20.6725 14.3416 21.5C14.3416 22.3275 13.6733 23 12.8454 23H7.15461C6.32668 23 5.65835 22.3275 5.65835 21.5C5.65835 20.6725 6.32668 20 7.15461 20H8.50374V3H2.99252V4.0075C2.99252 4.8375 2.3217 5.5075 1.49626 5.5075C0.668329 5.5075 0 4.8375 0 4.0075V1.5C0 0.6725 0.668329 0 1.49626 0H18.5037C19.3317 0 20 0.6725 20 1.5Z" fill="#639EFF"/>
        </svg>
      </button>
      <button @click="makeHeading" :disabled="!hasSelection" class="control-btn">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M13.4876 9.74158V11.0604C13.4876 11.9872 12.7344 12.7404 11.8076 12.7404C11.004 12.7404 10.332 12.1748 10.1668 11.4216H9.0048V18.5868C9.8476 18.6792 10.5056 19.3932 10.5056 20.2584C10.5056 21.188 9.7524 21.9384 8.8256 21.9384H5.824C4.89439 21.9384 4.14399 21.188 4.14399 20.2584C4.14399 19.3932 4.7992 18.6792 5.64479 18.5868V11.4216H4.48C4.3148 12.1748 3.6428 12.7404 2.8392 12.7404C1.9124 12.7404 1.15919 11.9872 1.15919 11.0604V9.74158C1.15919 8.81198 1.9124 8.06158 2.8392 8.06158H11.8076C12.7344 8.06158 13.4876 8.81198 13.4876 9.74158Z" fill="#639EFF"/>
          <path d="M26.9192 9.74158V11.0604C26.9192 11.9872 26.1688 12.7404 25.2392 12.7404C24.4356 12.7404 23.7636 12.1748 23.5984 11.4216H22.4364V18.5868C23.2792 18.6792 23.9372 19.3932 23.9372 20.2584C23.9372 21.188 23.184 21.9384 22.2572 21.9384H19.2556C18.326 21.9384 17.5756 21.188 17.5756 20.2584C17.5756 19.3932 18.2308 18.6792 19.0764 18.5868V11.4216H17.9144C17.7492 12.1748 17.0772 12.7404 16.2708 12.7404C15.344 12.7404 14.5908 11.9872 14.5908 11.0604V9.74158C14.5908 8.81198 15.344 8.06158 16.2708 8.06158H25.2392C26.1688 8.06158 26.9192 8.81198 26.9192 9.74158Z" fill="#639EFF"/>
        </svg>
      </button>
      <button @click="copyHtmlToClipboard" class="text-btn">Скопировать HTML</button>
      <button @click="deleteSelectedText" :disabled="!hasSelection" class="text-btn">Удалить выделенный текст</button>
      <button @click="editSelectedText" :disabled="!hasSelection" class="text-btn">Изменить текст</button>
    </div>
    <div class="text-list" ref="textList">
      <div
          v-for="(text, index) in texts"
          :key="index"
          :class="{'heading': text.isHeading}"
          @mouseup="updateSelection($event, index)"
          v-html="text.content"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentText: "",
      imageUrl: "",
      texts: [
          {content: 'Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.', isHeading: false},
          {content: `<h1>Смотрите какие обезьянки</h1>`, isHeading: false},
          {content: `<img src="https://www.wearegecko.co.uk/media/50316/mountain-3.jpg" style="max-width: 100%;">`, isHeading: false},
          {content: 'Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой инйцу шо шщйоц ущойц ущошцщйуо йцщуо йщцоу щйоу шщйцош ущйтересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.', isHeading: false},
          {content: 'Товарищи! новая модель организационной деятельности требуют от нас анализа направлений прогрессивного развития. Задача организации, в особенности же постоянный количественный рост и сфера нашей активности требуют от нас анализа позиций, занимаемых участниками в отношении поставленных задач. Задача организации, в особенности же реализация намеченных плановых заданий требуют от нас анализа системы обучения кадров, соответствует насущным потребностям.', isHeading: false}
      ],
      history: [],
      historyIndex: 0,
      selection: null, 
    };
  },
  computed: {
    canUndo() {
      return this.historyIndex > 0;
    },
    canRedo() {
      return this.historyIndex < this.history.length - 1;
    },
    hasSelection() {
      return this.selection && this.selection.text.trim() !== "";
    },
  },
  methods: {
    saveToHistory() {
      if (this.historyIndex < this.history.length - 1) {
        this.history.splice(this.historyIndex + 1);
      }
      this.history.push(JSON.parse(JSON.stringify(this.texts)));
      this.historyIndex = this.history.length - 1;
    },
    addText() {
      if (this.currentText.trim() !== "") {
        this.texts.push({ content: this.currentText.trim(), isHeading: false });
        this.saveToHistory();
        this.currentText = "";
      }
    },
    addImage() {
      if (this.imageUrl.trim() !== "") {
        const imgTag = `<img src="${this.imageUrl.trim()}" style="max-width: 100%;">`;
        this.texts.push({ content: imgTag, isHeading: false });
        this.saveToHistory();
        this.imageUrl = "";
      }
    },
    undo() {
      if (this.canUndo) {
        this.historyIndex--;
        this.texts = JSON.parse(JSON.stringify(this.history[this.historyIndex]));
      }
    },
    redo() {
      if (this.canRedo) {
        this.historyIndex++;
        this.texts = JSON.parse(JSON.stringify(this.history[this.historyIndex]));
      }
    },
    updateSelection(event, index) {
      const selection = window.getSelection();
      const selectedText = selection.toString();
      if (selectedText.trim()) {
        this.selection = {
          text: selectedText,
          index,
          start: selection.anchorOffset,
          end: selection.focusOffset,
        };
      } else {
        this.selection = null;
      }
    },
    splitSelectedText() {
      if (!this.selection) return;

      const { text, index, start, end } = this.selection;
      const originalText = this.texts[index].content;

      const before = originalText.slice(0, start);
      const selected = text.trim();
      const after = originalText.slice(end);

      const newTexts = this.texts.slice();
      newTexts.splice(index, 1, { content: before, isHeading: false }, { content: selected, isHeading: false }, { content: after, isHeading: false });
      this.texts = newTexts.filter((t) => t.content);

      this.saveToHistory();
      this.selection = null;
    },
    makeHeading() {
      if (!this.selection) return;

      const { text, index, start, end } = this.selection;
      const originalText = this.texts[index].content;

      const before = originalText.slice(0, start);
      const selected = text.trim();
      const after = originalText.slice(end);

      const newTexts = this.texts.slice();
      newTexts.splice(
          index,
          1,
          { content: before, isHeading: false },
          { content: `<h1>${selected}</h1>`, isHeading: true },
          { content: after, isHeading: false }
      );
      this.texts = newTexts.filter((t) => t.content);

      this.saveToHistory();
      this.selection = null;
    },
    copyHtmlToClipboard() {
      const htmlContent = this.$refs.textList.innerHTML;

      navigator.clipboard.writeText(htmlContent)
          .then(() => {
            alert("HTML скопирован в буфер обмена!");
          })
          .catch((err) => {
            console.error("Ошибка копирования в буфер обмена", err);
          });
    },
    deleteSelectedText() {
      if (!this.selection) return;

      const { index, start, end } = this.selection;
      const originalText = this.texts[index].content;

      const before = originalText.slice(0, start);
      const after = originalText.slice(end);

      const newTexts = this.texts.slice();
      newTexts.splice(index, 1, { content: before + after, isHeading: false });
      this.texts = newTexts.filter((t) => t.content);

      this.saveToHistory();
      this.selection = null;
    },
    editSelectedText() {
      if (!this.selection) return;

      const newText = prompt("Введите новый текст:", this.selection.text);
      if (newText !== null) {
        const { index, start, end } = this.selection;
        const originalText = this.texts[index].content;

        const before = originalText.slice(0, start);
        const after = originalText.slice(end);

        const newTexts = this.texts.slice();
        newTexts.splice(
            index,
            1,
            { content: before + newText + after, isHeading: false }
        );
        this.texts = newTexts.filter((t) => t.content);

        this.saveToHistory();
        this.selection = null;
      }
    },
  },
  mounted() {
    this.saveToHistory();
  },
};
</script>

<style scoped>

.container {
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
  gap: 20px;
}

.input {
  width: 400px;
  padding: 10px;
  font-size: 16px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.input:focus,.input:active{
  border: none;
  outline: none;
}
.input-btn {
  padding: 10px 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.input-btn:hover {
  background-color: #45a049;
}

.controls {
  margin-bottom: 20px;
  display: flex;
  gap: 20px;
}


.control-btn{
  background: #282828;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 52px;
  height: 48px;
  border: none;
  border-radius: 6px;
}
.control-btn:disabled{
  background: #3b3b3b;
}
.text-btn{
  background: none;
  border: none;
  font-size: 20px;
  color: #639EFF;
}
.text-btn:disabled{
  color: #b2cffd;
}
.text-list {
  margin-top: 20px;
}

.text-list div {
  margin-bottom: 10px;
}

.text-list .heading {
  font-size: 1.5em;
  font-weight: bold;
}

.text-list img {
  max-width: 100%;
}

</style>
