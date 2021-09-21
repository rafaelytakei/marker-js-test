<template>
  <div class="absolute top-10 right-10 flex flex-col">
    Controls
    <button @click="marker?.show">Add new marker</button>
    <button @click="marker?.createNewMarker(markerjs2.FrameMarker)">
      New marker
    </button>
    <div class="flex flex-col">
      <div
        v-for="(item, i) in markers"
        class="border-1 border-blue-400 px-5 my-3 flex flex-col"
        @click="setActiveMarker(i)"
      >
        <span> Name: {{ markerNames[i] || `Rectangle ${i + 1}` }} </span>
        <span> Top: {{ item.top }} </span>
        <span> Left: {{ item.left }} </span>
        <span> Width: {{ item.width }} </span>
        <span> Height: {{ item.height }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { marker, markerNames } from '~/composables/marker'
import * as markerjs2 from 'markerjs2'
import { PropType } from 'vue'
const props = defineProps({
  markers: {
    type: Object as PropType<Array<markerjs2.RectangleMarkerState>>,
    default: () => {},
  },
})
const setActiveMarker = (i: number) => {
  // marker.value.
  console.log(props.markers[i])
  // marker.value?.setCurrentMarker(props.markers[i])
}
</script>
