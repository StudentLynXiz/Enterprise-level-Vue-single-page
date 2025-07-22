<template>
  <div id="app">
    <ParticleBackground :config="particleConfig" />
    <AnimatedWave />
    <div class="content">
      <HolographicHeader title="ENTERPRISE X" subtitle="Next-Gen Business Intelligence" />
      <div class="dashboard-container">
        <InteractiveDashboard />
        <div class="card-grid">
          <GlowingCard v-for="(card, i) in cards" :key="i" :data="card" />
        </div>
      </div>
      <div class="cyber-footer">
        <div class="cyber-line"></div>
        <p>© 2025 ENTERPRISE X | SECURE CLOUD PLATFORM</p>
      </div>
    </div>
  </div>
</template>

<script>
import ParticleBackground from './components/ParticleBackground.vue'
import HolographicHeader from './components/HolographicHeader.vue'
import InteractiveDashboard from './components/InteractiveDashboard.vue'
import GlowingCard from './components/GlowingCard.vue'
import AnimatedWave from './components/AnimatedWave.vue'
import particleConfig from '@/assets/particle-config.json'

export default {
  components: {
    ParticleBackground,
    HolographicHeader,
    InteractiveDashboard,
    GlowingCard,
    AnimatedWave
  },
  data() {
    return {
      particleConfig,
      cards: [
        { 
          title: 'Real-Time Analytics', 
          value: '24.7K', 
          icon: '📊',
          color: '#ff7eb9',
          description: 'Live data processing across global nodes'
        },
        {
          title: 'Global Coverage', 
          value: '98%', 
          icon: '🌐',
          color: '#7afcff',
          description: 'Servers in 12 regions worldwide'
        },
        {
          title: 'Secure Transactions', 
          value: '100%', 
          icon: '🔒',
          color: '#ff65a3',
          description: 'Military-grade encryption protocols'
        },
        {
          title: 'AI Predictions', 
          value: '96.3%', 
          icon: '🤖',
          color: '#9d4edd',
          description: 'Machine learning accuracy rating'
        }
      ]
    }
  },
  mounted() {
    this.animateEntrance()
  },
  methods: {
    animateEntrance() {
      if (window.gsap) {
        gsap.from('.card-grid > *', {
          duration: 1,
          opacity: 0,
          y: 50,
          stagger: 0.2,
          ease: "back.out(1.7)"
        })
        
        gsap.from('.dashboard-container', {
          duration: 1.5,
          opacity: 0,
          y: 30,
          delay: 0.3,
          ease: "power3.out"
        })
      }
    }
  }
}
</script>

<style>
#app {
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

.content {
  position: relative;
  z-index: 10;
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}

.dashboard-container {
  margin-top: 3rem;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 30px;
  margin-top: 50px;
}

.cyber-footer {
  margin-top: 5rem;
  text-align: center;
  padding: 2rem 0;
  position: relative;
}

.cyber-line {
  height: 2px;
  background: linear-gradient(90deg, transparent, #00f7ff, transparent);
  margin-bottom: 1.5rem;
  position: relative;
}

.cyber-line::before,
.cyber-line::after {
  content: '';
  position: absolute;
  width: 15px;
  height: 15px;
  border: 2px solid #00f7ff;
  top: 50%;
  transform: translateY(-50%) rotate(45deg);
}

.cyber-line::before {
  left: 0;
}

.cyber-line::after {
  right: 0;
}

.cyber-footer p {
  font-size: 0.9rem;
  letter-spacing: 2px;
  color: rgba(255, 255, 255, 0.6);
  font-family: 'Orbitron', sans-serif;
}

@media (max-width: 768px) {
  .content {
    padding: 1rem;
  }
  
  .card-grid {
    grid-template-columns: 1fr;
  }
}
</style>