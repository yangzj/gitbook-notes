# 域名规约

1. 模版：${appName}-grpc-${env}.test.com, e.g. ums-grpc-dev.test.com, ums-grpc-stage.test.com

# 拦截器

1. 统一参数传递
   1. gd_user: json字符串，{"id":1,"orgId":2,"attributes":{"key":"value"}}，其中id为userId
2. deadline传递
   1. 设置全局的deadline参数（默认：60s），默认值为一个很大的值
   2. 支持deadline传递，A->B->C, B获取到A传递过来的dealine，直接传递给C，B不用重新设置新的deadline值 
3. 全局异常处理（java处理方式，其他语言需要确认是否该操作）
   1. 捕获到未知异常时，转为grpc异常，进行抛给请求端
4. 日志记录
   1. 请求方法、请求参数、gd_trace_no，接收到请求时间、请求处理时长。日志记录后，上报日志平台展示

# keeplive设置

1. 心跳保持
   1. 在没有请求时，客户端与服务端需要保持心跳通讯，参数：grpc.keepalive_permit_without_calls