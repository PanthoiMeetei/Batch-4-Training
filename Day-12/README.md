# Day 12: Advanced MySQL on EC2 & Production Database Management

## 📚 Learning Objectives
- Master advanced MySQL configurations on EC2
- Implement production-grade database security
- Practice complex CRUD operations and transactions
- Learn database performance optimization
- Understand backup and disaster recovery strategies

## 🎯 Advanced MySQL Implementation

### Production-Ready MySQL Setup
Building on Day 11's foundation, today we'll create a production-grade MySQL environment with advanced features, security hardening, and performance optimization.

### Architecture Overview
```
Internet → Load Balancer → EC2 Instances → MySQL Master/Slave
    ↓
Advanced Features:
├── SSL/TLS Encryption
├── Master-Slave Replication
├── Automated Backups
├── Performance Monitoring
└── Security Hardening
```

## 🛠️ Advanced Lab: Production MySQL Environment

### Prerequisites
- Completed Day 11 MySQL basics
- Two EC2 instances (Master and Slave)
- Advanced security group configuration
- SSL certificates for encryption

### Step 1: Launch Production EC2 Instances

```bash
# Master Instance Configuration
Name: mysql-master-prod
AMI: Amazon Linux 2023
Instance Type: t3.small (better performance)
Storage: 20GB gp3 with encryption
Security Group: mysql-prod-sg

# Slave Instance Configuration  
Name: mysql-slave-prod
AMI: Amazon Linux 2023
Instance Type: t3.small
Storage: 20GB gp3 with encryption
Security Group: mysql-prod-sg
```

**Advanced Security Group Rules:**
```
Inbound Rules:
- SSH (22): Your IP only
- MySQL (3306): Internal VPC only
- Custom TCP (33060): MySQL X Protocol
- HTTPS (443): Application servers

Outbound Rules:
- All traffic: 0.0.0.0/0 (for updates and replication)
```

### Step 2: Advanced MySQL Installation and Configuration

```bash
# Connect to Master instance
ssh -i your-key.pem ec2-user@master-ip

# Install MySQL 8.0 with additional tools
sudo yum update -y
sudo yum install mysql-server mysql-client -y

# Install performance monitoring tools
sudo yum install htop iotop sysstat -y

# Start and enable MySQL
sudo systemctl start mysqld
sudo systemctl enable mysqld

# Configure MySQL for production
sudo mysql_secure_installation
```

### Step 3: Production MySQL Configuration

```bash
# Edit MySQL configuration file
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

# Add production configurations:
```

```ini
[mysqld]
# Basic Settings
bind-address = 0.0.0.0
port = 3306
datadir = /var/lib/mysql
socket = /var/run/mysqld/mysqld.sock

# Performance Tuning
innodb_buffer_pool_size = 1G
innodb_log_file_size = 256M
innodb_flush_log_at_trx_commit = 2
query_cache_size = 128M
max_connections = 200
thread_cache_size = 16

# Security Settings
ssl-ca = /etc/mysql/ssl/ca-cert.pem
ssl-cert = /etc/mysql/ssl/server-cert.pem
ssl-key = /etc/mysql/ssl/server-key.pem
require_secure_transport = ON

# Logging
general_log = ON
general_log_file = /var/log/mysql/general.log
slow_query_log = ON
slow_query_log_file = /var/log/mysql/slow.log
long_query_time = 2

# Replication Settings (Master)
server-id = 1
log-bin = mysql-bin
binlog_format = ROW
expire_logs_days = 7
```

### Step 4: Create Production Database Schema

```sql
-- Connect to MySQL
mysql -u root -p

-- Create production database
CREATE DATABASE ecommerce_prod;
USE ecommerce_prod;

-- Create comprehensive tables
CREATE TABLE categories (
    category_id INT PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(100) NOT NULL,
    description TEXT,
    parent_category_id INT,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    INDEX idx_parent_category (parent_category_id),
    INDEX idx_active (is_active)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(200) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    cost_price DECIMAL(10,2),
    stock_quantity INT DEFAULT 0,
    category_id INT,
    sku VARCHAR(50) UNIQUE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(category_id),
    INDEX idx_category (category_id),
    INDEX idx_sku (sku),
    INDEX idx_price (price),
    INDEX idx_active (is_active)
);

CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(20),
    address TEXT,
    city VARCHAR(50),
    state VARCHAR(50),
    zip_code VARCHAR(10),
    country VARCHAR(50) DEFAULT 'USA',
    date_of_birth DATE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    INDEX idx_email (email),
    INDEX idx_name (first_name, last_name),
    INDEX idx_location (city, state)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT NOT NULL,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10,2) NOT NULL,
    tax_amount DECIMAL(10,2) DEFAULT 0,
    shipping_amount DECIMAL(10,2) DEFAULT 0,
    discount_amount DECIMAL(10,2) DEFAULT 0,
    status ENUM('pending', 'processing', 'shipped', 'delivered', 'cancelled') DEFAULT 'pending',
    shipping_address TEXT,
    payment_method VARCHAR(50),
    payment_status ENUM('pending', 'paid', 'failed', 'refunded') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    INDEX idx_customer (customer_id),
    INDEX idx_order_date (order_date),
    INDEX idx_status (status),
    INDEX idx_payment_status (payment_status)
);

CREATE TABLE order_items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    total_price DECIMAL(10,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(order_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    INDEX idx_order (order_id),
    INDEX idx_product (product_id)
);
```

### Step 5: Advanced CRUD Operations

#### Complex INSERT Operations

```sql
-- Insert sample categories
INSERT INTO categories (category_name, description) VALUES
('Electronics', 'Electronic devices and accessories'),
('Clothing', 'Apparel and fashion items'),
('Books', 'Books and educational materials'),
('Home & Garden', 'Home improvement and garden supplies'),
('Sports', 'Sports equipment and accessories');

-- Insert subcategories
INSERT INTO categories (category_name, description, parent_category_id) VALUES
('Smartphones', 'Mobile phones and accessories', 1),
('Laptops', 'Portable computers', 1),
('Men\'s Clothing', 'Clothing for men', 2),
('Women\'s Clothing', 'Clothing for women', 2);

-- Insert products with complex data
INSERT INTO products (product_name, description, price, cost_price, stock_quantity, category_id, sku) VALUES
('iPhone 15 Pro', 'Latest Apple smartphone with advanced features', 999.99, 750.00, 50, 6, 'IPH15PRO001'),
('MacBook Air M2', 'Lightweight laptop with M2 chip', 1199.99, 900.00, 25, 7, 'MBA-M2-001'),
('Nike Air Max', 'Comfortable running shoes', 129.99, 80.00, 100, 5, 'NIKE-AM-001'),
('Samsung Galaxy S24', 'Android smartphone with AI features', 899.99, 650.00, 75, 6, 'SGS24-001');

-- Insert customers
INSERT INTO customers (first_name, last_name, email, phone, address, city, state, zip_code) VALUES
('John', 'Smith', 'john.smith@email.com', '555-0101', '123 Main St', 'New York', 'NY', '10001'),
('Sarah', 'Johnson', 'sarah.j@email.com', '555-0102', '456 Oak Ave', 'Los Angeles', 'CA', '90210'),
('Mike', 'Brown', 'mike.brown@email.com', '555-0103', '789 Pine St', 'Chicago', 'IL', '60601'),
('Emily', 'Davis', 'emily.davis@email.com', '555-0104', '321 Elm St', 'Houston', 'TX', '77001');
```

#### Advanced SELECT Queries

```sql
-- Complex JOIN with aggregations
SELECT 
    c.category_name,
    COUNT(p.product_id) as product_count,
    AVG(p.price) as avg_price,
    MIN(p.price) as min_price,
    MAX(p.price) as max_price,
    SUM(p.stock_quantity) as total_stock
FROM categories c
LEFT JOIN products p ON c.category_id = p.category_id
WHERE c.parent_category_id IS NULL
GROUP BY c.category_id, c.category_name
HAVING product_count > 0
ORDER BY avg_price DESC;

-- Customer order analysis
SELECT 
    CONCAT(cu.first_name, ' ', cu.last_name) as customer_name,
    COUNT(o.order_id) as total_orders,
    SUM(o.total_amount) as total_spent,
    AVG(o.total_amount) as avg_order_value,
    MAX(o.order_date) as last_order_date
FROM customers cu
LEFT JOIN orders o ON cu.customer_id = o.customer_id
GROUP BY cu.customer_id, cu.first_name, cu.last_name
ORDER BY total_spent DESC;

-- Product performance analysis
SELECT 
    p.product_name,
    p.price,
    p.stock_quantity,
    COALESCE(SUM(oi.quantity), 0) as total_sold,
    COALESCE(SUM(oi.total_price), 0) as total_revenue,
    c.category_name
FROM products p
LEFT JOIN order_items oi ON p.product_id = oi.product_id
LEFT JOIN categories c ON p.category_id = c.category_id
GROUP BY p.product_id, p.product_name, p.price, p.stock_quantity, c.category_name
ORDER BY total_revenue DESC;
```

#### Transaction Management

```sql
-- Complex order creation with transaction
START TRANSACTION;

-- Insert order
INSERT INTO orders (customer_id, total_amount, tax_amount, shipping_amount, status, payment_method)
VALUES (1, 1329.98, 106.40, 15.99, 'processing', 'credit_card');

SET @order_id = LAST_INSERT_ID();

-- Insert order items
INSERT INTO order_items (order_id, product_id, quantity, unit_price, total_price) VALUES
(@order_id, 1, 1, 999.99, 999.99),
(@order_id, 3, 1, 129.99, 129.99);

-- Update product stock
UPDATE products SET stock_quantity = stock_quantity - 1 WHERE product_id = 1;
UPDATE products SET stock_quantity = stock_quantity - 1 WHERE product_id = 3;

-- Verify stock levels
SELECT product_id, product_name, stock_quantity 
FROM products 
WHERE product_id IN (1, 3) AND stock_quantity >= 0;

-- Commit if everything is successful
COMMIT;

-- If there's an error, rollback
-- ROLLBACK;
```

### Step 6: Performance Optimization

#### Query Optimization

```sql
-- Analyze slow queries
SELECT 
    query_time,
    lock_time,
    rows_sent,
    rows_examined,
    sql_text
FROM mysql.slow_log
ORDER BY query_time DESC
LIMIT 10;

-- Create composite indexes for better performance
CREATE INDEX idx_orders_customer_date ON orders(customer_id, order_date);
CREATE INDEX idx_products_category_price ON products(category_id, price);
CREATE INDEX idx_customers_location_active ON customers(city, state, is_active);

-- Analyze query execution plans
EXPLAIN SELECT 
    p.product_name,
    SUM(oi.quantity) as total_sold
FROM products p
JOIN order_items oi ON p.product_id = oi.product_id
JOIN orders o ON oi.order_id = o.order_id
WHERE o.order_date >= '2024-01-01'
GROUP BY p.product_id, p.product_name
ORDER BY total_sold DESC;
```

#### Database Maintenance

```sql
-- Optimize tables
OPTIMIZE TABLE products, customers, orders, order_items;

-- Analyze table statistics
ANALYZE TABLE products, customers, orders, order_items;

-- Check table status
SHOW TABLE STATUS LIKE 'products';

-- Monitor database size
SELECT 
    table_schema as 'Database',
    table_name as 'Table',
    ROUND(((data_length + index_length) / 1024 / 1024), 2) as 'Size (MB)'
FROM information_schema.tables
WHERE table_schema = 'ecommerce_prod'
ORDER BY (data_length + index_length) DESC;
```

### Step 7: Advanced Security Implementation

#### User Management and Privileges

```sql
-- Create application users with specific privileges
CREATE USER 'app_read'@'%' IDENTIFIED BY 'ReadOnlyPass123!';
CREATE USER 'app_write'@'%' IDENTIFIED BY 'WritePass123!';
CREATE USER 'app_admin'@'localhost' IDENTIFIED BY 'AdminPass123!';

-- Grant specific privileges
GRANT SELECT ON ecommerce_prod.* TO 'app_read'@'%';
GRANT SELECT, INSERT, UPDATE ON ecommerce_prod.* TO 'app_write'@'%';
GRANT ALL PRIVILEGES ON ecommerce_prod.* TO 'app_admin'@'localhost';

-- Create role-based access
CREATE ROLE 'ecommerce_reader';
CREATE ROLE 'ecommerce_writer';
CREATE ROLE 'ecommerce_admin';

GRANT SELECT ON ecommerce_prod.* TO 'ecommerce_reader';
GRANT SELECT, INSERT, UPDATE, DELETE ON ecommerce_prod.* TO 'ecommerce_writer';
GRANT ALL PRIVILEGES ON ecommerce_prod.* TO 'ecommerce_admin';

FLUSH PRIVILEGES;
```

#### SSL/TLS Configuration

```bash
# Generate SSL certificates
sudo mkdir -p /etc/mysql/ssl
cd /etc/mysql/ssl

# Create CA certificate
sudo openssl genrsa 2048 > ca-key.pem
sudo openssl req -new -x509 -nodes -days 3600 -key ca-key.pem -out ca-cert.pem

# Create server certificate
sudo openssl req -newkey rsa:2048 -days 3600 -nodes -keyout server-key.pem -out server-req.pem
sudo openssl rsa -in server-key.pem -out server-key.pem
sudo openssl x509 -req -in server-req.pem -days 3600 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 -out server-cert.pem

# Set proper permissions
sudo chown mysql:mysql /etc/mysql/ssl/*
sudo chmod 600 /etc/mysql/ssl/*-key.pem
sudo chmod 644 /etc/mysql/ssl/*-cert.pem

# Restart MySQL
sudo systemctl restart mysqld
```

### Step 8: Backup and Recovery Strategies

#### Automated Backup Script

```bash
#!/bin/bash
# backup-mysql.sh

# Configuration
DB_NAME="ecommerce_prod"
DB_USER="backup_user"
DB_PASS="BackupPass123!"
BACKUP_DIR="/opt/mysql-backups"
DATE=$(date +%Y%m%d_%H%M%S)
RETENTION_DAYS=7

# Create backup directory
mkdir -p $BACKUP_DIR

# Full database backup
mysqldump -u $DB_USER -p$DB_PASS \
  --single-transaction \
  --routines \
  --triggers \
  --events \
  --hex-blob \
  $DB_NAME > $BACKUP_DIR/${DB_NAME}_full_$DATE.sql

# Compress backup
gzip $BACKUP_DIR/${DB_NAME}_full_$DATE.sql

# Remove old backups
find $BACKUP_DIR -name "*.sql.gz" -mtime +$RETENTION_DAYS -delete

# Log backup completion
echo "$(date): Backup completed for $DB_NAME" >> /var/log/mysql-backup.log
```

#### Point-in-Time Recovery Setup

```sql
-- Enable binary logging for point-in-time recovery
SET GLOBAL binlog_format = 'ROW';
SET GLOBAL expire_logs_days = 7;

-- Show binary logs
SHOW BINARY LOGS;

-- Show master status
SHOW MASTER STATUS;

-- Create recovery point
FLUSH LOGS;
```

### Step 9: Monitoring and Alerting

#### Performance Monitoring Queries

```sql
-- Monitor active connections
SELECT 
    USER,
    HOST,
    DB,
    COMMAND,
    TIME,
    STATE,
    INFO
FROM INFORMATION_SCHEMA.PROCESSLIST
WHERE COMMAND != 'Sleep'
ORDER BY TIME DESC;

-- Monitor table locks
SELECT 
    r.trx_id waiting_trx_id,
    r.trx_mysql_thread_id waiting_thread,
    r.trx_query waiting_query,
    b.trx_id blocking_trx_id,
    b.trx_mysql_thread_id blocking_thread,
    b.trx_query blocking_query
FROM information_schema.innodb_lock_waits w
INNER JOIN information_schema.innodb_trx b ON b.trx_id = w.blocking_trx_id
INNER JOIN information_schema.innodb_trx r ON r.trx_id = w.requesting_trx_id;

-- Monitor database size growth
SELECT 
    table_schema,
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 1) AS 'DB Size in MB'
FROM information_schema.tables
GROUP BY table_schema;
```

## 🎯 Production Scenarios

### Scenario 1: High-Traffic Order Processing

```sql
-- Optimized order creation for high traffic
DELIMITER //
CREATE PROCEDURE ProcessOrder(
    IN p_customer_id INT,
    IN p_product_id INT,
    IN p_quantity INT,
    OUT p_order_id INT,
    OUT p_status VARCHAR(50)
)
BEGIN
    DECLARE v_price DECIMAL(10,2);
    DECLARE v_stock INT;
    DECLARE v_total DECIMAL(10,2);
    
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        SET p_status = 'ERROR';
    END;
    
    START TRANSACTION;
    
    -- Check product availability
    SELECT price, stock_quantity INTO v_price, v_stock
    FROM products 
    WHERE product_id = p_product_id AND is_active = TRUE
    FOR UPDATE;
    
    IF v_stock >= p_quantity THEN
        SET v_total = v_price * p_quantity;
        
        -- Create order
        INSERT INTO orders (customer_id, total_amount, status)
        VALUES (p_customer_id, v_total, 'processing');
        
        SET p_order_id = LAST_INSERT_ID();
        
        -- Add order item
        INSERT INTO order_items (order_id, product_id, quantity, unit_price, total_price)
        VALUES (p_order_id, p_product_id, p_quantity, v_price, v_total);
        
        -- Update stock
        UPDATE products 
        SET stock_quantity = stock_quantity - p_quantity
        WHERE product_id = p_product_id;
        
        COMMIT;
        SET p_status = 'SUCCESS';
    ELSE
        ROLLBACK;
        SET p_status = 'INSUFFICIENT_STOCK';
    END IF;
END //
DELIMITER ;

-- Test the procedure
CALL ProcessOrder(1, 1, 2, @order_id, @status);
SELECT @order_id, @status;
```

### Scenario 2: Customer Analytics Dashboard

```sql
-- Customer segmentation analysis
SELECT 
    CASE 
        WHEN total_spent >= 1000 THEN 'Premium'
        WHEN total_spent >= 500 THEN 'Gold'
        WHEN total_spent >= 100 THEN 'Silver'
        ELSE 'Bronze'
    END as customer_segment,
    COUNT(*) as customer_count,
    AVG(total_spent) as avg_spent,
    AVG(order_count) as avg_orders
FROM (
    SELECT 
        c.customer_id,
        COALESCE(SUM(o.total_amount), 0) as total_spent,
        COUNT(o.order_id) as order_count
    FROM customers c
    LEFT JOIN orders o ON c.customer_id = o.customer_id
    GROUP BY c.customer_id
) customer_stats
GROUP BY customer_segment
ORDER BY avg_spent DESC;
```

## 🏆 Lab Completion Checklist

- [ ] Production MySQL environment configured
- [ ] Advanced security measures implemented
- [ ] Complex database schema created
- [ ] Advanced CRUD operations performed
- [ ] Transaction management tested
- [ ] Performance optimization applied
- [ ] SSL/TLS encryption configured
- [ ] Automated backup system implemented
- [ ] Monitoring queries executed
- [ ] Production scenarios tested

## 📚 Key Takeaways

1. **Production Configuration**: Proper MySQL tuning for performance
2. **Security Hardening**: SSL, user management, and access control
3. **Transaction Management**: ACID compliance for data integrity
4. **Performance Optimization**: Indexing and query optimization
5. **Backup Strategies**: Automated backups and point-in-time recovery
6. **Monitoring**: Proactive database health monitoring

---

**Next Day Preview**: Day 13 will cover AWS RDS (Relational Database Service) - Managed database services and migration from EC2 MySQL.

**Instructor**: Neeraj Kumar  
**Date**: Day 12 - AWS DevOps Batch 4  
**Duration**: 4 hours (Theory: 1 hour, Practical: 3 hours)

## 🎉 Congratulations!

You've successfully implemented a production-grade MySQL environment on AWS EC2 with advanced features, security, and performance optimization!