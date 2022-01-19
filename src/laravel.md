# Laravel

## 認証 {#auth}

### Laravel 8 認証

公式
https://readouble.com/laravel/8.x/ja/fortify.html
https://readouble.com/laravel/8.x/ja/sanctum.html

認証の検討
https://qiita.com/kuriya/items/f9747b8c32656140d156

## Collections {#collections}

### chunk() から返り値を受け取る

何がしたかったか
- chunkの中(例でのforeach内)で処理ではなく、結果などをchunkの外で受けたい
- collectionのmapのようなことをchunkでしたい

こうした
- chunkの外に変数を用意
- 値渡しではなくリファレンス渡し（参照渡し）する。下記の例では`&$i`
- 参照渡し https://www.php.net/manual/ja/language.references.pass.php

```
 $i = 1;
 User::chunk(100, function ($items) use (&$i) {
   foreach ($items as $item) {
     // なんかの処理
     $i ++;
   }
 });
```

## Migration {#migration}

### Laravel migrationではtimestamp型のchangeが出来ない

version
- laravel 5.8.17
- mysql 5.7.30

記述内容
```
  Schema::table('table', function (Blueprint $table) {
   $table->timestamp('hoge')->comment('hoge')->change();
 });
```

エラー表示
```
 Doctrine\DBAL\DBALException  : Unknown column type "timestamp" requested. Any Doctrine type that you use has to be registered with \Doctrine\DBAL\Types\Type::addType(). You can get a list of all the known types with \Doctrine\DBAL\Types\Type::getTypesMap(). If this error occurs during database introspection then you might have forgotten to register all database types for a Doctrine Type. Use AbstractPlatform#registerDoctrineTypeMapping() or have your custom types implement Type#getMappedDatabaseTypes(). If the type name is empty you might have a problem with the cache or forgot some mapping information
```

解決方法
DBファサードを使う
```
  Schema::table('table', function (Blueprint $table) {
   DB::statement('ALTER TABLE `テーブル名` MODIFY COLUMN `カラム名` TIMESTAMP NULL;');
 });
```

## Artisanコンソール {#artisan}

### Tinker（REPL）

https://readouble.com/laravel/8.x/ja/artisan.html

> Tinkerを使用すると、Eloquentモデル、ジョブ、イベントなどを含む、コマンドラインでLaravelアプリケーション全体を操作できます。Tinker環境に入るには、tinkerArtisanコマンドを実行します。

```
php artisan tinker
```

#### デモUserの追加

```
$ php artisan tinker

App\Models\User::factory()->create(['email' => 'demo1@example.com']);
App\Models\User::factory()->create(['email' => 'demo2@example.com']);
App\Models\User::factory()->create(['email' => 'demo3@example.com']);
```

## Error Handling

### エラーログに追記する

version
- laravel 8.x

Doc: https://laravel.com/docs/8.x/errors#exception-log-context

app/Exceptions/Handler.php
```php
<?php

namespace App\Exceptions;

use Exception;
use Throwable;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Request;

class InvalidOrderException extends Exception
{
    // ...

    /**
     * Get the exception's context information.
     *
     * @return array
     */
    public function context()
    {
        try {
            return array_filter([
                'method' = Request::method();
                'url' => Request::fullUrl(),
                'input' => Request::except(['password', 'password_confirmation']),
                'userId' => Auth::id(),
                'email' => Auth::user() ? Auth::user()->email : null,
            ]);
        } catch (Throwable $e) {
            return [];
        }
    }
}
```

参考: https://stackoverflow.com/questions/35322037/error-log-on-laravel-5-with-the-url-where-error-occured
