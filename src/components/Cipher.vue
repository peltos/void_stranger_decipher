<template>
  <div class="cipher-wrapper-wrapper">
    <div class="cipher-wrapper">
      <div class="cipher d-flex flex-column align-center">
        <div class="cipher-row d-flex">
          <input type="checkbox" id="CheckboxTL" v-model="pattern[0]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxTL">7</label>

          <input type="checkbox" id="CheckboxTM" v-model="pattern[1]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxTM">8</label>

          <input type="checkbox" id="CheckboxTR" v-model="pattern[2]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxTR">9</label>
        </div>
        <div class="cipher-row d-flex">
          <input type="checkbox" id="CheckboxML" v-model="pattern[3]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxML">4</label>

          <div :class="`cipher-hollow ${validPaternStyle ? 'wrong' : ''}`"> X </div>

          <input type="checkbox" id="CheckboxMR" v-model="pattern[4]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxMR">6</label>
        </div>
        <div class="cipher-row d-flex">
          <input type="checkbox" id="CheckboxBL" v-model="pattern[5]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxBL">1</label>

          <input type="checkbox" id="CheckboxBM" v-model="pattern[6]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxBM">2</label>

          <input type="checkbox" id="CheckboxBR" v-model="pattern[7]" v-on:change="patternChanged()" />
          <label class="cipher-input" for="CheckboxBR">3</label>
        </div>
      </div>
    </div>
  </div>
  <v-btn @click="submitPattern">
    Enter
  </v-btn>
  <v-btn @click="clearPattern" @keydown="preventEnterKey">
    Clear
  </v-btn>
  <p>(you can use the numpad and enter key on your keyboard)</p>
  <section class="cipher-textarea-wrapper">
    <span>⠇⠀ ⠧⠀ ⠃⠀ ⠅⠆ ⠡⠂ </span>
    <textarea class="cipher-textarea" label="Label" @keyup="decipherText" v-model="cipher"></textarea>
  </section>
  <section class="cipher-textarea-wrapper">
    <span>INPUT</span>
    <textarea class="decipher-textarea" label="Label" @keyup="cipherText" v-model="decipher"></textarea>
  </section>
</template>

<script setup>
import { ref } from 'vue'

let pattern = ref([false, false, false,
  false, false,
  false, false, false])

let cipher = ref('')
let decipher = ref('')

let validPatern = ref(false)
let validPaternStyle = ref(false)

function preventEnterKey(e) {
  e.preventDefault();
}

function cipherText(e) {
  let textArray = e.target.value.split('')
  cipher.value = ''

  textArray.forEach(letter => {
    if(letter === 'a' || letter === 'A') cipher.value = '⠡⠀ '+cipher.value;
    if(letter === 'b' || letter === 'B') cipher.value = '⠁⠄ '+cipher.value;
    if(letter === 'c' || letter === 'C') cipher.value = '⠡⠄ '+cipher.value;
    if(letter === 'd' || letter === 'D') cipher.value = '⠅⠀ '+cipher.value;
    if(letter === 'e' || letter === 'E') cipher.value = '⠥⠀ '+cipher.value;
    if(letter === 'f' || letter === 'F') cipher.value = '⠅⠄ '+cipher.value;
    if(letter === 'g' || letter === 'G') cipher.value = '⠥⠄ '+cipher.value;
    if(letter === 'h' || letter === 'H') cipher.value = '⠁⠂ '+cipher.value;
    if(letter === 'i' || letter === 'I') cipher.value = '⠡⠂ '+cipher.value;
    if(letter === 'j' || letter === 'J') cipher.value = '⠁⠆ '+cipher.value;
    if(letter === 'k' || letter === 'K') cipher.value = '⠁⠴ '+cipher.value;
    if(letter === 'l' || letter === 'L') cipher.value = '⠅⠂ '+cipher.value;
    if(letter === 'm' || letter === 'M') cipher.value = '⠥⠂ '+cipher.value;
    if(letter === 'n' || letter === 'N') cipher.value = '⠅⠆ '+cipher.value;
    if(letter === 'o' || letter === 'O') cipher.value = '⠥⠆ '+cipher.value;
    if(letter === 'p' || letter === 'P') cipher.value = '⠃⠀ '+cipher.value;
    if(letter === 'q' || letter === 'Q') cipher.value = '⠣⠀ '+cipher.value;
    if(letter === 'r' || letter === 'R') cipher.value = '⠃⠄ '+cipher.value;
    if(letter === 's' || letter === 'S') cipher.value = '⠣⠄ '+cipher.value;
    if(letter === 't' || letter === 'T') cipher.value = '⠇⠀ '+cipher.value;
    if(letter === 'u' || letter === 'U') cipher.value = '⠧⠀ '+cipher.value;
    if(letter === 'v' || letter === 'V') cipher.value = '⠇⠄ '+cipher.value;
    if(letter === 'w' || letter === 'W') cipher.value = '⠧⠄ '+cipher.value;
    if(letter === 'x' || letter === 'X') cipher.value = '⠃⠂ '+cipher.value;
    if(letter === 'y' || letter === 'Y') cipher.value = '⠣⠂ '+cipher.value;
    if(letter === 'z' || letter === 'Z') cipher.value = '⠃⠆ '+cipher.value;
  });
}

function decipherText(e) {
  let textArray = e.target.value.split(' ');
  let nonGlyphCharacter = false;
  
  decipher.value = '';

  if(textArray.length === 1 && textArray[0] === '') return;

  textArray.forEach(glyph => {
    if(/^[a-zA-Z]*$/.test(glyph) || nonGlyphCharacter) {
      nonGlyphCharacter = true;
      return decipher.value = 'There is a non-glyph character in your glyph input. Only use the glyph input for glyph characters'
    }  

    if(glyph === '⠡⠀') decipher.value = 'A'+decipher.value;
    if(glyph === '⠁⠄') decipher.value = 'B'+decipher.value;
    if(glyph === '⠡⠄') decipher.value = 'C'+decipher.value;
    if(glyph === '⠅⠀') decipher.value = 'D'+decipher.value;
    if(glyph === '⠥⠀') decipher.value = 'E'+decipher.value;
    if(glyph === '⠅⠄') decipher.value = 'F'+decipher.value;
    if(glyph === '⠥⠄') decipher.value = 'G'+decipher.value;
    if(glyph === '⠁⠂') decipher.value = 'H'+decipher.value;
    if(glyph === '⠡⠂') decipher.value = 'I'+decipher.value;
    if(glyph === '⠁⠆') decipher.value = 'J'+decipher.value;
    if(glyph === '⠁⠴') decipher.value = 'K'+decipher.value;
    if(glyph === '⠅⠂') decipher.value = 'L'+decipher.value;
    if(glyph === '⠥⠂') decipher.value = 'M'+decipher.value;
    if(glyph === '⠅⠆') decipher.value = 'N'+decipher.value;
    if(glyph === '⠥⠆') decipher.value = 'O'+decipher.value;
    if(glyph === '⠃⠀') decipher.value = 'P'+decipher.value;
    if(glyph === '⠣⠀') decipher.value = 'Q'+decipher.value;
    if(glyph === '⠃⠄') decipher.value = 'R'+decipher.value;
    if(glyph === '⠣⠄') decipher.value = 'S'+decipher.value;
    if(glyph === '⠇⠀') decipher.value = 'T'+decipher.value;
    if(glyph === '⠧⠀') decipher.value = 'U'+decipher.value;
    if(glyph === '⠇⠄') decipher.value = 'V'+decipher.value;
    if(glyph === '⠧⠄') decipher.value = 'W'+decipher.value;
    if(glyph === '⠃⠂') decipher.value = 'X'+decipher.value;
    if(glyph === '⠣⠂') decipher.value = 'Y'+decipher.value;
    if(glyph === '⠃⠆') decipher.value = 'Z'+decipher.value;
  });
}

function submitPattern() {
  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'A', cipher.value = '⠡⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'B', cipher.value = '⠁⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && pattern.value[7])
    decipher.value += 'C', cipher.value = '⠡⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && !pattern.value[7])
    decipher.value += 'D', cipher.value = '⠅⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'E', cipher.value = '⠥⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'F', cipher.value = '⠅⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && pattern.value[7])
    decipher.value += 'G', cipher.value = '⠥⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && !pattern.value[7])
    decipher.value += 'H', cipher.value = '⠁⠂ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'I', cipher.value = '⠡⠂ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'J', cipher.value = '⠁⠆ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && pattern.value[7])
    decipher.value += 'K', cipher.value = '⠁⠴ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && !pattern.value[7])
    decipher.value += 'L', cipher.value = '⠅⠂ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'M', cipher.value = '⠥⠂ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'N', cipher.value = '⠅⠆ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && pattern.value[7])
    decipher.value += 'O', cipher.value = '⠥⠆ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && !pattern.value[7])
    decipher.value += 'P', cipher.value = '⠃⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'Q', cipher.value = '⠣⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'R', cipher.value = '⠃⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && pattern.value[7])
    decipher.value += 'S', cipher.value = '⠣⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && !pattern.value[7])
    decipher.value += 'T', cipher.value = '⠇⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'U', cipher.value = '⠧⠀ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'V', cipher.value = '⠇⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && pattern.value[7])
    decipher.value += 'W', cipher.value = '⠧⠄ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && !pattern.value[7])
    decipher.value += 'X', cipher.value = '⠃⠂ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7])
    decipher.value += 'Y', cipher.value = '⠣⠂ '+cipher.value, validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7])
    decipher.value += 'Z', cipher.value = '⠃⠆ '+cipher.value, validPatern.value = true

  if (!validPatern.value) {
    validPaternStyle.value = true;
    setTimeout(() => {
      validPaternStyle.value = false;
    }, 1000)
  }

  validPatern.value = false
  pattern.value = [false, false, false,
    false, false,
    false, false, false]
}

function clearPattern() {
  pattern.value = [false, false, false,
    false, false,
    false, false, false];
  cipher.value = '';
  decipher.value = '';
}

window.addEventListener('keydown', (e) => {
  if (e.code === 'Numpad7') pattern.value[0] = !pattern.value[0];
  if (e.code === 'Numpad8') pattern.value[1] = !pattern.value[1];
  if (e.code === 'Numpad9') pattern.value[2] = !pattern.value[2];
  if (e.code === 'Numpad4') pattern.value[3] = !pattern.value[3];
  if (e.code === 'Numpad6') pattern.value[4] = !pattern.value[4];
  if (e.code === 'Numpad1') pattern.value[5] = !pattern.value[5];
  if (e.code === 'Numpad2') pattern.value[6] = !pattern.value[6];
  if (e.code === 'Numpad3') pattern.value[7] = !pattern.value[7];
  if (e.key === 'Enter') submitPattern(e)
});
</script>

<style lang="scss">
.cipher-wrapper-wrapper {
  padding: 20px;
  width: 292px;
  display: flex;
  justify-content: center;
  margin: 0 auto 20px;
  border: 4px solid var(--selected-color-highlight);

  &+button {
    margin-right: 20px;
  }

  &~button {
    background-color: var(--selected-color-black);
  }

  &~button+p {
    color: var(--selected-color-black);
    margin-bottom: 20px;
  }
}

.cipher-wrapper {
  width: 228px;
  display: flex;
  justify-content: center;
  margin: 0 auto;
  border-top: 14px solid var(--selected-color-black);
  border-right: 14px solid white;
  border-bottom: 14px solid white;
  border-left: 14px solid var(--selected-color-black);
  padding: 4px;

  @media only screen and (min-width: 600px) {
    width: 246px;
  }
}

.cipher {
  row-gap: 24px;

  @media only screen and (min-width: 600px) {
    row-gap: 32px;
  }
}

.cipher-row {
  column-gap: 24px;
  position: relative;

  @media only screen and (min-width: 600px) {
    column-gap: 32px;
  }

  input {
    position: absolute;
    display: none;

    &:nth-of-type(2) {
      left: 80px;
    }

    &:nth-of-type(3) {
      left: 160px;
    }
  }

  .cipher-hollow+input {
    left: 160px;
  }
}

.cipher-input,
.cipher-hollow {
  width: 48px;
  height: 48px;
}

.cipher-input {
  cursor: pointer;
  background: var(--selected-color-black);
  transition: 200ms;
  display: flex;
  justify-content: center;
  align-items: center;
  letter-spacing: normal !important;

  input:checked+& {
    background: white;
    color: var(--selected-color-black);

  }
}

.cipher-hollow {
  font-size: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, Helvetica, sans-serif;
  color: red;
  opacity: 0;
  transition: 200ms;

  &.wrong {
    opacity: 1;
  }
}

section.cipher-textarea-wrapper {
  position: relative;

  &:first-of-type span {
    font-size: 10px;
  }

  span {
    position: absolute;
    top: 6px;
    left: 6px;
    font-size: 14px;
  }
}

.cipher-textarea {
  font-size: 32px !important;
}

.decipher-textarea {
  font-size: 48px !important;
}

.cipher-textarea,
.decipher-textarea {
  background-color: var(--selected-color-black);
  padding: 20px;
  color: white;
  width: 100%;

}
</style>
