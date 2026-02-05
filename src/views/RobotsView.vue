<script setup lang="ts">
import { ref } from 'vue'

const withBase = (path: string) => `${import.meta.env.BASE_URL}${path.replace(/^\//, '')}`

const robots = ref([
  { 
    id: 1, 
    name: 'HERO | 英雄', 
    type: 'Destroy Turret', 
    img: withBase('imgs/robots/1%E5%8F%B7%E8%8B%B1%E9%9B%84.webp'), 
    features: ['高伤害', '远程吊射', '建筑摧毁']
  },
  { 
    id: 2, 
    name: 'INFANTRY | 步兵', 
    type: 'Main Assault', 
    img: withBase('imgs/robots/4%E5%8F%B7%E6%AD%A5%E5%85%B5.webp'), 
    features: ['快速机动', '灵活打击', '前线突破']
  },
  { 
    id: 3, 
    name: 'SENTRY | 哨兵', 
    type: 'Auto Defense', 
    img: withBase('imgs/robots/7%E5%8F%B7%E5%93%A8%E5%85%B5.webp'), 
    features: ['自主导航', '自主决策', '区域控制']
  },
  { 
    id: 4, 
    name: 'ENGINEER | 工程', 
    type: 'Economic Support', 
    img: withBase('imgs/robots/2%E5%8F%B7%E5%B7%A5%E7%A8%8B.webp'), 
    features: ['地形跨越', '资源获取', '机械臂操作']
  },
  { 
    id: 5, 
    name: 'DART | 飞镖', 
    type: 'Long Range', 
    img: withBase('imgs/robots/8%E5%8F%B7%E9%A3%9E%E9%95%96.webp'), 
    features: ['超远程打击', '超高伤害', '致盲效果']
  },
  { 
    id: 6, 
    name: 'RADAR | 雷达', 
    type: 'Surveillance', 
    img: withBase('imgs/robots/9%E5%8F%B7%E9%9B%B7%E8%BE%BE.webp'), 
    features: ['全场视野', '信息共享', '战术中心']
  },
  { 
    id: 7, 
    name: 'AERIAL | 空中', 
    type: 'Air Support', 
    img: withBase('imgs/robots/6%E5%8F%B7%E6%97%A0%E4%BA%BA%E6%9C%BA.webp'), 
    features: ['空中打击', '强化火力', '视野侦察']
  },
])

const activeRobot = ref<number | null>(null)

const toggleRobot = (id: number) => {
  activeRobot.value = activeRobot.value === id ? null : id
}
</script>

<template>
  <div class="robots-container">
    <div class="header">
      <h1 class="page-title">MECHA ARSENAL <span class="count">[{{ robots.length }} UNITS DETECTED]</span></h1>
    </div>

    <div class="robots-grid">
      <div 
        v-for="robot in robots" 
        :key="robot.id" 
        class="robot-card"
        :class="{ active: activeRobot === robot.id }"
        @click="toggleRobot(robot.id)"
      >
        <div class="card-bg"></div>
        <div class="robot-visual">
          <img :src="robot.img" :alt="robot.name" loading="lazy" />
        </div>
        
        <div class="robot-info">
          <h2 class="robot-name">{{ robot.name }}</h2>
          <div class="robot-type">{{ robot.type }}</div>
        </div>

        <transition name="features-slide">
          <div class="features-panel" v-if="activeRobot === robot.id">
            <div class="features-list">
              <div v-for="(feature, idx) in robot.features" :key="idx" class="feature-tag">
                <span class="tag-icon">▸</span>
                {{ feature }}
              </div>
            </div>
          </div>
        </transition>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.robots-container {
  padding: 2rem 4rem;
  height: 100%;
}

.header {
  margin-bottom: 2rem;
  border-bottom: 1px solid rgba($color-primary, 0.3);
  padding-bottom: 1rem;
}

.page-title {
  font-family: $font-title;
  color: $color-white;
  display: flex;
  align-items: center;
  gap: 1rem;
  
  .count {
    color: $color-primary;
    font-size: 1rem;
    font-family: $font-code;
  }
}

.robots-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 2rem;
}

.robot-card {
  position: relative;
  height: 400px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba($color-text-dim, 0.2);
  overflow: hidden;
  cursor: pointer;
  transition: all 1.3s cubic-bezier(0.18, 0.98, 0.22, 1);
  transform-origin: left center;
  will-change: transform, box-shadow;
  
  &:hover {
    border-color: $color-primary;
    box-shadow: 0 0 20px rgba($color-primary, 0.2);
    
    .robot-visual img {
      transform: scale(1.05);
      filter: drop-shadow(0 0 10px rgba($color-primary, 0.5));
    }
  }
  
  &.active {
    grid-column: span 2;
    background: rgba($color-primary, 0.05);
    border-color: $color-accent;
    animation: card-expand 1.6s cubic-bezier(0.2, 0.9, 0.2, 1);
    
    .robot-visual {
      width: 55%;
      justify-content: flex-start;
      padding-left: 3rem;
    }
    
  }
}

.robot-visual {
  height: 70%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  
  img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
    transition: 0.3s;
    filter: drop-shadow(0 10px 10px black);
  }
}

.robot-info {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 1.5rem;
  background: linear-gradient(to top, rgba(0,0,0,0.9), transparent);
  
  .robot-name {
    font-family: $font-title;
    color: $color-white;
    margin: 0;
    font-size: 1.5rem;
  }
  
  .robot-type {
    font-family: $font-code;
    color: $color-primary;
    font-size: 0.8rem;
  }
}

.features-panel {
  position: absolute;
  top: 0;
  right: 0;
  width: 45%;
  height: 100%;
  background: rgba(13, 13, 14, 0.95);
  border-left: 2px solid $color-accent;
  padding: 2rem 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  pointer-events: auto;
  
  .features-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  
  .feature-tag {
    font-family: $font-code;
    font-size: 1rem;
    color: $color-white;
    padding: 0.8rem 1rem;
    background: rgba($color-primary, 0.1);
    border-left: 3px solid $color-accent;
    display: flex;
    align-items: center;
    gap: 0.8rem;
    transition: all 0.3s;
    
    &:hover {
      background: rgba($color-primary, 0.2);
      transform: translateX(5px);
    }
    
    .tag-icon {
      color: $color-accent;
      font-size: 1.2rem;
    }
  }
}

.features-panel .feature-tag {
  animation: feature-rise 1.3s cubic-bezier(0.18, 0.98, 0.22, 1) both;
}

.features-panel .feature-tag:nth-child(1) { animation-delay: 0.08s; }
.features-panel .feature-tag:nth-child(2) { animation-delay: 0.16s; }
.features-panel .feature-tag:nth-child(3) { animation-delay: 0.24s; }
.features-panel .feature-tag:nth-child(4) { animation-delay: 0.32s; }
.features-panel .feature-tag:nth-child(5) { animation-delay: 0.4s; }
.features-panel .feature-tag:nth-child(6) { animation-delay: 0.48s; }
.features-panel .feature-tag:nth-child(7) { animation-delay: 0.56s; }
.features-panel .feature-tag:nth-child(8) { animation-delay: 0.64s; }

.features-slide-enter-active,
.features-slide-leave-active {
  transition: opacity 1.3s ease-out, transform 1.3s cubic-bezier(0.18, 0.98, 0.22, 1);
}

.features-slide-enter-from,
.features-slide-leave-to {
  opacity: 0;
  transform: translateX(14px);
}

.features-slide-enter-to,
.features-slide-leave-from {
  opacity: 1;
  transform: translateX(0);
}

@keyframes card-expand {
  0% {
    transform: scaleX(0.95) scaleY(0.985);
    opacity: 0.99;
    box-shadow: 0 0 0 rgba($color-primary, 0);
  }
  60% {
    transform: scaleX(1.003) scaleY(1.002);
    box-shadow: 0 0 20px rgba($color-primary, 0.2);
  }
  100% {
    transform: scaleX(1) scaleY(1);
    opacity: 1;
    box-shadow: 0 0 18px rgba($color-primary, 0.15);
  }
}

@keyframes feature-rise {
  0% {
    opacity: 0;
    transform: translateY(10px) scale(0.98);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
</style>
