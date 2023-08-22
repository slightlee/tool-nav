<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const jsonData = ref('');
const formattedJson = ref('');

const removeEscapes = (): void => {
  formattedJson.value = jsonData.value.replace(/\\(.)/g, '$1');
};

const formatJson = (): void => {
  try {
    const parsedJson = JSON.parse(jsonData.value);
    formattedJson.value = JSON.stringify(parsedJson, null, 2);
  } catch (error) {
    console.error('无效的 JSON 数据');
    formattedJson.value = '';
  }
};

</script>

<template>
  <div class="container">
    <div class="left-pane">
      <!-- <h1>{{ msg }}</h1> -->
      <textarea v-model="jsonData" rows="30" cols="50"></textarea>
    </div>
    <div class="right-pane">
      <textarea v-model="formattedJson" rows="30" cols="50" readonly></textarea>
    </div>
  </div>
  <br/>
  <div class="bottom-pane">
      <button @click="removeEscapes">去除转义字符</button>
      <button @click="formatJson">格式化</button>
    </div>
</template>

<style scoped>
.container {
  display: flex;
}

.left-pane {
  margin-right: 10px;
}

.right-pane {
  flex-shrink: 0;
}
</style>
