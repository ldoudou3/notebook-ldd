代理用于开发时解决跨域，将前端请求转发到后端。
```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { resolve } from 'path'
import {API_BASE_URL} from './src/utils/constants'

// https://vite.dev/config/

export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': resolve(__dirname, 'src')
    }
  },

  server: {
    proxy: {
      '/api': {
        target: API_BASE_URL,
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')  //路径重写
      }
    }
  }
})

// 代理规则匹配: /api → target: http://localhost:8080
```