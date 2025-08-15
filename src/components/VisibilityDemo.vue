<template>
  <section class="section">
    <h2>🎪 v-show vs v-if демонстрация</h2>
    <div class="controls">
      <button @click="showWithIf = !showWithIf">v-if: {{ showWithIf ? 'Скрыть' : 'Показать' }}</button>
      <button @click="showWithShow = !showWithShow">v-show: {{ showWithShow ? 'Скрыть' : 'Показать' }}</button>
    </div>

    <div style="margin-top: 15px;">
      <div v-if="showWithIf" class="demo-box green">
        <strong>v-if элемент:</strong> Полностью удаляется из DOM
      </div>
      <div v-show="showWithShow" class="demo-box yellow">
        <strong>v-show элемент:</strong> Скрывается через CSS display: none
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
const showWithIf = ref(true)
const showWithShow = ref(true)
</script>

<style scoped>
.demo-box {
  padding: 15px;
  border-radius: 5px;
  margin: 5px 0;
}
.green {
  background: #d5e8d4;
}
.yellow {
  background: #ffe0b3;
}
</style>