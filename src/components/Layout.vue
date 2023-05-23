Skip to content
Sign up
platzi
/
practico-vue
Public
Code
Issues
Pull requests
Actions
Projects
Security
Insights
practico-vue/src/components/Layout.vue
@nerddiana
nerddiana Resume
 History
 1 contributor
74 lines (66 sloc)  1.19 KB
<template>
<div class="header">
    <slot name="header"></slot>
</div>
<div class="resume">
    <slot name="resume"></slot>
</div>
<div class="movements">
    <div class="head" @click="showMovimientos = !showMovimientos">
        <div class="grip"></div>
    </div>
    <div class="body" v-show="showMovimientos">
        <slot name="movements"></slot>
    </div>
</div>
</template>

<script setup>
import { ref } from "vue";
const showMovimientos = ref(false);
</script>

<style scoped>
.header,
.resume,
.movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 14px 0;
  box-sizing: border-box;
}
.header {
  position: fixed;
  width: 100vw;
}
.resume {
  min-height: 100vh;
}
.movements {
  z-index: 1;
  position: absolute;
  flex-direction: column;
  bottom: 0;
  width: 100vw;
  background-color: white;
  box-shadow: 0 -8px 16px #e5e5e5;
  border-radius: 24px;
}
.movements .head {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 24px;
  width: 100%;
  box-sizing: border-box;
}
.movements .body {
  height: 75vh;
  width: 100%;
}
.movements .head .grip {
  width: 120px;
  height: 8px;
  background-color: #e5e5e5;
  border-radius: 4px;
}
</style>
Footer
© 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
practico-vue/Layout.vue at 10-add-movement · platzi/practico-vue · GitHub