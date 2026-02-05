<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const contactMethods = [
  { icon: '📧', key: 'email', value: 'public@dreamchaser.ink' },
  { icon: '📱', key: 'phone', value: '+86 17511626718 (工作日)' },
  { icon: '💬', key: 'wechat', value: 'Dream Chaser机器人战队' },
  { icon: '🎮', key: 'qq', value: '106794812' },
  { icon: '📍', key: 'address', value: '北京市房山区北京理工大学良乡校区工训楼' }
]

const positions = [
  { key: 'mechanical', icon: '⚙️' },
  { key: 'electrical', icon: '💡' },
  { key: 'vision', icon: '👁️' },
  { key: 'control', icon: '💻' }
]

const goToWeChat = () => {
  window.open('https://mp.weixin.qq.com/s/UfRi2xrtFgaQ58vVTs3UNA', '_blank')
}
</script>

<template>
  <div class="contact-container">
    <div class="contact-header">
      <h1 class="contact-title">{{ t('contact.title') }}</h1>
      <p class="contact-subtitle">{{ t('contact.subtitle') }}</p>
    </div>

    <div class="content-grid">
      <!-- 联系方式 -->
      <section class="contact-section">
        <h2 class="section-title">
          <span class="title-line"></span>
          {{ t('contact.contactInfo') }}
          <span class="title-line"></span>
        </h2>
        
        <div class="contact-cards">
          <div v-for="method in contactMethods" :key="method.key" class="contact-card">
            <div class="contact-icon">{{ method.icon }}</div>
            <div class="contact-details">
              <div class="contact-label">{{ t(`contact.${method.key}`) }}</div>
              <div class="contact-value">{{ method.value }}</div>
            </div>
          </div>
        </div>
      </section>

      <!-- 加入我们 -->
      <section class="join-section">
        <h2 class="section-title">
          <span class="title-line"></span>
          {{ t('contact.joinUs') }}
          <span class="title-line"></span>
        </h2>
        
        <div class="join-banner">
          <h3>{{ t('contact.joinTitle') }}</h3>
          <p>{{ t('contact.joinDesc') }}</p>
        </div>

        <div class="positions-title">{{ t('contact.positions') }}</div>
        <div class="positions-grid">
          <div v-for="pos in positions" :key="pos.key" class="position-card">
            <div class="position-icon">{{ pos.icon }}</div>
            <h4 class="position-name">{{ t(`contact.${pos.key}`) }}</h4>
            <p class="position-desc">{{ t(`contact.${pos.key}Desc`) }}</p>
          </div>
        </div>

        <button class="recruitment-btn" @click="goToWeChat">
          {{ t('contact.recruitment') }} >>
        </button>
      </section>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.contact-container {
  min-height: 100%;
  padding: 4rem;
  background: $color-bg;
}

.contact-header {
  text-align: center;
  margin-bottom: 4rem;
  
  .contact-title {
    font-family: $font-title;
    font-size: 4rem;
    color: $color-primary;
    @include text-glow;
    margin: 0 0 1rem;
    text-transform: uppercase;
  }
  
  .contact-subtitle {
    font-family: $font-code;
    color: $color-text-dim;
    font-size: 1.2rem;
    letter-spacing: 2px;
  }
}

.content-grid {
  max-width: 1400px;
  margin: 0 auto;
  display: grid;
  gap: 4rem;
}

.section-title {
  display: flex;
  align-items: center;
  gap: 1rem;
  font-family: $font-title;
  font-size: 2rem;
  color: $color-primary;
  margin-bottom: 2rem;
  text-transform: uppercase;
  
  .title-line {
    flex: 1;
    height: 2px;
    background: linear-gradient(90deg, transparent, $color-primary, transparent);
  }
}

// 联系方式卡片
.contact-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.contact-card {
  @include glass-panel;
  padding: 2rem;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  transition: all 0.3s;
  
  &:hover {
    transform: translateY(-5px);
    border-color: $color-primary;
    box-shadow: 0 0 30px rgba($color-primary, 0.3);
  }
  
  .contact-icon {
    font-size: 3rem;
    flex-shrink: 0;
  }
  
  .contact-details {
    flex: 1;
    
    .contact-label {
      font-family: $font-code;
      color: $color-accent;
      font-size: 0.9rem;
      margin-bottom: 0.5rem;
      text-transform: uppercase;
    }
    
    .contact-value {
      font-family: $font-code;
      color: $color-white;
      font-size: 1.1rem;
      word-break: break-all;
    }
  }
}

// 加入我们
.join-section {
  .join-banner {
    @include glass-panel;
    padding: 3rem;
    text-align: center;
    margin-bottom: 3rem;
    background: linear-gradient(135deg, rgba($color-primary, 0.1), rgba($color-secondary, 0.1));
    
    h3 {
      font-family: $font-title;
      font-size: 2.5rem;
      color: $color-primary;
      margin: 0 0 1rem;
      @include text-glow;
    }
    
    p {
      font-family: $font-code;
      color: $color-text-main;
      font-size: 1.2rem;
      margin: 0;
    }
  }
  
  .positions-title {
    font-family: $font-code;
    font-size: 1.5rem;
    color: $color-accent;
    text-align: center;
    margin-bottom: 2rem;
    text-transform: uppercase;
  }
}

.positions-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 3rem;
}

.position-card {
  @include glass-panel;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s;
  
  &:hover {
    transform: translateY(-8px) scale(1.02);
    border-color: $color-accent;
    box-shadow: 0 0 40px rgba($color-accent, 0.3);
  }
  
  .position-icon {
    font-size: 3.5rem;
    margin-bottom: 1rem;
  }
  
  .position-name {
    font-family: $font-title;
    font-size: 1.5rem;
    color: $color-primary;
    margin: 0 0 1rem;
    text-transform: uppercase;
  }
  
  .position-desc {
    font-family: $font-code;
    color: $color-text-dim;
    font-size: 0.9rem;
    line-height: 1.6;
    margin: 0;
  }
}

.recruitment-btn {
  display: block;
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
  padding: 1.5rem;
  background: $color-secondary;
  border: 2px solid $color-secondary;
  color: $color-white;
  font-family: $font-title;
  font-size: 1.3rem;
  font-weight: bold;
  text-transform: uppercase;
  cursor: pointer;
  clip-path: polygon(10% 0, 100% 0, 100% 70%, 90% 100%, 0 100%, 0 30%);
  transition: all 0.3s;
  
  &:hover {
    background: transparent;
    transform: scale(1.05);
    box-shadow: 0 0 30px rgba($color-secondary, 0.5);
  }
}
</style>
