# 1단계: 빌더
FROM node:20-alpine AS builder

WORKDIR /app

# 모든 의존성 설치 (빌드에 필요)
COPY package*.json ./
RUN npm install

# Nest CLI가 설치되어 있지 않은 경우를 대비하여 npx 사용
# 또는 아래의 global 설치 중 하나 선택

# 👉 옵션 1: npx 사용해 nest build 실행 (추천)
COPY . .
RUN npx nest build

# 👉 옵션 2: Nest CLI 글로벌 설치
# RUN npm install -g @nestjs/cli
# COPY . .
# RUN nest build

# 프로덕션용 의존성만 다시 설치
RUN npm prune --production

# 2단계: 런타임 이미지
FROM node:20-alpine

WORKDIR /app

# 빌드된 결과물, 의존성 복사
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules

EXPOSE 3000

CMD ["node", "dist/main"]
