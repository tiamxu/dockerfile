# dockerfile
基础镜像dockerfile

#alpine基础镜像
```
基础alpine制作glibc基础镜像
####apk镜像源修改
sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
###修改时区
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone
###修改字体


```
#node基础镜像
```
FROM veryxuliang/alpine:3.10.2

RUN apk add --no-cache curl nodejs npm && \
npm install --production --registry=https://registry.npm.taobao.org && \
npm install -g pm2 --registry=https://registry.npm.taobao.org && \
rm -rf /root/.npm /root/.node-gyp /root/.config /root/.pm2 /usr/lib/node_modules/npm/man  \
/usr/share/man/* /usr/share/doc /tmp/* /var/cache/apk/*  \
/usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html /usr/lib/node_modules/npm/scripts

#构建
docker build -t veryxuliang/nodebase:10.16.3 -f Dockerfile.v2 .
#查看
docker run -it --rm veryxuliang/nodebase:10.16.3
/ # node -v
v10.16.3
/ # npm -v
6.9.0

