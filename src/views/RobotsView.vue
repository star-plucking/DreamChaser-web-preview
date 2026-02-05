<script setup lang="ts">
import { ref } from 'vue'

const robots = ref([
  { 
    id: 1, 
    name: 'HERO | 英雄', 
    type: 'Destroy Turret', 
    img: '/imgs/robots/1号英雄.webp', 
    features: ['高伤害', '远程吊射', '建筑摧毁']
  },
  { 
    id: 2, 
    name: 'INFANTRY | 步兵', 
    type: 'Main Assault', 
    img: '/imgs/robots/4号步兵.webp', 
    features: ['快速机动', '灵活打击', '前线突破']
  },
  { 
    id: 3, 
    name: 'SENTRY | 哨兵', 
    type: 'Auto Defense', 
    img: '/imgs/robots/7号哨兵.webp', 
    features: ['自主导航', '自主决策', '区域控制']
  },
  { 
    id: 4, 
    name: 'ENGINEER | 工程', 
    type: 'Economic Support', 
    img: '/imgs/robots/2号工程.webp', 
    features: ['地形跨越', '资源获取', '机械臂操作']
  },
  { 
    id: 5, 
    name: 'DART | 飞镖', 
    type: 'Long Range', 
    img: '/imgs/robots/8号飞镖.webp', 
    features: ['超远程打击', '超高伤害', '致盲效果']
  },
  { 
    id: 6, 
    name: 'RADAR | 雷达', 
    type: 'Surveillance', 
    img: '/imgs/robots/9号雷达.webp', 
    features: ['全场视野', '信息共享', '战术中心']
  },
  { 
    id: 7, 
    name: 'AERIAL | 空中', 
    type: 'Air Support', 
    img: '/imgs/robots/6号无人机.webp', 
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

        <div class="features-panel" v-if="activeRobot === robot.id">
          <div class="features-list">
            <div v-for="(feature, idx) in robot.features" :key="idx" class="feature-tag">
              <span class="tag-icon">▸</span>
              {{ feature }}
            </div>
          </div>
        </div>
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
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  
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
    
    .robot-visual {
      width: 55%;
      justify-content: flex-start;
      padding-left: 3rem;
    }
    
    .features-panel {
      opacity: 1;
      transform: translateX(0);
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
  opacity: 0;
  transform: translateX(20px);
  transition: 0.3s 0.1s;
  pointer-events: none;
  
  .robot-card.active & {
    pointer-events: auto;
  }
  
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
</style>
