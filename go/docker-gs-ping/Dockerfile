# import golang base image
FROM golang:1.19

# 设置工作目录,使用 WORKDIR 指令可以来指定工作目录（或者称为当前目录），
# 以后各层的当前目录就被改为指定的目录，如该目录不存在，WORKDIR 会帮你建立目录。
WORKDIR /app

# 将项目 modules files 复制进image中 /app/go.mod /app/go.sum
COPY ./go/docker-gs-ping/go.mod ./go/docker-gs-ping/go.sum ./

# RUN 执行命令，下载项目引用的依赖
RUN go mod download

# 引入程序源码
COPY ./go/docker-gs-ping/*.go ./

# 上一步完成了工具链：编译、链接...，开始编译构建程序的二进制可执行文件
RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping

EXPOSE 8080

# CMD tell Docker what command to execute when our image is used to start a container.
# images 加载进 container 时需要执行的操作
CMD ["/docker-gs-ping"]

