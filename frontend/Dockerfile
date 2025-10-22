FROM node:20-alpine

WORKDIR /app

RUN npm install -g serve

COPY package*.json ./
COPY yarn.lock ./
RUN yarn install --frozen-lockfile

COPY . .

RUN chmod +x copy_brand_assets.sh update_tab_name.sh update_app_color.sh || true
RUN ./copy_brand_assets.sh || true
RUN ./update_tab_name.sh || true
RUN ./update_app_color.sh || true

RUN yarn build

EXPOSE 3001
CMD ["serve", "-s", "build", "-l", "3001"]
