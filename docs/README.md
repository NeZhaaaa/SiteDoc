# Lumen

## 创建工程

> 

## 处理跨域

> 在bootstrap/app.php中添加应用的全局中间件

```php
$app->middleware([
    App\Http\Middleware\ExampleMiddleware::class
]);
```

> 在中间件的handler方法中增加允许跨域的方法

```php
        $response = $next($request);
        $origin = $request->server('HTTP_ORIGIN') ? $request->server('HTTP_ORIGIN') : '';
        //允许访问的origin        
        $allow_origin = [
            'http://localhost:8080',
            'http://localhost:9528',
            'http://localhost',
        ];
        if (in_array($origin, $allow_origin)) {
            $response->header('Access-Control-Allow-Origin', $origin);
            $response->header('Access-Control-Allow-Headers', 'Origin, Content-Type, Cookie, X-Token, X-CSRF-TOKEN, Accept, Authorization, X-XSRF-TOKEN');
            $response->header('Access-Control-Expose-Headers', 'Authorization, authenticated');
            $response->header('Access-Control-Allow-Methods', 'GET, POST, PATCH, PUT, OPTIONS');
            $response->header('Access-Control-Allow-Credentials', 'true');
        }
        return $response;
```



> Lumen没有像Laravel一样处理跨域请求中的options请求，需要在bootstrap/app.php中添加

```php
$app->router->group([
    'namespace' => 'App\Http\Controllers',
], function ($router) {
    $router->options('/{path:.*}', function ($path) {});//加这一行
    require __DIR__.'/../routes/web.php';
});
```

# vue

## axios

> axios默认提交请求是参数是拼接成url参数，且Content-Type为json



```js
//参数字段用param时，参数拼接在url后面,http://xxx?name=param
axios(
{
  method:'post'
  url:"http://xxx",
  param:{
  	name:'param'
	}
}
)

//用data的时候，参数在请求的body里
axios(
{
  method:'post'
  url:"http://xxx",
  data:{
  	name:'data'
	}
}
)
```

# 工具

## Logo制作

> https://logomakr.com/