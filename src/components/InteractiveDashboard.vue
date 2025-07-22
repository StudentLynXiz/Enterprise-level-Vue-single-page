<template>
  <div class="dashboard">
    <div class="dashboard-title">BUSINESS PERFORMANCE DASHBOARD</div>
    <div class="dashboard-content">
      <div class="metrics-grid">
        <div class="metric" v-for="(metric, index) in metrics" :key="index">
          <div class="metric-title">{{ metric.title }}</div>
          <div class="metric-value">{{ metric.value }}</div>
          <div class="metric-trend" :class="metric.trendClass">
            {{ metric.trend }}
          </div>
        </div>
      </div>
      <div class="chart-container">
        <div class="chart" ref="chart"></div>
        <div class="chart-info">
          <div class="info-item">
            <div class="info-label">REAL-TIME UPTIME</div>
            <div class="info-value">99.98%</div>
          </div>
          <div class="info-item">
            <div class="info-label">ACTIVE USERS</div>
            <div class="info-value">24.7K</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      metrics: [
        { title: 'REVENUE', value: '$2.4M', trend: '+12.4%', trendClass: 'positive' },
        { title: 'CONVERSION', value: '4.7%', trend: '+3.1%', trendClass: 'positive' },
        { title: 'ENGAGEMENT', value: '78.2%', trend: '+5.3%', trendClass: 'positive' },
        { title: 'CHURN RATE', value: '2.1%', trend: '-0.8%', trendClass: 'negative' }
      ]
    }
  },
  mounted() {
    this.renderChart()
  },
  methods: {
    renderChart() {
      const chart = this.$refs.chart
      if (!chart) return
      
      // 创建虚拟图表 - 实际项目中替换为ECharts或Chart.js
      chart.innerHTML = `
        <div class="chart-visual">
          <div class="chart-line" style="height: 80%; animation-delay: 0s"></div>
          <div class="chart-line" style="height: 65%; animation-delay: 0.2s"></div>
          <div class="chart-line" style="height: 90%; animation-delay: 0.4s"></div>
          <div class="chart-line" style="height: 50%; animation-delay: 0.6s"></div>
          <div class="chart-line" style="height: 75%; animation-delay: 0.8s"></div>
          <div class="chart-line" style="height: 85%; animation-delay: 1s"></div>
          <div class="chart-line" style="height: 95%; animation-delay: 1.2s"></div>
        </div>
        <div class="chart-labels">
          <span>MON</span>
          <span>TUE</span>
          <span>WED</span>
          <span>THU</span>
          <span>FRI</span>
          <span>SAT</span>
          <span>SUN</span>
        </div>
      `
    }
  }
}
</script>

<style scoped>
.dashboard {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 25px;
  padding: 2.5rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(15px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  position: relative;
}

.dashboard::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: linear-gradient(90deg, #ff00cc, #3333ff, #00ccff);
  background-size: 200% 200%;
  animation: gradientFlow 3s ease infinite;
}

.dashboard-title {
  font-size: 1.3rem;
  margin-bottom: 2rem;
  text-align: center;
  color: rgba(255, 255, 255, 0.9);
  letter-spacing: 2px;
  font-weight: 500;
  position: relative;
  padding-bottom: 1rem;
}

.dashboard-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 2px;
  background: linear-gradient(90deg, transparent, #00f7ff, transparent);
}

.metrics-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 25px;
  margin-bottom: 3rem;
}

.metric {
  background: rgba(0, 0, 0, 0.2);
  border-radius: 15px;
  padding: 1.5rem;
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.3s ease;
}

.metric:hover {
  transform: translateY(-5px);
  background: rgba(0, 0, 0, 0.3);
}

.metric-title {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 0.5rem;
  letter-spacing: 1px;
}

.metric-value {
  font-size: 2.2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  background: linear-gradient(to right, #7afcff, #ffffff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.metric-trend {
  font-size: 0.9rem;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  display: inline-block;
}

.metric-trend.positive {
  background: rgba(76, 175, 80, 0.2);
  color: #4CAF50;
}

.metric-trend.negative {
  background: rgba(244, 67, 54, 0.2);
  color: #F44336;
}

.chart-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.chart {
  height: 250px;
  background: rgba(0, 0, 0, 0.15);
  border-radius: 15px;
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  padding: 1.5rem;
  gap: 15px;
}

.chart-visual {
  display: flex;
  align-items: flex-end;
  height: 100%;
  width: 100%;
  gap: 20px;
}

.chart-line {
  width: 100%;
  background: linear-gradient(to top, #00f7ff, #7afcff);
  border-radius: 5px 5px 0 0;
  position: relative;
  animation: chartGrow 1s ease forwards;
  transform-origin: bottom;
  opacity: 0;
}

@keyframes chartGrow {
  from { transform: scaleY(0); opacity: 0; }
  to { transform: scaleY(1); opacity: 1; }
}

.chart-labels {
  display: flex;
  justify-content: space-around;
  padding: 0 1rem;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
}

.chart-info {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.info-item {
  background: rgba(0, 0, 0, 0.2);
  border-radius: 15px;
  padding: 1.5rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.info-label {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 0.5rem;
}

.info-value {
  font-size: 2rem;
  font-weight: 700;
  background: linear-gradient(to right, #ff7eb9, #ff65a3);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

@keyframes gradientFlow {
  0% { background-position: 0% 50% }
  50% { background-position: 100% 50% }
  100% { background-position: 0% 50% }
}

@media (max-width: 768px) {
  .dashboard {
    padding: 1.5rem;
  }
  
  .metrics-grid {
    grid-template-columns: 1fr 1fr;
  }
}
</style>