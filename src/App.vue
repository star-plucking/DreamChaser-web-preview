<script setup lang="ts">
import { RouterView } from 'vue-router'
import NavBar from '@/components/NavBar.vue'
import StatusBar from '@/components/StatusBar.vue'
import CommanderAssistant from '@/components/CommanderAssistant.vue'
</script>

<template>
  <div class="command-center-layout">
    <header class="top-bar">
      <NavBar />
    </header>
    
    <main class="viewport">
      <RouterView v-slot="{ Component }">
        <transition name="glitch-fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </RouterView>
    </main>

    <footer class="bottom-status">
      <StatusBar />
    </footer>

    <!-- 虚拟看板娘 -->
    <CommanderAssistant />
  </div>
</template>

<style lang="scss" scoped>
.command-center-layout {
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow: hidden;
  position: relative;
}

.top-bar {
  height: 64px;
  z-index: 100;
  border-bottom: 1px solid rgba($color-primary, 0.2);
  background: rgba($color-bg, 0.8);
  backdrop-filter: blur(10px);
}

.viewport {
  flex: 1;
  position: relative;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 0;
}

.bottom-status {
  height: 40px;
  border-top: 1px solid rgba($color-primary, 0.2);
  background: $color-bg;
  z-index: 100;
}

/* Transition Effects */
.glitch-fade-enter-active,
.glitch-fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.glitch-fade-enter-from,
.glitch-fade-leave-to {
  opacity: 0;
  transform: scale(1.02);
  filter: blur(2px);
}
</style>
