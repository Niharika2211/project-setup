
# Expense App Frontend and Nginx Setup

This guide walks you through the process of setting up Nginx to serve the frontend and proxy API requests to the backend.


## 1. Install Nginx

Install Nginx and enable it to start on boot:
```bash
dnf install nginx -y
systemctl enable nginx
systemctl start nginx
```

## 2. Remove Default Nginx Files

Clear the default Nginx directory:
```bash
rm -rf /usr/share/nginx/html/*
```

## 3. Clone the Frontend Repository

Navigate to the Nginx directory and clone the Expense App frontend:
```bash
git clone https://github.com/Niharika2211/expense-frontend.git /usr/share/nginx/html/
```

## 4. Configure Nginx for Proxy and Health Check

Create a new configuration file to handle API requests and health checks:
```bash
vim /etc/nginx/default.d/expense.conf
```

Add the following configuration:

```nginx
proxy_http_version 1.1;

location /api/ {
    proxy_pass http://localhost:8080/;  # Backend service running on port 8080
}

location /health {
    stub_status on;
    access_log off;
}
```

- The `/api/` location proxies all API requests to the backend service running on port `8080`.
- The `/health` location provides a simple status page for Nginx.

## 5. Test Nginx Configuration and Restart

Test the Nginx configuration for any errors:
```bash
nginx -t
```

If the test passes, restart Nginx to apply the changes:
```bash
systemctl restart nginx
```

## 6. Verify Nginx Service and Logs

### Check Nginx Listening Ports:
```bash
netstat -lntp
```

### Monitor Nginx Access Logs:
```bash
tail -f /var/log/nginx/access.log
```

### Monitor Nginx Error Logs:
```bash
tail -f /var/log/nginx/error.log
```

## 7. Default Nginx Configuration (Optional)

To view or edit the main Nginx configuration file:
```bash
vim /etc/nginx/nginx.conf
```
