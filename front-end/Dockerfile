# 使用 node 作为构建阶段的基础镜像
FROM node:16-alpine AS build

# 设置工作目录
WORKDIR /app

# 复制 package.json 和 package-lock.json
COPY package*.json ./

# 安装依赖
RUN npm install

# 复制项目文件到工作目录
COPY . .

# 构建前端应用
RUN npm run build

# 使用 nginx 作为生产阶段的基础镜像
FROM nginx:alpine

# 设置环境变量
ENV BASE_URL='http://182.92.100.66:5000/'

# 复制构建输出到 nginx 默认的静态文件目录
COPY --from=build /app/dist /usr/share/nginx/html

# 复制 nginx 配置文件
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 暴露 80 端口
EXPOSE 80

# 启动 nginx
CMD ["nginx", "-g", "daemon off;"]
