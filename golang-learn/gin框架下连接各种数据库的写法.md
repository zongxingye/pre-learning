# gin框架下的连接写法（如mysql，rabbitmq等）连接

## 不好的写法：
最初，我是声明了一个结构体，并通过函数接受的方式进行连接
```
type RabbitMQ struct {
	conn    *amqp.Connection
	channel *amqp.Channel
	done    chan error
}

func (r *RabbitMQ) Connect() (err error) {
	r.conn, err = amqp.Dial(uri)
	if err != nil {
		log.Printf("[amqp] connect error: %s\n", err)
		return err
	}
	r.channel, err = r.conn.Channel()
	if err != nil {
		log.Printf("[amqp] get channel error: %s\n", err)
		return err
	}
	r.done = make(chan error)
	return nil
}
```
因此，在业务罗辑代码块处的handler方法内，我建立了连接然后调用对应包的方法。
```
    // handler 内部
	rbmq := new(rabbitmq.RabbitMQ)
	err := rbmq.Connect()
	if err != nil {
		fmt.Println("链接shibai", err)
		return nil, nil
	}
    defer rbmq.Close()
    ...
```

这里有个问题就是，每次来一个请求线程我都是建立了一个连接，即每次都是建立一个tcp连接，开销相对巨大。因此，如果能够复用这个连接，可以大大减少开销

## 好的写法
```
func OrderPublish() (func(c *gin.Context), func()) {

    rbmq := new(rabbitmq.RabbitMQ)
	err := rbmq.Connect()
	if err != nil {
		fmt.Println("链接shibai", err)
		return nil, nil
	}
	return func(c *gin.Context) {
        // 业务逻辑
    }, func() { defer rbmq.Close() }
}
```
如此写法其实是在gin的router初始化的时候，就对rabbitmq进行了连接，而且我们把连接断开的close方法也作为闭包的方式一并返回，在router层我们可以显示的去调用close方法.
这样我们保证了只在服务退出的时候，关闭连接