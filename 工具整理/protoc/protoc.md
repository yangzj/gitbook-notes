> 生成go代码桩

```shell
/usr/local/protoc/bin/protoc --go_out=plugins=grpc:. --proto_path=. Greeter.proto
```

> 生成gateway代理桩代码

```shell
/usr/local/protoc/bin/protoc -I /usr/local/protoc/include --grpc-gateway_out=logtostderr=true:. --proto_path=. Greeter.proto
```

> 生成Swagger文档

```shell
/usr/local/protoc/bin/protoc --swagger_out=logtostderr=true:. --proto_path=. Greeter.proto
```

protoc -I /Users/eric/code/go_project/grpc-gateway-swagger/pkg/proto/ram/ --example_out=":gen" --proto_path=. proto/ram/*.proto



/usr/local/protoc/bin/protoc --markdown_out=:. --proto_path=. Greeter.proto



protoc --example_out=":gen" --proto_path=. proto/ram/*.proto



protoc  --example_out=":gen" --proto_path=./proto/ram/ ./proto/ram/aksk.proto



protoc  --example_out=":gen" --proto_path=./proto/ram/ ./proto/ram/*.proto





protoc -I ./proto/cpc/ --build-proxy_out=":" --proto_path=. proto/cpc/*.proto