FROM node:14.14.0-alpine as builder
WORKDIR '/app'
COPY package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# If line below doesn't work, remove the "as builder" on line 1 and on the line below change --from=builder to --from=0 (the rest stays the same)
COPY --from=builder /app/build /usr/share/nginx/html