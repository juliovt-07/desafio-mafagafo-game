<template>
  <div class="bg-gradient-to-b from-indigo-700 to-indigo-500 min-h-screen px-10 py-5">
    <header class="flex flex-col sm:flex-row justify-between items-center max-w-7xl mx-auto">
      <h1 class="cursor-pointer animate__animated animate__bounce animate__delay-4s">
        <img src="/logo.png" alt="logo" width="250">
      </h1>
      <div
        class="hidden sm:block border border-white-100 px-8 py-3 text-white rounded-3xl cursor-pointer hover:bg-white hover:text-indigo-600 ease-in duration-200"
      >
        Site Oficial
      </div>
    </header>
    <div class="flex flex-col items-center justify-center gap-10 md:gap-20 mt-20 md:mt-40 md:flex-row">
      <div class="time text-gray-300">
        <p class="text-4xl mb-4 text-left">Restam</p>
        <p class="text-7xl text-center min-w-72 border border-white-100 p-4 rounded-md animate__animated animate__pulse animate__infinite animate__slow">
          <span v-show="(duration.hours + 24*duration.days) > 0">{{ duration.hours + 24*duration.days }}:</span>{{ duration.minutes }}:{{ duration.seconds }}
        </p>
        <p class="text-4xl mt-4 text-right">
          {{ (duration.hours + 24*duration.days) == 0 ? 'Minutos' : 'Horas' }}
        </p>
      </div>
      <div>
        <img src="/mafa-1.png" alt="mafa 1" width="500">
      </div>
    </div>
  </div>
</template>

<script>
import 'animate.css'
import moment from 'moment'

export default {
  name: 'IndexPage',
  data() {
    return {
      duration: {}
    }
  },
  mounted() {
    var evento  = new Date(2022, 1, 17)
      , atual   = new Date().getTime()
      , duracao = moment.duration(evento - atual, 'milliseconds')
    
    this.duration = duracao._data

    setInterval(() => {
      duracao = moment.duration(duracao - 1000, 'milliseconds')
      this.duration = duracao._data
    }, 1000)
  }
}
</script>
