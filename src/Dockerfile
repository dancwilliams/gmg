# Build Phase
FROM node:12.4 as builder
WORKDIR /app
COPY ./gmg-app ./gmg-app
COPY ./gmg-client ./gmg-client
COPY ./gmg-server ./gmg-server
COPY ./build.sh .
RUN apt-get update && \
    apt-get install dos2unix && \
    dos2unix ./build.sh && \
    /bin/bash ./build.sh

# Run Phase
FROM node:8.9.1 as runtime
COPY --from=builder /app/gmg-client /app/gmg-client
COPY --from=builder /app/gmg-server /app/gmg-server
COPY --from=builder /app/gmg-app /app/gmg-app
WORKDIR /app/gmg-server
CMD ["npm", "run", "start:release"]
EXPOSE 8000:80
