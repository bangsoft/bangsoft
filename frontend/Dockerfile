# 1단계: 빌더
FROM node:20-alpine AS builder

WORKDIR /app

# 의존성 설치
COPY package*.json ./
RUN npm install

# 앱 소스 복사
COPY . .

# ✅ vue-cli-service 빌드 (npx 사용)
RUN npx vue-cli-service build

# 2단계: 정적 서버로 제공
FROM node:20-alpine

WORKDIR /app

# 정적 빌드 파일 복사
COPY --from=builder /app/dist ./dist

# 정적 서버 설치
RUN npm install -g http-server

EXPOSE 8080

CMD ["http-server", "dist"]
