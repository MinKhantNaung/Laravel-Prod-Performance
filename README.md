
# The Ultimate Performance For Laravel Apps

## **1. Use In-Built Performance Quick Wins**
```bash
php artisan optimize
php artisan config:cache
php artisan event:cache
php artisan route:cache
php artisan view:cache
```

## **2. Optimize Composer**
```bash
composer install --prefer-dist --no-dev -o
```

## **3. Choose The Right Drivers**
- For caching in production, developers recommend the in-memory cache drivers such as **Redis, Memcached, or DynamoDB.**

- For queueing, developers recommend the **Redis, SQS, or Beanstalkd drivers.**

- For sessions, developers recommend the **Database, Redis, Memcached, or DynamoDB drivers.**

##### Redis Configuration Guide

- If you are on Ubuntu,
```bash
sudo apt update
sudo apt install redis-server
```
- Check the Real Redis Service Name

```bash
systemctl list-units --type=service | grep redis
```

- If it shows something like redis-server.service, that's the actual name to use. Now Enable the Service
```bash
sudo systemctl enable redis-server
# Then start it
sudo systemctl start redis-server
# Check Status
sudo systemctl status redis-server
```
- Optional: Test Redis
```bash
redis-cli ping
# You will see 'PONG'
```
- Install Redis PHP Extension (with your PHP version)
```bash
sudo apt install php8.4-redis
```
- Then restart PHP
```bash
sudo systemctl restart php8.4-fpm
```
- Check Installed Extensions for PHP and see 'redis'
```bash
php8.3 -m
```
- Configure .env (for cache, session, queue)
```dotenv
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
```
- Clear and Warm Up Cache
```bash
php artisan config:clear
php artisan cache:clear
php artisan config:cache
```
- To test caching: (I will use Tinker)
```bash
php artisan tinker 
> Cache::put('foo', 'bar', 600);
> $value = Cache::get('foo');
= 'bar'

# Check Drivers
> config('cache.default')
= 'redis'

> config('session.driver')
= 'redis'
```
- Now, check Redis CLI directly:
```bash
redis-cli
keys *
```
- You should see keys.

## **4. Queue Your Time-Consuming Tasks**
## **5. Set Compression Headers On Text Format Files**
#### Enabling gzip compression in Nginx
- Edit the Nginx configuration file:
- Open your Nginx configuration (for a specific site):
```bash
sudo nano /etc/nginx/sites-available/your-site
```
- Enable gzip Compression:
- Look for the http block, and within it, you can add or modify the gzip settings
```bash
http {
    # Enable gzip compression
    gzip on;
    # Set compression level (1-9, 9 being the highest)
    gzip_comp_level 6;
    # Enable compression for response sizes larger than 1000 bytes
    gzip_min_length 1000;
    # Add a header to let browsers know the content is compressed
    gzip_vary on;
    gzip_types 
        text/plain
        text/css
        application/javascript
        application/json
        text/javascript
        application/x-javascript
        text/xml
        application/xml
        application/xml+rss
        font/woff2
        image/svg+xml;

    # Additional configuration...
}
```
- Save and Exit:
- Test and Reload Nginx:
```bash
sudo nginx -t
sudo systemctl reload nginx
```
- Verify Compression:
- In Google Chrome (your site), open the Developer Tools (right-click -> "Inspect"), go to the Network tab, and refresh the page. Check the "Content-Encoding" header for the file type (it should show gzip for compressed files).
## **6. Set Cache Headers On Static Assets**
   https://laravel.com/docs/12.x/responses#cache-control-middleware
## **7. Consider Using A CDN To Serve Assets**
## **8. Minify Your JS and CSS Code**
## **9. Use Cache Wisely**
## **10. Identify Your App's Performance Bottlenecks**

---

### Credits & Inspiration

This guide is built with help from:

- Laravel’s official docs
- Advice from experienced devs in the community
- Support from ChatGPT during development and troubleshooting

