<template>
  <div class="mt-10">
    <img ref="imgRef" :src="image" :alt="name" />
  </div>
</template>

<script setup lang="ts">
import * as markerjs2 from 'markerjs2'
import { PropType } from 'vue'
import { marker } from '~/composables/marker'

const props = defineProps({
  image: {
    type: String,
    required: true,
  },
  name: {
    type: String,
    default: 'default',
  },
  state: {
    type: Object as PropType<markerjs2.MarkerAreaState>,
    default: () => {},
  },
})
const emits = defineEmits(['update-markers'])
const imgRef = ref()
onMounted(() => {
  initMarker()
})

const initMarker = () => {
  marker.value = new markerjs2.MarkerArea(imgRef.value)
  marker.value.addRenderEventListener((dataUrl, state) => {
    imgRef.value.src = dataUrl
    emits('update-markers', state)
  })
  if (props.state && Object.keys(props.state).length > 0) {
    marker.value.restoreState(props.state)
  }
  marker.value.availableMarkerTypes = [markerjs2.FrameMarker]
}
watch(
  () => props.image,
  () => {
    initMarker()
  }
)
</script>
