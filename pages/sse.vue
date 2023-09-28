<template>
  <button @click="createSSE">创建sse</button>
  <button @click="sendMessage">发送数据</button>
</template>
<script setup lang="ts">
let esOne: EventSource;
function createSSE() {
  esOne = new EventSource("http://127.0.0.1:8888/sse/1/sse");
  esOne.onmessage = function (e) {
    console.log("小甲", e.data);
  };
}

async function sendMessage(){
  const { data, pending, error, refresh } = await useFetch('http://127.0.0.1:8888/sse/addCart/1', {
    method: 'POST',
    body: { name: '小甲' }
})
}

onBeforeUnmount(() => {
  console.log("onBeforeUnmount");
  esOne.close();
});
</script>
<style></style>
