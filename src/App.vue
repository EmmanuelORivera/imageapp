<script setup>
import ImageGallery from './components/ImageGallery.vue'
import SideBar from './components/SideBar.vue'
import { ref } from 'vue'

const isImageColored = ref(true)
const isSnackbarVisible = ref(false)

const onSelectOption = (selectedOption) => {
  isImageColored.value = selectedOption
}
const onVisibleSnackbar = (newValue) => {
  isSnackbarVisible.value = newValue
}
</script>
<template>
  <v-app>
    <SideBar @select-option="onSelectOption" />
    <v-main>
      <v-snackbar
        v-model="isSnackbarVisible"
        color="green-lighten-1"
        location="top"
      >
        The url image was copied on the clipboard!!!
      </v-snackbar>

      <ImageGallery
        :isImageColored="isImageColored"
        @visible-snackbar="onVisibleSnackbar"
      />
    </v-main>
  </v-app>
</template>
