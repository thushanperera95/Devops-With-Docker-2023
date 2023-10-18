FROM node:16-alpine3.17 as build-stage
WORKDIR /usr/src/app
COPY . .
RUN npm install && \
    REACT_APP_BACKEND_URL=http://localhost:8080 npm run build
FROM node:16-alpine3.17
EXPOSE 5000
WORKDIR /usr/src/app
COPY --from=build-stage /usr/src/app/build /usr/src/app/build
RUN npm install -g serve && \
    adduser -S appuser && \
    chown appuser .
USER appuser
CMD ["serve", "-s", "-l", "5000", "build"]