<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import type { Ref } from 'vue'

type geoLocation = {
  latitude: number
  longitude: number
}

const coords: Ref<geoLocation | undefined> = ref()
const geoLocationBlockedByUser: Ref<boolean> = ref(false)

const getGeoLocation = async (): Promise<void> => {
  await navigator.geolocation.getCurrentPosition(
    async (position: { coords: geoLocation }) => {
      coords.value = position.coords
    },
    (error: { message: string }) => {
      geoLocationBlockedByUser.value = true
      console.error(error)
    },
  )
}

onMounted(async () => {
  await getGeoLocation()
})
</script>

<template>
  <div v-if="coords && !geoLocationBlockedByUser">{{ coords.latitude }} {{ coords.longitude }}</div>
  <div v-if="geoLocationBlockedByUser">
    Geolocation is blocked by user. Please allow geolocation access in your browser settings.
  </div>
</template>
