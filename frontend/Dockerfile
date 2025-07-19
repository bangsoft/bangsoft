# 1단계: 빌더
FROM node:20-alpine AS builder

WORKDIR /app

# 모든 의존성 설치 (빌드에 필요)
COPY package*.json ./
RUN npm install

# 소스코드 복사 및 빌드
COPY . .
RUN npm run build

# 프로덕션용 의존성만 다시 설치 (이미지 크기 최적화)
RUN npm prune --production

# 2단계: 실행 환경 최소화
FROM node:20-alpine

WORKDIR /app

# 빌드 결과 및 프로덕션 의존성 복사
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules

EXPOSE 3000

CMD ["node", "dist/main"]
