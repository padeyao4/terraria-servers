<script setup lang="ts">
import { Connection, Document, User } from '@element-plus/icons-vue'
import { ElCard, ElIcon, ElScrollbar } from 'element-plus'
import { onMounted, ref } from 'vue'

import PocketBase, { type ListResult, type RecordModel } from 'pocketbase';

const pb = new PocketBase('https://pb.liangpi.site');

interface Server {
  id: string;
  name: string;
  address: string;
  admin: string;
  description: string;
}

const serverList = ref<ListResult<RecordModel>>();

onMounted(async () => {
  // fetch a paginated records list
  const resultList = await pb.collection('terraria_server').getList(1, 50, {
      filter: 'address != ""',
  });
  serverList.value = resultList;
});


function getStatusClass(status: string) {
  switch (status) {
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
            <el-button type="primary" icon="Plus" circle size="default" title="添加服务器" />
            <el-avatar class="avatar" icon="User" :size="36"
              src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642ab5acc11d8d85.jpeg" />
          </div>
        </div>
      </header>

      <main class="main-content">
        <el-scrollbar>
          <div class="server-grid">
            <el-card v-for="server in serverList?.items" :key="server.id" class="server-card" shadow="hover">
              <template #header>
                <div class="card-header">
                  <el-text size="large">{{ server.name }}</el-text>
                  <div class="server-status-indicator" :class="getStatusClass(server.online)" title="服务器状态" />
                </div>
              </template>

              <div class="server-details">
                <p>
                  <el-icon>
                    <Connection />
                  </el-icon>
                  <el-text>地址：{{ server.address }}:{{ server.port }}</el-text>
                </p>
                <p>
                  <el-icon>
                    <User />
                  </el-icon>
                  <el-text>管理员：{{ server.admin }}</el-text>
                </p>
                <p>
                  <el-icon>
                    <Document />
                  </el-icon>
                  <el-text>详情：{{ server.detail.length > 10 ? server.detail.substring(0, 10) + '...' : server.detail }}</el-text>
                </p>
              </div>
            </el-card>
          </div>
        </el-scrollbar>
      </main>
    </div>
  </div>
</template>

<style scoped>
body,
html {
  margin: 0;
  padding: 0;
  background: linear-gradient(135deg, #f6f8f9 0%, #e5ebee 100%);
  min-height: 100vh;
  overflow: hidden;
}

.root {
  background-color: #f6f8f9;
  width: 100vw;
  height: 100%;
  overflow: hidden;
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
  display: flex;
  align-items: center;
  gap: 8px;
  margin: 5px 0;
  line-height: 1.5;
}

.server-details .el-icon {
  color: #2c3e50;
  font-size: 16px;
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
  background-color: #67c23a;
  /* 绿色 */
}

.status-offline {
  background-color: #f56c6c;
  /* 红色 */
}

.status-unknown {
  background-color: #e6a23c;
  /* 黄色 */
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