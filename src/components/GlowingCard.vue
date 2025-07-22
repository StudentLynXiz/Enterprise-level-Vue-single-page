<template>
  <div 
    class="glowing-card"
    :style="{ '--glow-color': data.color }"
    @mousemove="handleMouseMove"
    @mouseleave="resetCard"
    @click="animateClick"
  >
    <div class="card-content">
      <div class="icon">{{ data.icon }}</div>
      <h3>{{ data.title }}</h3>
      <div class="value">{{ data.value }}</div>
      <div class="description">{{ data.description }}</div>
    </div>
    <div class="glow-effect"></div>
    <div class="corner corner-tl"></div>
    <div class="corner corner-tr"></div>
    <div class="corner corner-bl"></div>
    <div class="corner corner-br"></div>
  </div>
</template>

<script>
export default {
  props: {
    data: Object
  },
  methods: {
    handleMouseMove(e) {
      const card = e.currentTarget
      const rect = card.getBoundingClientRect()
      const x = e.clientX - rect.left
      const y = e.clientY - rect.top
      
      card.style.setProperty('--mouse-x', `${x}px`)
      card.style.setProperty('--mouse-y', `${y}px`)
      
      // 动态倾斜效果
      const tiltX = (rect.width / 2 - x) / 20
      const tiltY = (rect.height / 2 - y) / 20
      card.style.transform = `perspective(1000px) rotateX(${tiltY}deg) rotateY(${-tiltX}deg)`
    },
    resetCard(e) {
      const card = e.currentTarget
      card.style.removeProperty('--mouse-x')
      card.style.removeProperty('--mouse-y')
      card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)'
    },
    animateClick(e) {
      const card = e.currentTarget
      card.classList.add('clicked')
      setTimeout(() => card.classList.remove('clicked'), 500)
    }
  }
}
</script>

<style scoped>
.glowing-card {
  position: relative;
  background: rgba(25, 25, 35, 0.7);
  border-radius: 20px;
  padding: 2.5rem 2rem;
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer;
  transform-style: preserve-3d;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  height: 100%;
}

.glowing-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    600px circle at var(--mouse-x, 100px) var(--mouse-y, 100px),
    var(--glow-color),
    transparent 50%
  );
  opacity: 0.15;
  z-index: -1;
  transition: opacity 0.4s ease;
}

.glowing-card:hover {
  transform: translateY(-15px) scale(1.03);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
}

.glowing-card:hover::before {
  opacity: 0.25;
}

.glowing-card.clicked {
  animation: pulse 0.5s ease;
}

.card-content {
  position: relative;
  z-index: 2;
  text-align: center;
  transform: translateZ(50px);
}

h3 {
  font-size: 1.4rem;
  margin-bottom: 0.5rem;
  font-weight: 500;
  letter-spacing: 1px;
}

.icon {
  font-size: 3.5rem;
  margin-bottom: 1.5rem;
  transition: transform 0.3s ease;
}

.glowing-card:hover .icon {
  transform: scale(1.1) translateY(-5px);
}

.value {
  font-size: 3rem;
  font-weight: 700;
  margin: 1rem 0;
  background: linear-gradient(to right, var(--glow-color), #ffffff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  letter-spacing: 1px;
}

.description {
  font-size: 0.95rem;
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.6;
  margin-top: 1.5rem;
}

.glow-effect {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 20px;
  box-shadow: inset 0 0 30px rgba(255, 255, 255, 0.1);
  pointer-events: none;
}

.corner {
  position: absolute;
  width: 15px;
  height: 15px;
  border: 2px solid var(--glow-color);
  opacity: 0.7;
}

.corner-tl {
  top: 10px;
  left: 10px;
  border-right: none;
  border-bottom: none;
}

.corner-tr {
  top: 10px;
  right: 10px;
  border-left: none;
  border-bottom: none;
}

.corner-bl {
  bottom: 10px;
  left: 10px;
  border-right: none;
  border-top: none;
}

.corner-br {
  bottom: 10px;
  right: 10px;
  border-left: none;
  border-top: none;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}
</style>