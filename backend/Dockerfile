# 1. Build Stage
FROM node:20-alpine AS builder
WORKDIR /app

# devDependencies를 포함한 모든 의존성 설치
COPY package*.json ./
RUN npm install

# 소스 코드 복사 및 애플리케이션 빌드
COPY . .
RUN npm run build

# 2. Production Stage
FROM node:20-alpine
WORKDIR /app

# 프로덕션 의존성만 설치
COPY package*.json ./
RUN npm install --only=prod

# 빌드 결과물만 이전 스테이지에서 복사
COPY --from=builder /app/dist ./dist

# 애플리케이션 실행
CMD ["node", "dist/main"]