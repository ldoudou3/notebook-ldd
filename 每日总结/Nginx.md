1. nginx的作用
	1. 反向代理：在高并发场景，可以在多个服务器上部署后端，前端发来的所有请求，经过nginx，负载均衡的分发给不同的后端。
	2. 网关：日志、压缩、限流、自定义
2. 实现 nginx.conf中定义
3. 单线程
	1. 用单线程来处理所有的网络连接，解决了并发问题；
4. 多进程
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