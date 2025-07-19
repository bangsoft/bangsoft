# 1단계: 빌드 전용
FROM node:20-alpine AS builder

WORKDIR /app

# 의존성 설치
COPY package*.json ./
RUN npm install

# 소스코드 복사 & 빌드
COPY . .

# ✅ npx로 빌드 실행 (vite 또는 react 기반 프레임워크 대응)
RUN npx vite build
# 또는
# RUN npx react-scripts build

# 2단계: http-server로 정적파일 서빙
FROM node:20-alpine

WORKDIR /app

# 빌드 결과 복사
COPY --from=builder /app/dist ./dist

# ✅ 정적 서버 설치
RUN npm install -g http-server

EXPOSE 8080

CMD ["http-server", "dist"]
