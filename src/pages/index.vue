<template>
  <div class="px-5 py-5 flex flex-col">
    <div class="flex flex-col">
      <span class="text-lg text-orange-500">Upload a template</span>
      <file-uploader @upload="setTemplate" />
    </div>
    <div v-if="templateImg">
      <image-marker
        :image="templateImg"
        name="templateImage"
        @update-markers="updateTemplateMarkers"
        :state="templateMarkers"
      />
    </div>
  </div>
  <markers-panel :markers="templateMarkers?.markers" />
</template>

<script setup lang="ts">
import * as markerjs2 from 'markerjs2'
const templateImg = ref('')
const templateMarkers = ref<markerjs2.MarkerAreaState>()
const setTemplate = (files: FileList) => {
  templateImg.value = URL.createObjectURL(files[0])
}
const updateTemplateMarkers = (markers: markerjs2.MarkerAreaState) => {
  templateMarkers.value = markers
  console.log(templateMarkers.value)
}
</script>

<style scoped></style>
