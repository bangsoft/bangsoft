# 1단계: 빌드 전용
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# 2단계: 정적 파일 서비스 (http-server)
FROM node:20-alpine

WORKDIR /app

# 빌드 결과 복사
COPY --from=builder /app/dist ./dist

# 정적 서버 설치
RUN npm install -g http-server

EXPOSE 8080

CMD ["http-server", "dist"]
