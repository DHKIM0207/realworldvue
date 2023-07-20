<script setup>
import EventCard from '@/components/EventCard.vue'
import { onMounted, ref } from 'vue'
import EventService from '@/services/EventService.js'

const events = ref(null)

onMounted(() => {
    // 컴포넌트 생성 시 모의 DB에서 이벤트 가져오기
    EventService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.log(error)
    })
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>