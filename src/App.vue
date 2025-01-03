<script setup lang="ts">
import { ref, computed } from 'vue'
import { ElCard, ElScrollbar } from 'element-plus'


const serverList = ref([
  {
    id: 1,
    name: '服务器1',
    address: '192.168.1.1',
    admin: 'admin1',
    description: '泰拉瑞亚主服务器',
    status: '运行中'
  },
  {
    id: 2,
    name: '服务器2',
    address: '192.168.1.2',
    admin: 'admin2',
    description: '泰拉瑞亚备用服务器',
    status: '运行中'
  },
  {
    id: 3,
    name: '服务器3',
    address: '192.168.1.3',
    admin: 'admin3',
    description: '泰拉瑞亚测试服务器',
    status: '离线'
  },
  {
    id: 4,
    name: '服务器4',
    address: '192.168.1.4',
    admin: 'admin4',
    description: '泰拉瑞亚开发服务器',
    status: '运行中'
  },
  {
    id: 5,
    name: '服务器5',
    address: '192.168.1.5',
    admin: 'admin5',
    description: '泰拉瑞亚社区服务器',
    status: '运行中'
  },
  {
    id: 6,
    name: '服务器6',
    address: '192.168.1.6',
    admin: 'admin6',
    description: '泰拉瑞亚PVP服务器',
    status: '离线'
  },
  {
    id: 7,
    name: '服务器7',
    address: '192.168.1.7',
    admin: 'admin7',
    description: '泰拉瑞亚生存服务器',
    status: '运行中'
  },
  {
    id: 8,
    name: '服务器8',
    address: '192.168.1.8',
    admin: 'admin8',
    description: '泰拉瑞亚创造服务器',
    status: '运行中'
  },
  {
    id: 9,
    name: '服务器9',
    address: '192.168.1.9',
    admin: 'admin9',
    description: '泰拉瑞亚模组服务器',
    status: '离线'
  },
  {
    id: 10,
    name: '服务器10',
    address: '192.168.1.10',
    admin: 'admin10',
    description: '泰拉瑞亚专家模式服务器',
    status: '运行中'
  },
  {
    id: 11,
    name: '服务器11',
    address: '192.168.1.11',
    admin: 'admin11',
    description: '泰拉瑞亚困难模式服务器',
    status: '运行中'
  },
  {
    id: 12,
    name: '服务器12',
    address: '192.168.1.12',
    admin: 'admin12',
    description: '泰拉瑞亚仲裁者服务器',
    status: '离线'
  },
  {
    id: 13,
    name: '服务器13',
    address: '192.168.1.13',
    admin: 'admin13',
    description: '泰拉瑞亚极限模式服务器',
    status: '运行中'
  },
  {
    id: 14,
    name: '服务器14',
    address: '192.168.1.14',
    admin: 'admin14',
    description: '泰拉瑞亚娱乐服务器',
    status: '运行中'
  },
  {
    id: 15,
    name: '服务器15',
    address: '192.168.1.15',
    admin: 'admin15',
    description: '泰拉瑞亚竞技服务器',
    status: '离线'
  },
  {
    id: 16,
    name: '服务器16',
    address: '192.168.1.16',
    admin: 'admin16',
    description: '泰拉瑞亚休闲服务器',
    status: '运行中'
  }
])

function getStatusClass(status: string) {
  switch(status) {
    case '运行中': return 'status-running'
    case '离线': return 'status-offline'
    default: return 'status-unknown'
  }
}
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
      
      <main class="main-content">
        <el-scrollbar>
          <div class="server-grid">
            <el-card 
              v-for="server in serverList" 
              :key="server.id" 
              class="server-card" 
              shadow="hover"
            >
              <template #header>
                <div class="card-header">
                  <span>{{ server.name }}</span>
                  <div 
                    class="server-status-indicator" 
                    :class="getStatusClass(server.status)"
                    title="服务器状态"
                  />
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
  background: rgba(255, 255, 255, 0.9);
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
}

.header {
  position: sticky;
  top: 0;
  z-index: 100;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  padding: 16px;
  border-bottom: 1px solid rgba(44, 62, 80, 0.1);
}

.header-content {
  display: flex;
  height: 100%;
  width: 100%;
  justify-content: space-between;
  align-items: center;
}

.server-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  margin: 16px;
}

.server-card {
  transition: all 0.3s ease;
  border-radius: 6px;
  overflow: hidden;
}

:deep(.el-card) {
  border-radius: 6px;
}

:deep(.el-card__header) {
  border-top-left-radius: 6px;
  border-top-right-radius: 6px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.server-details {
  background: rgba(255, 255, 255, 0.8);
  padding: 10px;
  border-radius: 6px;
}

.server-details p {
  margin: 5px 0;
  line-height: 1.5;
}

.server-details strong {
  color: #2c3e50;
  font-weight: 500;
  margin-right: 5px;
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

.card-header span {
  font-size: 1.1rem;
  font-weight: 600;
  color: #2c3e50;
}

.server-status-indicator {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  display: inline-block;
}

.status-running {
  background-color: #67c23a;  /* 绿色 */
}

.status-offline {
  background-color: #f56c6c;  /* 红色 */
}

.status-unknown {
  background-color: #e6a23c;  /* 黄色 */
}

.main-content {
  flex-grow: 1;
  overflow-y: auto;
}

/* 隐藏滚动条，但保留滚动功能 */
.main-content::-webkit-scrollbar {
  width: 0;
  background: transparent;
}
</style>