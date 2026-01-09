# Brotli Compression Setup for Nginx

This guide walks you through enabling Brotli compression in Nginx on Ubuntu 24.04. Brotli provides better compression ratios than gzip, resulting in faster page loads and reduced bandwidth usage.

## Prerequisites

- Ubuntu 24.04
- Root or sudo access

## Installation Steps

### 1. Update System Packages

```bash
sudo apt update
```

### 2. Install Nginx

```bash
sudo apt install -y nginx
```

### 3. Install Brotli Modules

Install the Nginx Brotli modules for dynamic and static compression:

```bash
sudo apt install -y \
  libnginx-mod-http-brotli-filter \
  libnginx-mod-http-brotli-static
```

- `libnginx-mod-http-brotli-filter`: Compresses responses on-the-fly
- `libnginx-mod-http-brotli-static`: Serves pre-compressed `.br` files

## Configuration

### 4. Edit Nginx Configuration

Open the main Nginx configuration file:

```bash
sudo vim /etc/nginx/nginx.conf
```

Add the following Brotli settings inside the `http` block:

```nginx
##
# Brotli Settings
##

brotli on;
brotli_comp_level 6;
brotli_static on;
brotli_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
```

**Configuration Options:**
- `brotli on`: Enables dynamic Brotli compression
- `brotli_comp_level 6`: Sets compression level (0-11, default is 6)
- `brotli_static on`: Enables serving pre-compressed static files
- `brotli_types`: Specifies MIME types to compress

### 5. Restart Nginx

Apply the configuration changes:

```bash
sudo systemctl restart nginx
```

## Verification

Test if Brotli compression is working:

```bash
curl -H "Accept-Encoding: br" -I http://127.0.0.1
```

Look for the `Content-Encoding: br` header in the response. If present, Brotli compression is working correctly.

## Additional Commands

Check Nginx status:
```bash
sudo systemctl status nginx
```

Test Nginx configuration:
```bash
sudo nginx -t
```

View Nginx error logs:
```bash
sudo tail -f /var/log/nginx/error.log
```

## Troubleshooting

If Brotli isn't working:
1. Verify the modules are loaded: `nginx -V 2>&1 | grep brotli`
2. Check for configuration errors: `sudo nginx -t`
3. Ensure your test requests include the `Accept-Encoding: br` header
4. Review Nginx error logs for any issues

## Resources

- [Nginx Brotli Module Documentation](https://github.com/google/ngx_brotli)
- [Brotli Compression Algorithm](https://github.com/google/brotli)

