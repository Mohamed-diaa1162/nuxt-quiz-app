<template>
  <div class="d-flex justify-content-center">
    <div
      v-for="time in times"
      :key="time.id"
      class="time-part text-green"
      :time="times"
    >
      <span class="mx-1 main-text">{{ time.time }}</span>
      <span class="mx-1">{{ time.text }}</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Counter',

  data() {
    return {
      endTime: '',
      times: [
        { id: 1, text: 'Hours', time: 0 },
        { id: 2, text: 'Minutes', time: 0 },
        { id: 3, text: 'Seconds', time: 1 },
      ],
      progress: 100,
      // isActive: false,
      timeInterval: undefined,
      startTime: Date.parse(new Date()),
    }
  },
  created() {
    this.updateTimer()
    setInterval(() => {
      this.updateTimer()
    }, 1000)
  },
  methods: {
    updateTimer() {
      this.endTime = Date.parse(new Date())
      const diff = this.endTime - this.startTime
      const seconds = Math.floor(diff / 1000)
      const minutes = Math.floor(seconds / 60)
      const hours = Math.floor(minutes / 60)
      this.times[0].time = hours
      this.times[1].time = minutes - hours * 60
      this.times[2].time = seconds - minutes * 60
      this.progress = (seconds / 3600) * 100
    },
  },
}
</script>
<style lang="scss" scoped>
.time-part {
  display: flex;
  position: relative;
}
</style>
