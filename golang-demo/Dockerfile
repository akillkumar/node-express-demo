FROM public.ecr.aws/zeet/lambdahandler:v0.2.0 as build

RUN yum install -y golang
RUN go env -w GOPROXY=direct

ADD go.mod go.sum ./

RUN go mod download
ADD . .

RUN go build -o /main

FROM public.ecr.aws/zeet/lambdahandler:v0.2.0
ENV BIN main
COPY --from=build /$BIN /$BIN
ENTRYPOINT [ "/main" ]  
