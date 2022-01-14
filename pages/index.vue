<template>
  <div class=" mx-auto  ">
    <div class="w-full md:px-12 px-6 py-4 bg-purple-400 text-gray-900 font-extrabold tracking-tighter">
        <h2 class="text-4xl ">
          <TrainIcon class="h-6 mr-2" color="#1f2937"/>
          Hunt Train Tracker
        </h2>
    </div>
    <div class="md:px-12 px-6 py-6">
    <div class="grid xl:grid-cols-3 lg:grid-cols-2 md:grid-cols-1 sm:grid-cols-1 gap-4">
    <div v-for="(expac, index) in huntMarksJson['A-Ranks']" :key="index" class="bg-gray-900 py-4 px-6 rounded-xl">
      <h3 class="text-2xl mb-4 uppercase tracking-widest text-purple-400">
        <SparkleIcon class="h-4"/>
        {{ expac.name }}
        <span v-if="expac.instance">
          Instance {{ expac.instance }}
        </span>
      </h3>
      <table class="table-auto border-collapse w-full">
        <tr class="text-left font-medium tracking-wide uppercase text-gray-400 rounded">
          <th class="py-1 pr-4 border-b-2 border-gray-700">Name</th>
          <th class="py-1 pr-4 border-b-2 border-gray-700">Zone</th>
          <th class="py-1 pr-4 border-b-2 border-gray-700">Timer</th>
          <th class="py-1 border-b-2 border-gray-700"> </th>
        </tr>
        <tr v-for="(mark, index) in expac.marks" :key="index" class="">
          <td class="py-2 pr-4 border-b border-gray-800 leading-tight">
            <div class="text-gray-300 font-semibold mb-0">{{ mark.name }}</div>
            <div class="text-sm text-gray-500">{{ mark.altName }}</div>
          </td>
          <td class="py-1 pr-4 border-b border-gray-800">
            {{ mark.zone }}
          </td>
          <td class="py-1 pr-4 border-b border-gray-800">
            <MarkTimer :time-stamp="mark.lastKilled" />
          </td>
          <td class="py-1 border-b border-gray-800">
            <button class=" text-xs tracking-wider uppercase py-1 px-4 border rounded-full border-purple-400 text-gray-300 hover:bg-purple-400 hover:text-gray-900 font-bold outline-none">Mark Dead</button>
          </td>
        </tr>
      </table>
    </div>
    </div>
    </div>
  </div>
</template>
<style>
body {
  @apply bg-gray-800 text-gray-200;
}
</style>
<script>
import MarkTimer from '../components/MarkTimer.vue'
import SparkleIcon from '../components/SparkleIcon.vue'
import TrainIcon from '../components/TrainIcon.vue'
import huntMarks from '../static/huntMarks.json'
export default {
  target: 'static',
  name: 'IndexPage',
  components: {
    MarkTimer,
    SparkleIcon,
    TrainIcon
  },
  data () {
    return {
      huntMarksJson: huntMarks
    }
  }
}
</script>
