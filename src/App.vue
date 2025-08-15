<template>
  <div class="app">
    <h1>🎭 Vue.js: Условный рендеринг и списки</h1>
    <UserManager />
    <VisibilityDemo />
  </div>
</template>

<script setup>
import UserManager from './components/UserManager.vue'
import VisibilityDemo from './components/VisibilityDemo.vue'
</script>

<style scoped>
.app {
  background: white;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 20px 40px rgba(0,0,0,0.1);
  max-width: 800px;
  margin: 0 auto;
}
</style>