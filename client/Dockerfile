FROM node:alpine
WORKDIR '/app'
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
# ElasticBeanstalk only port expose
EXPOSE 3000

# Copy over nginx configuration file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# From '0' is the previous 'FROM' build. Can't use FROM node:alpine as NAMED
# Copy over all HTML from previous container into the nginx web server directory
COPY --from=0 /app/build /usr/share/nginx/html
