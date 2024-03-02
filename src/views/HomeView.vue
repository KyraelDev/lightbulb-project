<template>
  <div 
    @mouseover="toggleHover(true)"
    @mouseleave="toggleHover(false)"
    v-show="!lampadinaCliccata"
    class="custom-cursor w-[100vw] flex justify-center items-center">
    <img 
      @click="toggleLampadina"
      :class="{ 'animatelampadina': lampadinaHover }"
      class="lampadina" 
      src="../assets/imgs/omori-lightbulb.gif"
    >
  </div>

  <div 
    v-show="lampadinaCliccata"
    class="schermo-nero testo-omori-game2">
    <p class="text-6xl mb-6">Why did you turn the light off?</p>
    <button @click="toggleLampadina" class="btn-riaccendi rounded-full p-4 hover:scale-105 transition-transform">I'm afraid of the dark... Please bring me to light.</button>
  </div>

  <audio ref="audio" loop>
    <source src="../assets/sounds/04.SpacesIn-between.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>
</template>

<script>
export default {
  data() {
    return {
      lampadinaCliccata: false,
      lampadinaHover: false,
      audio: null
    };
  },
  mounted() {
    // Ottieni il riferimento all'elemento audio
    this.audio = this.$refs.audio;
    
    // Imposta il volume al 3%
    this.audio.volume = 0.03;
    
    // Avvia la riproduzione dell'audio dopo un ritardo di 2 secondi
    setTimeout(() => {
      this.avviaRiproduzioneAudio();
    }, 2000);
  },
  methods: {
    toggleLampadina() {
      this.lampadinaCliccata = !this.lampadinaCliccata;
    },
    toggleHover(value) {
      this.lampadinaHover = value;
    },
    avviaRiproduzioneAudio() {
      // Avvia la riproduzione dell'audio solo se il browser lo consente
      if (this.audio) {
        this.audio.play().catch(error => {
          console.error("Impossibile avviare la riproduzione dell'audio:", error);
        });
      }
    }
  }
}
</script>

<style scoped>
.animatelampadina {
  cursor: pointer;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.schermo-nero {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: black;
  color: white;
  text-align: center;
  padding-top: 50vh;
}

.btn-riaccendi {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: white;
  color: black;
  border: none;
  cursor: pointer;
}

.custom-cursor {
  cursor: url('../assets/imgs/cursorebase.png'), auto;
}

.testo-omori-game2 {
  font-family: 'OmoriGame2', sans-serif;
}
</style>
