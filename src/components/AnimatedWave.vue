<template>
  <div class="wave-container">
    <div class="wave wave1" :style="{ background: waveColor }"></div>
    <div class="wave wave2" :style="{ background: waveColor }"></div>
    <div class="wave wave3" :style="{ background: waveColor }"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      waveColor: 'rgba(0, 247, 255, 0.1)'
    }
  },
  mounted() {
    this.animateWaves()
  },
  methods: {
    animateWaves() {
      if (window.gsap) {
        gsap.to('.wave1', {
          duration: 15,
          x: '-100%',
          repeat: -1,
          ease: 'none'
        })
        
        gsap.to('.wave2', {
          duration: 12,
          x: '100%',
          repeat: -1,
          ease: 'none'
        })
        
        gsap.to('.wave3', {
          duration: 18,
          x: '-150%',
          repeat: -1,
          ease: 'none'
        })
      }
    }
  }
}
</script>

<style scoped>
.wave-container {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 15vh;
  overflow: hidden;
  z-index: 1;
  opacity: 0.7;
}

.wave {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 200%;
  height: 100%;
  background: rgba(0, 247, 255, 0.1);
  border-radius: 50% 50% 0 0;
}

.wave1 {
  animation: wave 15s linear infinite;
  height: 120%;
  opacity: 0.7;
  background: linear-gradient(90deg, transparent, rgba(0, 247, 255, 0.2), transparent);
}

.wave2 {
  animation: wave 12s linear infinite;
  height: 100%;
  opacity: 0.5;
  animation-delay: -5s;
  bottom: 5px;
}

.wave3 {
  animation: wave 18s linear infinite;
  height: 80%;
  opacity: 0.3;
  animation-delay: -2s;
  bottom: 10px;
}

@keyframes wave {
  0% {
    transform: translateX(0) translateZ(0) scaleY(1);
  }
  50% {
    transform: translateX(-25%) translateZ(0) scaleY(0.8);
  }
  100% {
    transform: translateX(-50%) translateZ(0) scaleY(1);
  }
}
</style>