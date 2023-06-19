# import golang base image
FROM golang:1.16-buster AS build

# 设置工作目录,使用 WORKDIR 指令可以来指定工作目录（或者称为当前目录），
# 以后各层的当前目录就被改为指定的目录，如该目录不存在，WORKDIR 会帮你建立目录。
WORKDIR /app

# 将项目 modules files 复制进image中 /app/go.mod /app/go.sum
COPY go.mod go.sum ./

# 引入程序源码
COPY *.go ./

# RUN 执行命令，下载项目引用的依赖
RUN go mod download

# 上一步完成了工具链：编译、链接...，开始编译构建程序的二进制可执行文件
RUN go build -o /docker-gs-ping-roach

##
## Deploy
##
FROM gcr.io/distroless/base-debian10

WORKDIR /

# 将编译后的二进制文件放入更精简的“distroless”镜像中来构建最终镜像
COPY --from=build /docker-gs-ping-roach /docker-gs-ping-roach

EXPOSE 8080

USER nonroot:nonroot

# CMD and ENTRYPOINT tell Docker what command to execute when our image is used to start a container.
# images 加载进 container 时需要执行的操作
# CMD ["/docker-ps-ping"]
ENTRYPOINT ["/docker-gs-ping-roach"]



