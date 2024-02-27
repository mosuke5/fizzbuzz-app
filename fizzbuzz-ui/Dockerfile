# ビルドステージ
FROM node:18 as builder

ARG ENVIRONMENT
ENV ENVIRONMENT=${ENVIRONMENT}
# アプリケーションのソースコードをコピー
WORKDIR /app

COPY . .
RUN npm install

# TypeScriptをコンパイル
RUN npm run build

# サンプル用に--build-argで渡したパラメータを成果物にいれておく
RUN echo "hello ${ENVIRONMENT}" > /app/dist/hello.html

# 実行ステージ
FROM registry.access.redhat.com/ubi8/nginx-122

# ビルドステージからビルド済みのファイルをコピー
COPY --from=builder /app/dist .

# Nginxを起動
CMD ["nginx", "-g", "daemon off;"]

