<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

// 发展历程时间线
const milestones = [
  {
    year: '2015-2018',
    title: '前身阶段',
    titleEn: 'Early Years',
    desc: '自动化学院成立RoboMaster和Robocon参赛队，Robocon战队在2016年和2017年分别获得全国三等奖和北部分区赛三等奖',
    descEn: 'School of Automation established RoboMaster and Robocon teams. Robocon team won National Third Prize in 2016 and Northern Regional Third Prize in 2017',
    image: ''
  },
  {
    year: '2018',
    title: '正式成立',
    titleEn: 'Official Establishment',
    desc: '2018年5月10日，北京理工大学机器人队正式挂牌成立，战队名称确定为Dream Chaser（追梦战队），释义为"我们都在努力奔跑，我们都是追梦人"',
    descEn: 'May 10, 2018, BIT Robot Team officially established as Dream Chaser, meaning "We are all running hard, we are all dream chasers"',
    image: ''
  },
  {
    year: '2019',
    title: '首战告捷',
    titleEn: 'First Victory',
    desc: '获得北部赛区二等奖，全国三等奖，步兵对抗单项赛全国冠军',
    descEn: 'Northern Regional Second Prize, National Third Prize, and National Champion in Infantry Combat',
    image: ''
  },
  {
    year: '2020',
    title: '线上突破',
    titleEn: 'Online Achievement',
    desc: '受疫情影响线下赛取消，线上评审获得全国二等奖，工程机器人获得线上评审一等奖',
    descEn: 'Due to COVID-19, won National Second Prize in online review, Engineering Robot won First Prize',
    image: ''
  },
  {
    year: '2021',
    title: '晋级八强',
    titleEn: 'Top 8 Achievement',
    desc: '北部赛区一等奖，以八强成绩晋级全国赛，获得全国二等奖',
    descEn: 'Northern Regional First Prize, advanced to nationals as Top 8, won National Second Prize',
    image: ''
  },
  {
    year: '2022',
    title: '多线开花',
    titleEn: 'Multiple Achievements',
    desc: '东部赛区二等奖、全国赛三等奖，高校联盟赛一等奖',
    descEn: 'Eastern Regional Second Prize, National Third Prize, University League First Prize',
    image: ''
  },
  {
    year: '2023',
    title: '稳步前行',
    titleEn: 'Steady Progress',
    desc: '北部分区赛三十二强',
    descEn: 'Top 32 in Northern Regional',
    image: ''
  },
  {
    year: '2024',
    title: '巅峰时刻',
    titleEn: 'Peak Moment',
    desc: '中部分区赛冠军，全国赛十六强，获得国家级一等奖',
    descEn: 'Central Regional Champion, National Top 16, National First Prize',
    image: ''
  },
  {
    year: '2025',
    title: '持续拼搏',
    titleEn: 'Continuous Effort',
    desc: '东部分区赛三十二强',
    descEn: 'Top 32 in Eastern Regional',
    image: ''
  }
]

// 荣誉展示
const honors = [
  {
    title: '2024中部赛区冠军',
    titleEn: '2024 Central Regional Champion',
    event: 'RoboMaster 2024',
    eventEn: 'RoboMaster 2024',
    image: ''
  },
  {
    title: '国家级一等奖',
    titleEn: 'National First Prize',
    event: 'RoboMaster 2024中部分区赛',
    eventEn: 'RoboMaster 2024 Central Regional',
    image: ''
  },
  {
    title: '高校联盟赛一等奖',
    titleEn: 'University League First Prize',
    event: 'RoboMaster 2022',
    eventEn: 'RoboMaster 2022',
    image: ''
  },
  {
    title: '北部赛区一等奖',
    titleEn: 'Northern Regional First Prize',
    event: 'RoboMaster 2021',
    eventEn: 'RoboMaster 2021',
    image: ''
  },
  {
    title: '步兵对抗全国冠军',
    titleEn: 'Infantry Combat National Champion',
    event: 'RoboMaster 2019',
    eventEn: 'RoboMaster 2019',
    image: ''
  },
  {
    title: 'Robocon全国三等奖',
    titleEn: 'Robocon National Third Prize',
    event: 'Robocon 2016',
    eventEn: 'Robocon 2016',
    image: ''
  }
]
</script>

<template>
  <div class="history-container">
    <div class="header">
      <h1>{{ t('history.title') }}</h1>
      <p>{{ t('history.subtitle') }}</p>
    </div>

    <!-- 发展历程时间线 -->
    <section class="timeline-section">
      <h2 class="section-title">{{ t('history.journey') }}</h2>
      <div class="timeline">
        <div v-for="(milestone, index) in milestones" :key="index" class="timeline-item" :class="{ right: index % 2 === 1 }">
          <div class="timeline-content">
            <div class="timeline-year">{{ milestone.year }}</div>
            <div class="timeline-card">
              <div v-if="milestone.image" class="timeline-image">
                <img :src="milestone.image" :alt="milestone.title" />
              </div>
              <div class="timeline-info">
                <h3>{{ $i18n.locale === 'zh-CN' ? milestone.title : milestone.titleEn }}</h3>
                <p>{{ $i18n.locale === 'zh-CN' ? milestone.desc : milestone.descEn }}</p>
              </div>
            </div>
          </div>
          <div class="timeline-dot"></div>
        </div>
      </div>
    </section>

    <!-- 荣誉墙 -->
    <section class="honors-section">
      <h2 class="section-title">{{ t('history.honors') }}</h2>
      <div class="honors-grid">
        <div v-for="(honor, index) in honors" :key="index" class="honor-card">
          <div v-if="honor.image" class="honor-image">
            <img :src="honor.image" :alt="honor.title" />
          </div>
          <div v-else class="honor-placeholder">
            <div class="trophy-icon">🏆</div>
          </div>
          <div class="honor-info">
            <h3>{{ $i18n.locale === 'zh-CN' ? honor.title : honor.titleEn }}</h3>
            <p>{{ $i18n.locale === 'zh-CN' ? honor.event : honor.eventEn }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style lang="scss" scoped>
.history-container {
  padding: 2rem 4rem;
  height: 100%;
  overflow-y: auto;
}

.header {
  text-align: center;
  margin-bottom: 4rem;
  
  h1 {
    font-family: $font-title;
    font-size: 4rem;
    color: $color-primary;
    @include text-glow;
    margin: 0;
    text-transform: uppercase;
  }
  
  p {
    color: $color-text-dim;
    font-family: $font-code;
    letter-spacing: 4px;
    margin-top: 1rem;
    font-size: 1.2rem;
  }
}

.section-title {
  font-family: $font-title;
  font-size: 2.5rem;
  color: $color-accent;
  text-align: center;
  margin-bottom: 3rem;
  text-transform: uppercase;
  position: relative;
  
  &::after {
    content: '';
    display: block;
    width: 100px;
    height: 3px;
    background: $color-accent;
    margin: 1rem auto 0;
  }
}

// 时间线样式
.timeline-section {
  max-width: 1200px;
  margin: 0 auto 6rem;
}

.timeline {
  position: relative;
  padding: 2rem 0;
  
  &::before {
    content: '';
    position: absolute;
    left: 50%;
    top: 0;
    bottom: 0;
    width: 2px;
    background: linear-gradient(180deg, transparent, $color-primary, transparent);
    transform: translateX(-50%);
  }
}

.timeline-item {
  display: flex;
  justify-content: flex-end;
  padding-right: 50%;
  position: relative;
  margin-bottom: 3rem;
  
  &.right {
    justify-content: flex-start;
    padding-right: 0;
    padding-left: 50%;
    
    .timeline-content {
      margin-left: 3rem;
    }
  }
  
  .timeline-content {
    margin-right: 3rem;
    max-width: 500px;
  }
}

.timeline-year {
  font-family: $font-title;
  font-size: 2rem;
  color: $color-primary;
  font-weight: bold;
  margin-bottom: 1rem;
  @include text-glow;
}

.timeline-card {
  @include glass-panel;
  padding: 1.5rem;
  transition: all 0.3s;
  
  &:hover {
    transform: translateY(-5px);
    border-color: $color-primary;
    box-shadow: 0 0 30px rgba($color-primary, 0.3);
  }
  
  .timeline-image {
    width: 100%;
    height: 200px;
    margin-bottom: 1rem;
    overflow: hidden;
    border: 1px solid rgba($color-primary, 0.3);
    
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  
  .timeline-info {
    h3 {
      font-family: $font-title;
      font-size: 1.5rem;
      color: $color-white;
      margin: 0 0 0.5rem;
    }
    
    p {
      font-family: $font-code;
      color: $color-text-dim;
      font-size: 0.95rem;
      line-height: 1.6;
      margin: 0;
    }
  }
}

.timeline-dot {
  position: absolute;
  left: 50%;
  top: 0;
  width: 20px;
  height: 20px;
  background: $color-primary;
  border: 4px solid $color-bg;
  border-radius: 50%;
  transform: translateX(-50%);
  box-shadow: 0 0 20px $color-primary;
  z-index: 10;
}

// 荣誉墙样式
.honors-section {
  max-width: 1400px;
  margin: 0 auto;
}

.honors-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.honor-card {
  @include glass-panel;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s;
  
  &:hover {
    transform: translateY(-10px) scale(1.02);
    border-color: $color-accent;
    box-shadow: 0 0 40px rgba($color-accent, 0.4);
  }
  
  .honor-image {
    width: 100%;
    height: 250px;
    margin-bottom: 1.5rem;
    overflow: hidden;
    border: 2px solid rgba($color-accent, 0.3);
    
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  
  .honor-placeholder {
    width: 100%;
    height: 250px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, rgba($color-primary, 0.1), rgba($color-accent, 0.1));
    border: 2px dashed rgba($color-accent, 0.3);
    margin-bottom: 1.5rem;
    
    .trophy-icon {
      font-size: 6rem;
      filter: drop-shadow(0 0 20px rgba($color-accent, 0.5));
    }
  }
  
  .honor-info {
    h3 {
      font-family: $font-title;
      font-size: 1.5rem;
      color: $color-accent;
      margin: 0 0 0.5rem;
      text-transform: uppercase;
    }
    
    p {
      font-family: $font-code;
      color: $color-text-dim;
      font-size: 1rem;
      margin: 0;
    }
  }
}

// 响应式适配
@media (max-width: 768px) {
  .timeline {
    &::before {
      left: 30px;
    }
  }
  
  .timeline-item {
    padding-right: 0;
    padding-left: 60px !important;
    
    .timeline-content {
      margin: 0 !important;
    }
  }
  
  .timeline-dot {
    left: 30px;
  }
}
</style>
