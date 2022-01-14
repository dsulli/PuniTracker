<template>
  <span class="font-bold" :class="timerColorClass">{{timer}}</span>
</template>

<script>
import intervalToDuration from 'date-fns/intervalToDuration'
import differenceInHours from 'date-fns/differenceInHours'

export default {
  props: {
    timeStamp: {
      type: Number,
      required: true,
      default: 1642057629
    },
    type: {
      type: String,
      default: 'A-Rank'
    }
  },
  data () {
    return {
      dateTime: new Date(this.timeStamp * 1000),
      timer: '',
      duration: {}
    }
  },
  computed: {
    timerColorClass () {
      const hourDifference = differenceInHours(
        new Date(),
        this.dateTime
      )
      if (hourDifference < 4) {
        return { 'text-red-400': true }
      } else if (hourDifference > 4 && hourDifference < 6) {
        return { 'text-yellow-500': true }
      } else if (hourDifference >= 6) {
        return { 'text-green-500': true }
      }
      return {}
    }
  },
  created () {
    setInterval(this.updateTimestamp, 1000)
  },
  methods: {
    updateTimestamp () {
      this.duration = intervalToDuration({ start: this.dateTime, end: new Date() })
      this.timer = `${this.duration.hours}:${this.convertToDoubleDigit(this.duration.minutes)}:${this.convertToDoubleDigit(this.duration.seconds)}`
    },
    convertToDoubleDigit (num) {
      if (num < 10) {
        return `0${num}`
      }
      return num
    }
  }
}
</script>
