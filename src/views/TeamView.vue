<script setup lang="ts">
import { ref } from 'vue'

interface Member {
  id: number;
  name: string;
  role: string;
  group: string; // 分类：MANAGEMENT、OPERATORS 等
  img: string;
  title: string; // 队内职务
  technicalGroup: string; // 技术组
  description: string; // 个人介绍
}

// 模拟数据 - 实际应从 public/imgs/people 读取或重命名后引用
// 这里为了演示稳定性，部分使用机器人图或占位图，如果您已在 public/imgs/people 下整理好，可替换路径
const members = ref<Member[]>([
  { 
    id: 1, name: 'Cheng Zhihong', role: 'Captain', group: 'MANAGEMENT', 
    img: '/imgs/people/3号-操作手-陈志鸿-大二.webp',
    title: '队长',
    technicalGroup: '电控组',
    description: '具备卓越的领导能力和技术专长，负责团队整体战略规划与执行。'
  },
  { 
    id: 2, name: 'Wang Beizhuo', role: 'Project Manager', group: 'MANAGEMENT', 
    img: '/imgs/people/1号-操作手-王倍卓-大二.webp',
    title: '项管',
    technicalGroup: '机械组',
    description: '优秀的项目管理者，协调团队资源与进度，确保项目按时高质量完成。'
  },
  { 
    id: 3, name: 'Jiang Huantong', role: 'Head of the Embedded Software Group', group: 'EMBEDDED SOFTWARE', 
    img: 'public\\imgs\\people\\北京理工大学_人员\\北京理工大学_人员\\研发代表\\7号-研发代表-姜欢桐-大二.webp',
    title: '电控组负责人',
    technicalGroup: '电控组',
    description: '嵌入式软件专家，精通系统架构设计与优化，领导电控组技术研发。Sugar Bro aka 唐哥'
  },
  { 
    id: 4, name: 'Yang Ruixinag', role: 'Head of the Mechanical Group', group: 'MECHANICS', 
    img: '/imgs/people/4号-操作手-杨锐翔-大二.webp',
    title: '机械组负责人',
    technicalGroup: '机械组',
    description: '机械设计和加工工艺专家，负责机构优化和可靠性保障。创新意识强，方案执行能力强。'
  }
])

const activeMember = ref<Member>(members.value[0])

const selectMember = (m: Member) => {
  activeMember.value = m
}
</script>

<template>
  <div class="team-container">
    <div class="roster-panel">
      <h2 class="panel-title">/// ACTIVE ROSTER</h2>
      
      <div class="group-section">
        <h3 class="group-title">MANAGEMENT</h3>
        <div class="member-list">
          <div 
            v-for="m in members.filter(x => x.group === 'MANAGEMENT')" 
            :key="m.id"
            class="member-card-mini"
            :class="{ active: activeMember.id === m.id }"
            @click="selectMember(m)"
          >
            <div class="avatar-thumb">
              <img :src="m.img" alt="" />
            </div>
            <div class="info">
              <div class="name">{{ m.name }}</div>
              <div class="role">{{ m.role }}</div>
            </div>
          </div>
        </div>
      </div>

      <div class="group-section">
        <h3 class="group-title">ENGINEERING</h3>
        <div class="member-list">
          <div 
            v-for="m in members.filter(x => x.group !== 'OPERATORS' && x.group !== 'MANAGEMENT')" 
            :key="m.id"
            class="member-card-mini"
            :class="{ active: activeMember.id === m.id }"
            @click="selectMember(m)"
          >
            <div class="avatar-thumb">
              <img :src="m.img" alt="" />
            </div>
            <div class="info">
              <div class="name">{{ m.name }}</div>
              <div class="role">{{ m.role }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="profile-panel">
      <div class="profile-card">
        <div class="profile-header">
          <div class="id-tag">ID: 00{{ activeMember.id }}</div>
          <h1 class="full-name">{{ activeMember.name }}</h1>
          <div class="rank">POSITION: {{ activeMember.role.toUpperCase() }}</div>
        </div>
        
        <div class="profile-body">
          <div class="photo-large">
            <img :src="activeMember.img" :alt="activeMember.name" />
            <div class="scan-line"></div>
          </div>
          
          <div class="bio-section">
            <div class="bio-item">
              <label>队内职务</label>
              <div class="bio-content">{{ activeMember.title }}</div>
            </div>
            
            <div class="bio-item">
              <label>技术组</label>
              <div class="bio-content">{{ activeMember.technicalGroup }}</div>
            </div>
            
            <div class="bio-item">
              <label>个人介绍</label>
              <div class="bio-content bio-description">{{ activeMember.description }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.team-container {
  display: flex;
  height: 100%;
  padding: 2rem;
  gap: 2rem;
}

.roster-panel {
  width: 300px;
  border-right: 1px solid rgba($color-primary, 0.2);
  padding-right: 2rem;
  overflow-y: auto;
  
  .panel-title {
    color: $color-accent;
    font-family: $font-title;
    margin-bottom: 2rem;
  }
  
  .group-title {
    color: $color-text-dim;
    font-size: 0.8rem;
    margin: 1.5rem 0 1rem;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }
}

.member-card-mini {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 10px;
  border: 1px solid transparent;
  cursor: pointer;
  background: rgba(0,0,0,0.3);
  margin-bottom: 8px;
  transition: 0.2s;
  
  &:hover {
    background: rgba($color-primary, 0.1);
  }
  
  &.active {
    border-color: $color-primary;
    background: rgba($color-primary, 0.15);
    
    .name { color: $color-primary; }
  }
  
  .avatar-thumb {
    width: 40px; height: 40px;
    background: #333;
    overflow: hidden;
    img { width: 100%; height: 100%; object-fit: cover; }
  }
  
  .name { font-family: $font-title; color: white; font-size: 0.9rem; }
  .role { font-size: 0.7rem; color: $color-text-dim; }
}

.profile-panel {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.profile-card {
  width: 100%;
  max-width: 800px;
  background: rgba(13, 13, 14, 0.8);
  border: 1px solid $color-primary;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  position: relative;
  
  &::before {
    content: '';
    position: absolute;
    top: -5px; left: -5px; right: -5px; bottom: -5px;
    border: 1px dashed rgba($color-primary, 0.3);
    z-index: -1;
  }
}

.profile-header {
  border-bottom: 2px solid $color-primary;
  padding-bottom: 1rem;
  
  .id-tag { color: $color-text-dim; font-family: $font-code; }
  .full-name { font-family: $font-title; font-size: 3rem; margin: 0; color: white; text-transform: uppercase; }
  .rank { color: $color-accent; font-family: $font-code; letter-spacing: 2px; }
}

.profile-body {
  display: flex;
  gap: 3rem;
  height: 400px;
}

.photo-large {
  flex: 1;
  background: #000;
  position: relative;
  overflow: hidden;
  border: 1px solid rgba(255,255,255,0.1);
  
  img {
    width: 100%;
    height: 100%;
    object-fit: contain; // 使用 cover 如果照片比例统一
    filter: contrast(110%);
  }
  
  .scan-line {
    position: absolute;
    top: 0; left: 0; width: 100%; height: 4px;
    background: rgba($color-primary, 0.5);
    box-shadow: 0 0 10px $color-primary;
    animation: scan 3s infinite linear;
    pointer-events: none;
  }
}

@keyframes scan {
  0% { top: -10%; }
  100% { top: 110%; }
}

.bio-section {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  overflow-y: auto;
  padding-right: 1rem;
  
  .bio-item {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    
    label {
      color: $color-accent;
      font-family: $font-title;
      font-size: 0.9rem;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    
    .bio-content {
      color: $color-text-dim;
      font-size: 0.95rem;
      line-height: 1.6;
      padding: 0.75rem;
      background: rgba(255,255,255,0.05);
      border-left: 2px solid $color-primary;
      padding-left: 1rem;
    }
    
    .bio-description {
      min-height: 80px;
    }
  }
}
</style>
