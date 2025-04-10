
# The Ultimate Performance For Laravel Apps

1. **Use In-Built Performance Quick Wins**
```bash
php artisan optimize
php artisan config:cache
php artisan event:cache
php artisan route:cache
php artisan view:cache
```

2. **Optimize Composer**
```bash
composer install --prefer-dist --no-dev -o
```

3. **Choose The Right Drivers**
- For caching in production, we recommend the in-memory cache drivers such as Redis, Memcached, or DynamoDB.

- For queueing, we recommend the Redis, SQS, or Beanstalkd drivers.

- For sessions, we recommend the Database, Redis, Memcached, or DynamoDB drivers.

4. **Queue Your Time-Consuming Tasks**
5. **Set Compression Headers On Text Format Files**
6. **Set Cache Headers On Static Assets**
   https://laravel.com/docs/12.x/responses#cache-control-middleware
7. **Consider Using A CDN To Serve Assets**
8. **Minify Your JS and CSS Code**
9. **Use Cache Wisely**
10. **Identify Your App's Performance Bottlenecks**

