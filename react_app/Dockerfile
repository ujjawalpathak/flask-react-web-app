# build environment
FROM node:13.12.0-alpine as build
WORKDIR /stats
ENV PATH /stats/node_modules/.bin:$PATH
COPY package.json ./
COPY yarn.lock ./
RUN npm install --silent
RUN npm install react-scripts@3.4.1 -g --silent
COPY . ./
RUN npm run build

# production environment
FROM nginx:stable-alpine
COPY --from=build /stats/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]