# kala-redis

``` dockerfile
FROM  golang:alpine3.12

RUN apk add --no-cache \
    git


RUN apk add --update --no-cache py-pip && \
    pip3 install --upgrade pip setuptools httpie && \
    rm -r /root/.cache

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install Kala
RUN go get -v github.com/ajvb/kala


WORKDIR /kala-ui/
COPY . .

#Run App
CMD ["kala", "serve", "-v", "--jobdb=redis", "--jobdb-address=redis-server:6379"]
EXPOSE 8000
```
