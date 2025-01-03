<script setup lang="ts">
import { ref } from 'vue';
const serverList = ref([
  { id: 1, name: '服务器1', address: '192.168.1.1', admin: 'admin', description: '这是一个泰拉瑞亚服务器' ,status: '运行中'},
  { id: 2, name: '服务器2', address: '192.168.1.2', admin: 'admin', description: '这是一个泰拉瑞亚服务器' ,status: '运行中' },
  { id: 3, name: '服务器3', address: '192.168.1.3', admin: 'admin', description: '这是一个泰拉瑞亚服务器' ,status: '运行中'},
])
</script>
<template>
  <div>
    <header>
      <div style="display: flex; align-items: center;">
        <h1 style="margin-right: 10px;">泰拉瑞亚服务器管理</h1>
        <el-avatar class="avatar" icon="User" />
      </div>

    </header>
    <main>
      <el-scrollbar>
        <div v-for="server in serverList" :key="server.id" class="server-item">
          <h2>{{ server.name }}</h2>
          <p>{{ server.address }}</p>
          <p>{{ server.admin }}</p>
          <el-tag type="success">{{ server.status }}</el-tag>
          <p>{{ server.description }}</p>
        </div>
      </el-scrollbar>
    </main>
  </div>
</template>
<style scoped>
.server-item {
  padding: 1rem;
  border: 1px solid #ccc;
  margin: 1rem 0;
}
</style>