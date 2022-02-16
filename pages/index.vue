<template>
  <div class="bg-gradient-to-b from-indigo-700 to-indigo-500 min-h-screen px-10 pt-5 relative">
    <canvas v-show="finish" id="my-canvas" class="absolute top-0"></canvas>
    <header class="flex flex-col sm:flex-row justify-between items-center max-w-7xl mx-auto">
      <a href="https://mafagafo.com/" class="cursor-pointer">      
        <h1 class="animate__animated animate__bounce animate__delay-4s">
          <img src="/logo.png" alt="logo" width="250">
        </h1>
      </a>
      <a href="https://mafagafo.com/" class="cursor-pointer">
        <div
          class="hidden sm:block border border-white-100 px-8 py-3 text-white rounded-3xl hover:bg-white hover:text-indigo-600 ease-in duration-200"
        >
          Site Oficial
        </div>
      </a>
    </header>

    <div class="mt-10 md:mt-20 text-center text-white">
      <h2 class="font-semibold text-3xl">
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. <br>
        Ipsam voluptatum repudiandae.
      </h2>
      <h6 class="text-2xl mt-5">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. <br>
        Commodi repellat voluptates quas rem minima
      </h6>
    </div>

    <div class="flex flex-col items-center justify-center gap-10 md:gap-20 mt-20 md:flex-row">
      <div v-if="!finish" class="time text-gray-300">
        <p v-show="!loading" class="text-4xl mb-4 text-left">Restam</p>
        <div v-if="loading" class="loading"/>
        <p v-else class="text-7xl text-center min-w-72 border border-white-100 p-4 rounded-md animate__animated animate__pulse animate__infinite animate__slow">
          <span v-show="(duration.hours + 24*duration.days) > 0"><span v-show="(duration.hours + 24*duration.days) < 10">0</span>{{ duration.hours + 24*duration.days }}:</span><span v-show="duration.minutes < 10">0</span>{{ duration.minutes }}:<span v-show="duration.seconds < 10">0</span>{{ duration.seconds }}
        </p>
        <p v-show="!loading" class="text-4xl mt-4 text-right">
          {{ (duration.hours + 24*duration.days) == 0 ? 'Minutos' : 'Horas' }}
        </p>
      </div>
      <div>
        <img src="/mafa-1.png" alt="mafa 1" width="400" style="max-width: 370px;">
      </div>
    </div>

    <div class="mx-auto text-center text-white mt-20">
      <h6 class="text-xl">
        Lorem ipsum dolor sit amet consectetur adipisicing elit.
      </h6>
    </div>
    <div class="mx-auto w-min flex justify-center items-center mt-5 rounded-lg border border-l-0">
      <input type="email" placeholder="mafauser@mafamail.com" v-model="email" class="py-3 px-3 rounded-l-lg outline-none text-gray-600 font-semibold">
      <div @click="clear()" class="text-white w-max px-3 py-2 text-lg font-semibold cursor-pointer opacity-50 hover:opacity-100 hover:bg-indigo-600 rounded-r-lg ease-in duration-200">
        Notificar-me
      </div>
    </div>
  </div>
</template>

<script>
import 'animate.css'
import moment from 'moment'
import ConfettiGenerator from 'confetti-js'

export default {
  name: 'IndexPage',
  data() {
    return {
      duration: {},
      loading: true,
      finish: false,
      email: ''
    }
  },
  mounted() {
    var confettiElement = document.getElementById('my-canvas');
    var confettiSettings = { target: confettiElement };
    var confetti = new ConfettiGenerator(confettiSettings);
    confetti.render();

    var evento  = new Date(2022, 1, 18)
      , atual   = new Date().getTime()
      , duracao = moment.duration(evento - atual, 'milliseconds')
    
    this.duration = duracao._data

    setInterval(() => {
      duracao = moment.duration(duracao - 1000, 'milliseconds')
      this.duration = duracao._data
      if (this.duration.minutes <= 0 && this.duration.seconds <= 0 && this.duration.hours <=0 && this.duration.days <= 0) {
        this.finish = true
      }
    }, 1000)

    setTimeout(() => {
      this.loading = false
    }, 5000)
  },
  methods: {
    clear() {
      this.email = ''
    }
  }
}
</script>

<style>
.loading {
  border: 3px solid hsla(0, 0%, 81%, 0.2);
  border-top-color: #f0f0f0;
  border-radius: 50%;
  width: 3em;
  height: 3em;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}
</style>