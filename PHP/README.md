# Các câu lệnh cơ bản của laravel

## 1. Composer

- Tải composer

```php
composer install
```

## 2. .Env

- Tạo file .env rồi tạo key:

```php
cp .env.example .env
php artisan key:generate
```

## 3. Nodejs

- Chạy nodejs:

```php
npm install
npm run watch
```

## 3. Server

- Chạy server

```php
php artisan serve
```

## 3. Laravel Mix

- Cài đặt laravel Mix và cài đặt xử lí môi trường

```php
npm install laravel-mix --save-dev
npm install cross-env --save-dev
```

- Cấu hình file package.json

```php
{
    "private": true,
    "type": "commonjs",
    "scripts": {
        "dev": "mix",
        "watch": "mix watch",
        "build": "mix --production"
    },
    "devDependencies": {
        "axios": "^1.6.4",
        "laravel-mix": "^6.0.49"
    }
}

```

- Ví dụ về file webpack.mix.js

```php
const mix = require("laravel-mix");

const css = "resources/css/";
const js = "resources/js/";
const libs = "resources/libs/";

mix.minify(
    [
        libs + "bootstrap-5.3.3-dist/css/bootstrap.min.css",
        libs + "bootstrap-icons-1.11.3/font/bootstrap-icons.min.css",
        libs + "fontawesome-free-6.5.2-web/css/all.min.css",
        libs + "chosen/chosen.min.css",
        css + "front/main.css",
    ],
    "public/css/front.min.css"
).version();

mix.minify(
    [
        libs + "bootstrap-5.3.3-dist/js/bootstrap.bundle.min.js",
        libs + "fontawesome-free-6.5.2-web/js/all.min.js",
        libs + "chosen/chosen.jquery.min.js",
    ],
    "public/js/front.min.js"
).version();

```
