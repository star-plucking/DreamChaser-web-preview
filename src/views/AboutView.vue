<script setup lang="ts">
import { ref } from 'vue'

const withBase = (path: string) => `${import.meta.env.BASE_URL}${path.replace(/^\//, '')}`

// 随机打乱数组的工具函数
const shuffleArray = <T>(array: T[]): T[] => {
  const newArr = [...array]
  for (let i = newArr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [newArr[i], newArr[j]] = [newArr[j], newArr[i]]
  }
  return newArr
}

// 照片墙数据 - 为每张图片分配不同的尺寸类型
const photos = ref(shuffleArray([
  { id: 1, src: withBase('imgs/photo_wall/photo_01.webp'), size: 'large' },
  { id: 2, src: withBase('imgs/photo_wall/photo_02.webp'), size: 'wide' },
  { id: 3, src: withBase('imgs/photo_wall/photo_03.webp'), size: 'small' },
  { id: 4, src: withBase('imgs/photo_wall/photo_04.webp'), size: 'wide' },
  { id: 5, src: withBase('imgs/photo_wall/photo_05.webp'), size: 'large' },
  { id: 6, src: withBase('imgs/photo_wall/photo_06.webp'), size: 'small' },
  { id: 7, src: withBase('imgs/photo_wall/photo_07.webp'), size: 'medium' },
  { id: 8, src: withBase('imgs/photo_wall/photo_08.webp'), size: 'wide' },
  { id: 9, src: withBase('imgs/photo_wall/photo_09.webp'), size: 'large' },
  { id: 10, src: withBase('imgs/photo_wall/photo_10.webp'), size: 'wide' },
  { id: 11, src: withBase('imgs/photo_wall/photo_11.webp'), size: 'small' }
]))

const selectedPhoto = ref<string | null>(null)

const openPhoto = (src: string) => {
  selectedPhoto.value = src
}

const closePhoto = () => {
  selectedPhoto.value = null
}
</script>

<template>
  <div class="about-container">
    <!-- 队伍介绍部分 -->
    <section class="intro-section">
      <div class="section-header">
        <h1 class="section-title">/// TEAM PROFILE</h1>
        <div class="title-deco"></div>
      </div>

      <div class="intro-content">
        <div class="content-wrapper">
          <div class="team-name">
            <span class="team-cn">北京理工大学追梦战队</span>
            <span class="team-en">DREAM CHASER</span>
          </div>

          <div class="description-block">
            <p>
              北京理工大学追梦战队（Dream Chaser） 成立于2018年，是由自动化学院指导、面向全校选拔的校级学生机器人战队，前身可追溯至2015年的RoboMaster与Robocon参赛队。战队以 RoboMaster机甲大师赛 为核心平台，致力于培养具备价值引领、知识积累与工程实践能力的工程创新人才。
            </p>

            <p>
              战队在近十年中屡获佳绩，多次晋级全国赛并斩获国家级奖项，2024赛季获得分区赛冠军及全国赛一等奖。其发展始终秉持“追求极致、团队协作、勇于创新”等核心原则。除竞赛外，追梦战队高度重视技术研发与文化传承，通过“薪火培训”、校内机甲大师赛、技术开源等方式推动科创普及，并形成“谦卑、包容、传承”的团队文化。同时以“机娘IP”和多平台新媒体运营构建独特品牌影响力。
            </p>

            <p>
              目前，战队拥有80余名跨学院成员，致力于打造高质量科创平台，欢迎不同基础的同学加入，共同在机器人竞赛与工程实践中追梦前行。
            </p>
          </div>

          <div class="stats-highlight">
            <div class="stat-item">
              <div class="stat-number">2018</div>
              <div class="stat-label">成立年份</div>
            </div>
            <div class="stat-item">
              <div class="stat-number">80+</div>
              <div class="stat-label">队员人数</div>
            </div>
            <div class="stat-item">
              <div class="stat-number">1ST</div>
              <div class="stat-label">2024全国赛</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 照片墙部分 -->
    <section class="photo-wall-section">
      <div class="section-header">
        <h2 class="section-title">/// MOMENTS ARCHIVE</h2>
        <div class="title-deco"></div>
      </div>

      <div class="photo-grid">
        <div
          v-for="photo in photos"
          :key="photo.id"
          :class="['photo-item', `photo-${photo.size}`]"
          @click="openPhoto(photo.src)"
        >
          <div class="photo-frame">
            <img :src="photo.src" :alt="`照片 ${photo.id}`" />
            <div class="photo-overlay">
              <div class="photo-id">#{{ String(photo.id).padStart(2, '0') }}</div>
            </div>
            <div class="corner-deco top-left"></div>
            <div class="corner-deco top-right"></div>
            <div class="corner-deco bottom-left"></div>
            <div class="corner-deco bottom-right"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- 图片预览弹窗 -->
    <transition name="modal-fade">
      <div v-if="selectedPhoto" class="photo-modal" @click="closePhoto">
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="closePhoto">
            <span>×</span>
          </button>
          <img :src="selectedPhoto" alt="预览" />
        </div>
      </div>
    </transition>
  </div>
</template>

<style lang="scss" scoped>
.about-container {
  min-height: 100%;
  padding: 2rem 4rem;
  padding-bottom: 4rem;
}

/* Section Header */
.section-header {
  margin-bottom: 2rem;
  position: relative;

  .section-title {
    font-family: $font-title;
    font-size: 2rem;
    color: $color-accent;
    text-transform: uppercase;
    letter-spacing: 2px;
    display: inline-block;
  }

  .title-deco {
    height: 2px;
    background: linear-gradient(90deg, $color-primary 0%, transparent 100%);
    margin-top: 0.5rem;
  }
}

/* 介绍部分 */
.intro-section {
  margin-bottom: 4rem;

  .intro-content {
    @include glass-panel;
    padding: 2rem;
    position: relative;

    &::before {
      content: '';
      position: absolute;
      top: -1px;
      left: 20px;
      right: 20px;
      height: 1px;
      background: $color-primary;
      box-shadow: 0 0 10px $color-primary;
    }
  }

  .content-wrapper {
    max-width: 1200px;
    margin: 0 auto;
  }

  .team-name {
    text-align: center;
    margin-bottom: 2rem;
    padding-bottom: 1.5rem;
    border-bottom: 1px solid rgba($color-primary, 0.3);

    .team-cn {
      display: block;
      font-size: 2rem;
      font-weight: bold;
      color: $color-text-main;
      margin-bottom: 0.5rem;
    }

    .team-en {
      display: block;
      font-family: $font-title;
      font-size: 1.2rem;
      color: $color-primary;
      letter-spacing: 4px;
      @include text-glow;
    }
  }

  .description-block {
    font-size: 1rem;
    line-height: 1.8;
    color: $color-text-dim;

    p {
      margin-bottom: 1.5rem;
      text-indent: 2em;
      text-align: justify;

      &:hover {
        color: rgba($color-text-main, 0.9);
        transition: color 0.3s ease;
      }
    }
  }

  .stats-highlight {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
    margin-top: 2rem;
    padding-top: 2rem;
    border-top: 1px solid rgba($color-primary, 0.3);

    .stat-item {
      text-align: center;
      padding: 1rem;
      background: rgba(0, 0, 0, 0.3);
      border: 1px solid rgba($color-primary, 0.2);
      position: relative;

      &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 2px;
        background: linear-gradient(90deg, transparent, $color-primary, transparent);
        animation: scan-line 3s infinite;
      }

      .stat-number {
        font-family: $font-title;
        font-size: 2.5rem;
        color: $color-primary;
        font-weight: bold;
        @include text-glow;
      }

      .stat-label {
        font-size: 0.9rem;
        color: $color-text-dim;
        margin-top: 0.5rem;
        letter-spacing: 1px;
      }
    }
  }
}

@keyframes scan-line {
  0%, 100% { transform: translateY(0); opacity: 0.3; }
  50% { transform: translateY(60px); opacity: 1; }
}

/* 照片墙部分 */
.photo-wall-section {
  .photo-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-auto-rows: 300px;
    gap: 1.5rem;
    grid-auto-flow: dense;
  }

  .photo-item {
    position: relative;
    overflow: hidden;
    cursor: pointer;

    &.photo-large {
      grid-column: span 2;
      grid-row: span 2;
    }

    &.photo-wide {
      grid-column: span 2;
      grid-row: span 1;
    }

    &.photo-medium {
      grid-column: span 1;
      grid-row: span 2;
    }

    &.photo-small {
      grid-column: span 1;
      grid-row: span 1;
    }

    .photo-frame {
      width: 100%;
      height: 100%;
      position: relative;
      border: 1px solid rgba($color-primary, 0.3);
      background: #000;
      overflow: hidden;
      transition: all 0.3s ease;

      &:hover {
        border-color: $color-primary;
        box-shadow: 0 0 20px rgba($color-primary, 0.4);
        transform: scale(1.02);

        .photo-overlay {
          opacity: 1;
        }

        img {
          filter: brightness(1.1) contrast(1.1);
        }
      }

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: all 0.3s ease;
        filter: grayscale(20%);
      }

      .photo-overlay {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: linear-gradient(135deg, rgba($color-primary, 0.2) 0%, transparent 50%);
        opacity: 0;
        transition: opacity 0.3s ease;
        pointer-events: none;

        .photo-id {
          position: absolute;
          top: 10px;
          right: 10px;
          font-family: $font-code;
          color: $color-primary;
          font-size: 0.8rem;
          background: rgba(0, 0, 0, 0.7);
          padding: 4px 8px;
          border: 1px solid $color-primary;
          @include text-glow;
        }
      }

      .corner-deco {
        position: absolute;
        width: 10px;
        height: 10px;
        border: 2px solid $color-primary;
        opacity: 0;
        transition: opacity 0.3s ease;

        &.top-left {
          top: 5px;
          left: 5px;
          border-right: none;
          border-bottom: none;
        }

        &.top-right {
          top: 5px;
          right: 5px;
          border-left: none;
          border-bottom: none;
        }

        &.bottom-left {
          bottom: 5px;
          left: 5px;
          border-right: none;
          border-top: none;
        }

        &.bottom-right {
          bottom: 5px;
          right: 5px;
          border-left: none;
          border-top: none;
        }
      }

      &:hover .corner-deco {
        opacity: 1;
      }
    }
  }
}

/* 图片预览弹窗 */
.photo-modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  backdrop-filter: blur(5px);

  .modal-content {
    position: relative;
    max-width: 90vw;
    max-height: 90vh;
    border: 2px solid $color-primary;
    box-shadow: 0 0 30px rgba($color-primary, 0.5);

    img {
      display: block;
      max-width: 100%;
      max-height: 90vh;
      object-fit: contain;
    }
  }

  .close-btn {
    position: absolute;
    top: -40px;
    right: 0;
    background: transparent;
    border: 1px solid $color-primary;
    color: $color-primary;
    font-size: 2rem;
    width: 40px;
    height: 40px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-family: $font-title;
    display: flex;
    align-items: center;
    justify-content: center;

    &:hover {
      background: rgba($color-primary, 0.2);
      box-shadow: 0 0 15px rgba($color-primary, 0.5);
    }
  }
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

/* 响应式设计 */
@media (max-width: 1024px) {
  .about-container {
    padding: 1.5rem 2rem;
  }

  .stats-highlight {
    grid-template-columns: repeat(3, 1fr);
  }

  .photo-grid {
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)) !important;
    grid-auto-rows: 220px !important;
  }
}

@media (max-width: 768px) {
  .about-container {
    padding: 1rem;
  }

  .section-title {
    font-size: 1.5rem !important;
  }

  .team-name .team-cn {
    font-size: 1.5rem !important;
  }

  .team-name .team-en {
    font-size: 1rem !important;
  }

  .stats-highlight {
    grid-template-columns: 1fr !important;
    gap: 1rem;
  }

  .photo-grid {
    grid-template-columns: repeat(2, 1fr) !important;
    grid-auto-rows: 160px !important;
  }

  .photo-item.photo-large {
    grid-column: span 2 !important;
    grid-row: span 2 !important;
  }

  .photo-item.photo-wide {
    grid-column: span 2 !important;
    grid-row: span 1 !important;
  }

  .photo-item.photo-medium {
    grid-column: span 1 !important;
    grid-row: span 2 !important;
  }
}
</style>
