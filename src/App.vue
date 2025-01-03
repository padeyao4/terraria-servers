<script setup lang="ts">
import { ref } from 'vue'
import { ElCard, ElTag, ElScrollbar } from 'element-plus'

const serverList = ref([
  {
    id: 1,
    name: '服务器1',
    address: '192.168.1.1',
    admin: 'admin',
    description: '这是一个泰拉瑞亚服务器',
    status: '运行中'
  },
  {
    id: 2,
    name: '服务器2',
    address: '192.168.1.2',
    admin: 'admin',
    description: '这是一个泰拉瑞亚服务器',
    status: '运行中'
  },
  {
    id: 3,
    name: '服务器3',
    address: '192.168.1.3',
    admin: 'admin',
    description: '这是一个泰拉瑞亚服务器',
    status: '运行中'
  }
])
</script>

<template>
  <div class="root">
    <div class="container">
      <header class="header">
        <div class="header-content">
          <h2 class="main-title">Terraria Server</h2>
          <div class="header-actions">
            <el-button 
              type="primary" 
              icon="Plus" 
              circle 
              size="default"
              title="添加服务器"
            />
            <el-avatar 
              class="avatar" 
              icon="User" 
              :size="36"
              src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642ab5acc11d8d85.jpeg" 
            />
          </div>
        </div>
      </header>
      
      <hr class="divider"/>
      
      <main class="main-content">
        <el-scrollbar>
          <div class="server-grid">
            <el-card v-for="server in serverList" :key="server.id" class="server-card" shadow="hover">
              <template #header>
                <div class="card-header">
                  <span>{{ server.name }}</span>
                  <el-tag type="success" size="small">{{ server.status }}</el-tag>
                </div>
              </template>

              <div class="server-details">
                <p><strong>地址：</strong>{{ server.address }}</p>
                <p><strong>管理员：</strong>{{ server.admin }}</p>
                <p><strong>描述：</strong>{{ server.description }}</p>
              </div>
            </el-card>
          </div>
        </el-scrollbar>
      </main>
    </div>
  </div>
</template>

<style scoped>
body, html {
  margin: 0;
  padding: 0;
  background: linear-gradient(135deg, #f6f8f9 0%, #e5ebee 100%);
  min-height: 100vh;
}

.root{
  background-color: #f6f8f9;
  width: 100vw;
  height: 100%;
}

.container {
  max-width: 1200px;
  height: 100vh;
  margin: 0 auto;
  padding: 20px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  overflow-x: hidden;
}

.header {
  margin-bottom: 20px;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.server-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.server-card {
  transition: all 0.3s ease;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.server-details {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.server-metrics {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 10px;
}

.metric {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.title-section {
  display: flex;
  flex-direction: column;
}

.title-section h2 {
  margin: 0;
  color: #2c3e50;
  font-size: 1.5rem;
  font-weight: 600;
}

.subtitle {
  margin: 0;
  color: #7f8c8d;
  font-size: 0.9rem;
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 10px;
}

.divider {
  border: none;
  border-top: 1px solid rgba(44, 62, 80, 0.1);
  margin: 20px 0;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 10px;
}

.main-title {
  margin: 0;
  color: #2c3e50;
  font-size: 1.5rem;
  font-weight: 600;
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 10px;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 10px;
}
</style>