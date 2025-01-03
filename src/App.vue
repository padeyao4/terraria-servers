<script setup lang="ts">
import { ref } from 'vue'
import { ElCard, ElTag, ElScrollbar } from 'element-plus'

function getProgressColor(percentage: string) {
  const num = parseInt(percentage)
  if (num < 60) return '#67c23a'  // 绿色
  if (num < 80) return '#e6a23c'  // 黄色
  return '#f56c6c'  // 红色
}

const serverList = ref([
  {
    id: 1,
    name: '服务器1',
    address: '192.168.1.1',
    admin: 'admin',
    description: '这是一个泰拉瑞亚服务器',
    status: '运行中',
    cpu: '80%',
    memory: '60%'
  },
  {
    id: 2,
    name: '服务器2',
    address: '192.168.1.2',
    admin: 'admin',
    description: '这是一个泰拉瑞亚服务器',
    status: '运行中',
    cpu: '50%',
    memory: '40%'
  },
  {
    id: 3,
    name: '服务器3',
    address: '192.168.1.3',
    admin: 'admin',
    description: '这是一个泰拉瑞亚服务器',
    status: '运行中',
    cpu: '70%',
    memory: '55%'
  }
])
</script>

<template>
  <div class="root">
  <div class="container">
    <header class="header">
      <div class="header-content">
        <h2 style="color: #2c3e50;">Terraria Server List</h2>
        <el-avatar class="avatar" icon="User" :size="50"
          src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642ab5acc11d8d85.jpeg" />
      </div>
    </header>
    <hr style="border: 1px solid #2c3e5020;margin-bottom: 24px;"/>
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

              <div class="server-metrics">
                <div class="metric">
                  <span>CPU</span>
                  <el-progress :percentage="parseInt(server.cpu)" :color="getProgressColor(server.cpu)" />
                </div>
                <div class="metric">
                  <span>内存</span>
                  <el-progress :percentage="parseInt(server.memory)" :color="getProgressColor(server.memory)" />
                </div>
              </div>
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
</style>