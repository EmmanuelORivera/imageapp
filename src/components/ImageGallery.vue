<script setup>
import { defineEmits, defineProps, computed } from 'vue'
const emits = defineEmits(['visibleSnackbar'])
const props = defineProps(['isImageColored'])
const grayScale = computed(() => (props.isImageColored ? '' : '&grayscale'))

const copyOnClipboardUrlImage = async (n) => {
  const url = generateUrlImage(n)
  await navigator.clipboard.writeText(url)

  emits('visibleSnackbar', true)
}

const generateUrlImage = (n) => {
  return `https://picsum.photos/500/300?image=${n * 5 + 10}${grayScale.value}`
}
</script>
<template>
  <v-card class="mx-5 my-2 pa-3">
    <v-row>
      <v-col v-for="n in 200" :key="n" cols="4" sm="3" md="2" lg="1">
        <v-card @click="copyOnClipboardUrlImage(n)">
          <v-img
            :src="generateUrlImage(n)"
            :lazy-src="generateUrlImage(n)"
            aspect-ratio="1"
            cover
          >
            <template v-slot:placeholder>
              <v-row class="fill-height ma-0" align="center" justify="center">
                <v-progress-circular
                  indeterminate
                  color="red-lighten-1"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-card>
      </v-col>
    </v-row>
  </v-card>
</template>
