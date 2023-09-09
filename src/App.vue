<template>
  <v-app>
    <v-main class="">
      <v-container class="fill-height">
        <v-responsive class="align-center text-center">
          <div class="h1-container">
            <h1>Void Stranger <br /> Decipher</h1>
            <h1 class="h1-shadow">Void Stranger <br /> Decipher</h1>
          </div>
          <Cipher />
        </v-responsive>
        <div class="color-container">
          <div class="color-button gray" @click="changeColor('gray')"> </div>
          <div class="color-button red" @click="changeColor('red')"> </div>
          <div class="color-button orange" @click="changeColor('orange')"> </div>
          <div class="color-button yellow" @click="changeColor('yellow')"> </div>
          <div class="color-button green" @click="changeColor('green')"> </div>
          <div class="color-button blue" @click="changeColor('blue')"> </div>
          <div class="color-button lila" @click="changeColor('lila')"> </div>
          <div class="color-button violet" @click="changeColor('violet')"> </div>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import Cipher from '@/components/Cipher.vue'
import { onMounted } from 'vue'

onMounted(() => {
  
  const colorLocalStorage = localStorage.getItem("cipherColor");
  if(colorLocalStorage) {
    changeColor(colorLocalStorage)
  }
})

function changeColor(color) {
  const r = document.querySelector(':root');
  const rs = getComputedStyle(r);
  r.style.setProperty('--selected-color-black',  rs.getPropertyValue(`--${color}-color-black`));
  r.style.setProperty('--selected-color-primary',  rs.getPropertyValue(`--${color}-color-primary`));
  r.style.setProperty('--selected-color-highlight',  rs.getPropertyValue(`--${color}-color-highlight`));
  localStorage.setItem("cipherColor", color);
}
</script>

<style lang="scss">
@font-face {
  font-family: 'Alkhemikal';
  src: url('assets/fonts/Alkhemikal.eot');
  src: url('assets/fonts/Alkhemikal.eot?#iefix') format('embedded-opentype'),
    url('assets/fonts/Alkhemikal.woff2') format('woff2'),
    url('assets/fonts/Alkhemikal.woff') format('woff'),
    url('assets/fonts/Alkhemikal.ttf') format('truetype'),
    url('assets/fonts/Alkhemikal.svg#Alkhemikal') format('svg');
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}

:root {
  --selected-color-black: #000;
  --selected-color-primary: #c0c0c0;
  --selected-color-highlight: #808080;

  --gray-color-black: #000;
  --gray-color-primary: #c0c0c0;
  --gray-color-highlight: #808080;
  
  --red-color-black: #140000;
  --red-color-primary: #f87b57;
  --red-color-highlight: #c20d0d;
  
  --orange-color-black: #120f05;
  --orange-color-primary: #f9a040;
  --orange-color-highlight: #c05a3c;
  
  --yellow-color-black: #0f0f00;
  --yellow-color-primary: #eac300;
  --yellow-color-highlight: #ba779a;
  
  --green-color-black: #001414;
  --green-color-primary: #58dd8b;
  --green-color-highlight: #0c7064;
  
  --blue-color-black: #152b30;
  --blue-color-primary: #64c8fa;
  --blue-color-highlight: #077593;
  
  --lila-color-black: #0d0020;
  --lila-color-primary: #a799cc;
  --lila-color-highlight: #754671;

  --violet-color-black: #05001e;
  --violet-color-primary: #bb81c8;
  --violet-color-highlight: #6531a0;
}

html,
body,
main {
  background-color: var(--selected-color-primary);
  font-family: Alkhemikal;
}

main {
  border-top: 14px solid white;
  border-right: 14px solid var(--selected-color-black);
  border-bottom: 14px solid var(--selected-color-black);
  border-left: 14px solid white;
}

.h1-container {
  position: relative;
}

h1 {
  margin-bottom: 20px;
  color: var(--selected-color-black);
  font-size: 32px;
  position: relative;
  z-index: 1;

  @media only screen and (min-width: 600px) {
    font-size: 48px;
  }

  &.h1-shadow {
    position: absolute;
    top: 0;
    transform: translate(-48.5%,2%);
    left: 50%;
    color: var(--selected-color-highlight);
    z-index: 0;
    display: none;

    @media only screen and (min-width: 600px) {
      display: block;
    }
  }
}

.color-container {
  display: block;
  position: fixed;
  left: 32px;
  top: 32px;
  display: flex;
  column-gap: 16px;
  row-gap: 16px;
  flex-wrap: wrap;
  margin-right: 32px;
  z-index: 5;

  .color-button {
    width: 32px;
    height: 32px;
    border: 4px solid white;
    cursor: pointer;

    &.gray {
      background-color: var(--gray-color-primary);
    }

    &.red {
      background-color: var(--red-color-primary);
    }

    &.orange {
      background-color: var(--orange-color-primary);
    }

    &.yellow {
      background-color: var(--yellow-color-primary);
    }

    &.green {
      background-color: var(--green-color-primary);
    }

    &.blue {
      background-color: var(--blue-color-primary);
    }

    &.lila {
      background-color: var(--blue-color-primary);
    }

    &.violet {
      background-color: var(--violet-color-primary);
    }
  }
}
</style>