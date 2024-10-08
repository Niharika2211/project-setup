
# Expense App Backend Setup

This guide outlines the steps to install Node.js, clone the Expense App backend repository, and set up the backend as a service using systemd.

## 1. Install Node.js

Disable the default Node.js module and enable Node.js version 20:
```bash
dnf module disable nodejs -y
dnf module enable nodejs:20 -y
dnf install nodejs -y
```

## 2. Create a User for the Backend

Create a dedicated user for the backend service:
```bash
useradd expense
```

## 3. Clone the Backend Repository

Create the application directory, navigate to it, and clone the backend repository:
```bash
mkdir /app
git clone https://github.com/Niharika2211/expense-backend.git /app
```

## 4. Install Dependencies

Install the required Node.js packages for the backend:
```bash
npm install
```

## 5. Set Up systemd Service for Backend

Create a service file to manage the backend as a systemd service:
```bash
vim /etc/systemd/system/backend.service
```

Add the following content:

```ini
[Unit]
Description=Backend Service

[Service]
User=expense
Environment=DB_HOST="172.31.43.131"
Environment=DB_USER="expense"
Environment=DB_PWD="ExpenseApp@1"
Environment=DB_DATABASE="transactions"
ExecStart=/bin/node /app/expense-backend/index.js
SyslogIdentifier=backend

[Install]
WantedBy=multi-user.target
```

## 6. Enable and Start the Backend Service

Reload the systemd daemon, start the backend service, and enable it to start on boot:
```bash
systemctl daemon-reload
systemctl start backend
systemctl enable backend
```

## 7. Verify the Service Status

Check the status of the backend service:
```bash
systemctl status backend
```

## 8. Monitoring and Logs

### Monitor the service logs in real-time:
```bash
journalctl -u -f backend
```

### Verify network ports:
```bash
netstat -lntp
```

### Tail system messages:
```bash
tail -f /var/log/messages
```

## 9. Test the Endpoint

You can test if the backend service is running by accessing the health or transaction endpoint using:
```
http://<ip>:<port>/health
http://<ip>:<port>/transaction
```
