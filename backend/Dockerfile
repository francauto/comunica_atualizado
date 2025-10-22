FROM node:20-alpine

WORKDIR /app

# Dependências básicas
RUN apk add --no-cache git openssh-client netcat-openbsd tzdata

# Configura timezone
ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Instala dependências
COPY package*.json ./
COPY yarn.lock ./
RUN yarn install --frozen-lockfile

# Copia o código do backend
COPY . .

# Torna scripts executáveis
RUN chmod +x copy_cert_assets.sh docker-entrypoint.sh || true

# Executa o script de certificados se existir
RUN ./copy_cert_assets.sh || true

# Build final
RUN yarn build

EXPOSE 3000
CMD ["./docker-entrypoint.sh"]
