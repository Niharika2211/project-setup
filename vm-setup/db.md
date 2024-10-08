# Expense App Database Setup


## 1. Install MySQL Server
```bash
dnf install mysql-server -y
```

## 2. Enable and Start MySQL Service
Enable the MySQL service to start on boot and immediately start it:
```bash
systemctl enable mysqld
systemctl start mysqld
```

## 3. Secure MySQL Installation
Set a root password for MySQL (in this example, the password is `ExpenseApp@1`):
```bash
mysql_secure_installation --set-root-pass ExpenseApp@1
```

## 4. Clone the Expense Schema Repository
Clone the repository containing the database schema:
```bash
git clone https://github.com/Niharika2211/expense-schema.git
```

## 5. Import the Schema into MySQL
Navigate to the directory where the `expense-schema.sql` file is located, then import the SQL schema into MySQL:
```bash
mysql < backend.sql
```

## 6. Verify the Database Setup
### List all databases:
```sql
SHOW DATABASES;
```

### Select the `transactions` database:
```sql
USE transactions;
```

### Show tables:
```sql
SHOW TABLES;
```

### Query the `transactions` table:
```sql
SELECT * FROM transactions;
```

## 7. Check MySQL Network and Process Status
### View MySQL network listeners:
```bash
netstat -lntp
```

### Check MySQL logs:
```bash
journalctl -u mysql
```

### Verify MySQL processes:
```bash
ps -ef | grep mysqld
```
