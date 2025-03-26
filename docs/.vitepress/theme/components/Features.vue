<template>
    <div class="features">
      <div v-for="(feature, index) in features" :key="index" class="feature-item" @click="navigate(feature.link)">
        <h3>{{ feature.title }}</h3>
        <p>{{ feature.details }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import { useData } from 'vitepress';
  import { useRouter } from 'vitepress'; // 引入 useRouter
  
  export default {
    setup() {
      const { theme } = useData();
      const router = useRouter(); // 获取路由实例
      // 使用 import.meta.env.BASE_URL 获取 base 路径
      const base = import.meta.env.BASE_URL || '/';
      return {
        features: theme.value.features || [], // 从 themeConfig 中读取 features
        navigate: (link) => {
            if (link) {
                const fullPath = `${base}${link.replace(/^\//, '')}`; // 拼接 base 和 link
                debugger
                router.go(fullPath); // 使用 router.go 方法跳转
            }
        },
      };
    },
  };
  </script>
  
  <style scoped>
  .features {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap:20px;
  }
  
  .feature-item {
    border: 1px solid #ddd;
    padding: 15px;
    border-radius: 8px;
    cursor: pointer;
    transition: transform 0.2s ease;
  }
  
  .feature-item:hover {
    transform: scale(1.05);
  }
  </style>