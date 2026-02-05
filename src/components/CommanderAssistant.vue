<script setup lang="ts">
import { ref } from 'vue'

const isExpanded = ref(false)
const showMenu = ref(false)

const nasUrls = {
  internal: 'http://nas.dreamchaser.ink',
  external: 'http://nas2.dreamchaser.ink'
}

const toggleMenu = () => {
  showMenu.value = !showMenu.value
  isExpanded.value = !isExpanded.value
}

const openNas = (type: 'internal' | 'external') => {
  window.open(nasUrls[type], '_blank')
  showMenu.value = false
  isExpanded.value = false
}
</script>

<template>
  <div class="assistant-container" :class="{ expanded: isExpanded }">
    <div class="nas-menu" v-if="showMenu">
      <div class="menu-title">选择NAS入口</div>
      <button class="menu-item" @click="openNas('internal')">
        <span class="icon">🏫</span>
        <div class="item-info">
          <div class="item-title">校内访问</div>
          <div class="item-url">nas.dreamchaser.ink</div>
        </div>
      </button>
      <button class="menu-item" @click="openNas('external')">
        <span class="icon">🌐</span>
        <div class="item-info">
          <div class="item-title">校外访问</div>
          <div class="item-url">nas2.dreamchaser.ink</div>
        </div>
      </button>
    </div>
    <div class="avatar" @click="toggleMenu">
      <div class="avatar-placeholder">
        <span class="nas-icon">📁</span>
      </div>
      <div class="ring"></div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.assistant-container {
  position: fixed;
  bottom: 60px;
  right: 20px;
  z-index: 200;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 15px;
}

.avatar {
  width: 80px;
  height: 80px;
  position: relative;
  cursor: pointer;
  transition: transform 0.3s;
  
  &:hover {
    transform: scale(1.1);
  }

  .avatar-placeholder {
    width: 100%;
    height: 100%;
    background: radial-gradient(circle at 30% 30%, $color-primary, #000);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    border: 2px solid $color-primary;
    box-shadow: 0 0 15px $color-primary;
    font-size: 2rem;
    
    .nas-icon {
      filter: drop-shadow(0 0 8px $color-primary);
    }
  }

  .ring {
    position: absolute;
    top: -5px; left: -5px;
    width: 90px; height: 90px;
    border: 1px dashed $color-accent;
    border-radius: 50%;
    animation: rotate 10s linear infinite;
  }
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.nas-menu {
  background: rgba(13, 13, 14, 0.95);
  border: 2px solid $color-primary;
  border-radius: 12px;
  padding: 1rem;
  min-width: 280px;
  box-shadow: 0 0 30px rgba($color-primary, 0.3);
  animation: slideIn 0.3s ease-out;
  
  .menu-title {
    color: $color-primary;
    font-family: $font-title;
    font-size: 1rem;
    margin-bottom: 1rem;
    text-align: center;
    padding-bottom: 0.5rem;
    border-bottom: 1px solid rgba($color-primary, 0.3);
  }
  
  .menu-item {
    width: 100%;
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1rem;
    margin-bottom: 0.5rem;
    background: rgba($color-primary, 0.05);
    border: 1px solid rgba($color-primary, 0.3);
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s;
    color: $color-white;
    
    &:last-child {
      margin-bottom: 0;
    }
    
    &:hover {
      background: rgba($color-primary, 0.15);
      border-color: $color-primary;
      transform: translateX(-5px);
      box-shadow: 0 0 15px rgba($color-primary, 0.3);
    }
    
    .icon {
      font-size: 1.8rem;
      flex-shrink: 0;
    }
    
    .item-info {
      flex: 1;
      text-align: left;
      
      .item-title {
        font-family: $font-title;
        font-size: 1rem;
        margin-bottom: 0.25rem;
        color: $color-white;
      }
      
      .item-url {
        font-family: $font-code;
        font-size: 0.75rem;
        color: $color-text-dim;
      }
    }
  }
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
