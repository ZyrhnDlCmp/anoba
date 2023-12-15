### Note
Create your own branch, then push your own changes in your branch to avoid conflict


**Set up**
```sh
npm i
composer update
```

**Generate key**
```sh
php artisan key:generate
```

**Reset database**
```sh
php artisan db:wipe
```

***Run migrations**
```sh
php artisan migrate
```

**Seed database**
```sh
php artisan db:seed
```

**Run project**
```sh
php artisan serve
npm run dev
```


## Not necessary, just notes

**Run tests**
```sh
vendor\bin\phpunit
```

**Build for production**
```sh
npm run prod
cp .env.example .env
php artisan config:cache
php artisan route:cache
php artisan optimize
```

**Make model**
```sh
php artisan make:model Status
php artisan make:migration create_status
```

**Make controller**
```sh
php artisan make:controller StatusController
