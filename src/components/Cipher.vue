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
  <v-btn @click="submitPattern">
    Clear
  </v-btn>
  <p>(you can use the numpad and enter key on your keyboard)</p>
  <div>
    <textarea class="cipher-textarea" label="Label" v-model="decipher" disabled></textarea>
  </div>
</template>

<script setup>
import { ref } from 'vue'

let pattern = ref([false, false, false,
  false, false,
  false, false, false])

let decipher = ref('')

let validPatern = ref(false)
let validPaternStyle = ref(false)

function submitPattern() {

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'A', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'B', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && pattern.value[7]) decipher.value += 'C', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && !pattern.value[7]) decipher.value += 'D', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'E', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'F', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && pattern.value[7]) decipher.value += 'G', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && !pattern.value[7]) decipher.value += 'H', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'I', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'J', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && pattern.value[7]) decipher.value += 'K', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && !pattern.value[7]) decipher.value += 'L', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'M', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'N', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    !pattern.value[3] && pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && pattern.value[7]) decipher.value += 'O', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && !pattern.value[7]) decipher.value += 'P', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'Q', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'R', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && pattern.value[7]) decipher.value += 'S', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && !pattern.value[7]) decipher.value += 'T', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'U', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'V', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && !pattern.value[4] &&
    pattern.value[5] && pattern.value[6] && pattern.value[7]) decipher.value += 'W', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && !pattern.value[7]) decipher.value += 'X', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && pattern.value[6] && !pattern.value[7]) decipher.value += 'Y', validPatern.value = true

  if (pattern.value[0] && !pattern.value[1] && !pattern.value[2] &&
    pattern.value[3] && pattern.value[4] &&
    !pattern.value[5] && !pattern.value[6] && pattern.value[7]) decipher.value += 'Z', validPatern.value = true



  if (!validPatern.value) {
    console.log(validPatern);
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

.cipher-textarea {
  background-color: var(--selected-color-black);
  padding: 20px;
  color: white;
  width: 100%;
  font-size: 48px !important;
}
</style>
