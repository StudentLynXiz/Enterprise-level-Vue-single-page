<template>
  <div class="header">
    <h1 class="holographic" ref="hologram">{{ title }}</h1>
    <h2 class="subtitle">{{ subtitle }}</h2>
    <div class="scan-line"></div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    subtitle: String
  },
  mounted() {
    this.addHologramEffect()
  },
  methods: {
    addHologramEffect() {
      if (window.gsap) {
        gsap.to('.scan-line', {
          duration: 4,
          y: '100%',
          repeat: -1,
          ease: 'none'
        })
        
        gsap.from('.holographic', {
          duration: 1.5,
          opacity: 0,
          y: -30,
          ease: "elastic.out(1, 0.3)"
        })
        
        gsap.to('.holographic', {
          duration: 6,
          textShadow: '0 0 10px #00f7ff, 0 0 20px #00f7ff, 0 0 30px #00f7ff',
          repeat: -1,
          yoyo: true,
          ease: "sine.inOut"
        })
      }
    }
  }
}
</script>

<style scoped>
.header {
  text-align: center;
  padding: 3rem 0 4rem;
  position: relative;
  overflow: hidden;
}

.holographic {
  font-size: 4.5rem;
  background: linear-gradient(45deg, 
    #ff00cc, #3333ff, #00ccff, #ff00cc,
    #ff00cc, #3333ff, #00ccff, #ff00cc);
  background-size: 400% 400%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: hologram 8s ease infinite;
  text-shadow: 0 0 15px rgba(0, 247, 255, 0.5);
  position: relative;
  font-family: 'Orbitron', sans-serif;
  font-weight: 700;
  letter-spacing: 3px;
  margin-bottom: 1rem;
}

.subtitle {
  font-size: 1.5rem;
  color: rgba(255, 255, 255, 0.8);
  letter-spacing: 4px;
  text-transform: uppercase;
  font-weight: 300;
  position: relative;
  animation: fadeIn 2s ease;
}

.scan-line {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 3px;
  background: linear-gradient(90deg, transparent, rgba(0, 247, 255, 0.8), transparent);
  box-shadow: 0 0 10px rgba(0, 247, 255, 0.5);
}

@keyframes hologram {
  0% { 
    background-position: 0% 50%;
    text-shadow: 0 0 10px #00f7ff, 0 0 20px #00f7ff; 
  }
  50% { 
    background-position: 100% 50%;
    text-shadow: 0 0 20px #ff00cc, 0 0 30px #ff00cc; 
  }
  100% { 
    background-position: 0% 50%;
    text-shadow: 0 0 10px #00ccff, 0 0 20px #00ccff; 
  }
}

@keyframes fadeIn {
  from { 
    opacity: 0;
    transform: translateY(20px);
  }
  to { 
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .holographic {
    font-size: 2.5rem;
  }
  
  .subtitle {
    font-size: 1rem;
  }
}
</style>