<template>
  <file-upload ref="upload" v-model="files" @update:model-value="test" @input-file="inputFile"> 上传文件 </file-upload>
  <ul>
    <li v-for="file,index in files" :key="file.name">
      {{ file.name }} - Error: {{ file.error }}, Success: {{ file.success }}
    </li>
  </ul>
</template>
<script setup lang="ts">
import FileUpload, { VueUploadItem } from "vue-upload-component";
const files = ref<VueUploadItem[]>([]);
console.log("files", files);
let filesR = reactive([])
console.log("filesR", filesR)
function inputFile(newFile: VueUploadItem | undefined, oldFile: VueUploadItem | undefined) {
  if (newFile && oldFile && !newFile.active && oldFile.active) {
    // 获得相应数据
    console.log("response", newFile.response);
    if (newFile.xhr) {
      //  获得响应状态码
      console.log("status", newFile.xhr.status);
    }
  }
}

watch(files, (newFiles, oldFiles) => {
  console.log("files", newFiles);
  console.log("oldFiles", oldFiles);
});
</script>
<style></style>
