FROM node:20-alpine

WORKDIR /app

# Instala dependências básicas do sistema
RUN apk add --no-cache git openssh-client netcat-openbsd tzdata

# Configura timezone
ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Copia arquivos de dependência
COPY package*.json ./
COPY package-lock.json ./

# Instala dependências via npm
RUN npm ci

# Copia o restante do código
COPY . .

# Torna scripts executáveis, se existirem
RUN chmod +x copy_cert_assets.sh docker-entrypoint.sh || true

# Executa o script de certificados (caso exista)
RUN ./copy_cert_assets.sh || true

# Compila o projeto (caso tenha build)
RUN npm run build --if-present

# Expõe a porta padrão
EXPOSE 3957

# Define o entrypoint
CMD ["./docker-entrypoint.sh"]
