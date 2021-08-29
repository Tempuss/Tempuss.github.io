---
layout: post
title: Laravel에서 PHP CLI 실행
date: 2018-12-20 16:06:00 +0900
category: Web 
---


```
<?php
define('LARAVEL_START', microtime(true));

require __DIR__.'/../../vendor/autoload.php';


$app = require_once __DIR__.'/../../bootstrap/app.php';

$kernel = $app->make(Illuminate\Contracts\Http\Kernel::class);

$response = $kernel->handle(
$request = Illuminate\Http\Request::capture()
);

$kernel->terminate($request, $response);


//클래스 생성
$elaClass = new \App\Http\Controllers\ElasticController();

//커넥션 생성
$elaClass->setClient();

//Data insert
$elaClass->insertCount();


```

라라벨에 컨트롤러로 등록된 코드를 cli로 실행하고 싶을 경우엔 위 코드대로 따로 파일을 만들어 실행하면 된다

다만 require와 require_once 부분의 경우 달라질수 있는데 상위 디렉토리로 올라갈때 laravel 루트 디렉토리가 되어야 한다

예를 들어 보자



DOCUMENT_ROOT는 /var/www/laravel/public 디렉토리이고 
위의 파일읜 /var/www/larvel/module/cli 디렉토리에 있을 경우 위 소스코드처럼 ../../ 두단계 상위디렉토리로 이동하여 실행해야 한다

그 이후엔 일반적인 Class 생성 및 메소드 실행방법이랑 똑같다 
다만 CLI로 돌아가기 때문에 시각적으로 확인할 방법이 없으므로 따로 로그는 남기도록 해서 잘 작동하는지 확인 할 수 있는 방법을 마련해놓는게 좋다




CLI로 실행 할 경우 PHP 위의 코드가 있는 파일을 고대로 php로 실행 시키면 된다


```
php /var/www/laravel/module/cli/CliElastic.php
```


이렇게 실행시키면 laravel의 컨트롤러에 있는 코드를 cli로 실행 시킬수 있다


크론탭으로 등록 시키려 할경우엔 아래처럼 등록하면 2분마다 작동한다
```
*/2 * * * * php /var/www/laravel/module/cli/CliElastic.php
```


이렇게 하면 매 1분 마다 실행된다


```
* * * * * php /var/www/laravel/module/cli/CliElastic.php

```

