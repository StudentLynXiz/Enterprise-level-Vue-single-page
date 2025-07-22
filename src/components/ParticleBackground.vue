<template>
  <div class="particles" ref="particles"></div>
</template>

<script>
export default {
  props: {
    config: Object
  },
  mounted() {
    this.initParticles()
  },
  methods: {
    async initParticles() {
      try {
        const particlesJS = (await import('particles.js')).default
        particlesJS('particles', this.config)
        
        // 添加鼠标交互特效
        window.pJSDom = window.pJSDom || []
        window.addEventListener('mousemove', (e) => {
          if (window.pJSDom[0]?.pJS?.interactivity) {
            window.pJSDom[0].pJS.interactivity.mouse.pos_x = e.clientX
            window.pJSDom[0].pJS.interactivity.mouse.pos_y = e.clientY
          }
        })
      } catch (error) {
        console.error('Particles.js loading failed:', error)
      }
    }
  }
}
</script>

<style scoped>
.particles {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 0;
  background: linear-gradient(135deg, #0f0c29 0%, #302b63 50%, #24243e 100%);
}
</style>