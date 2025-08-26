﻿# Day 4: Static Website Hosting with Nginx

This project demonstrates how to host a static website using **Nginx** on **SUSE Linux** and **Amazon Linux**. It's a lightweight, production-ready setup ideal for portfolios, documentation, or internal dashboards.

## 📋 Table of Contents

- [Prerequisites](#-prerequisites)
- [SUSE Linux Deployment](#-suse-linux-deployment)
- [Amazon Linux Deployment](#-amazon-linux-deployment)
- [Troubleshooting](#-troubleshooting)
- [Best Practices](#-best-practices)
- [Next Steps](#-next-steps)

---

## 📦 Prerequisites

### For SUSE Linux
- SUSE Linux (SLES/SLED or openSUSE)
- Basic HTML file (e.g., `index.html`)
- Root or sudo access
- Internet connection for package installation

### For Amazon Linux
- Amazon Linux EC2 instance
- Security group configured to allow HTTP (port 80) traffic
- Basic HTML file (e.g., `index.html`)
- Root or sudo access

---

## 🐧 SUSE Linux Deployment

### Step 1: Install Nginx

```bash
# Update package repository
sudo zypper refresh

# Install Nginx
sudo zypper install nginx
```

### Step 2: Create Your Static Website Directory

```bash
# Create website directory
sudo mkdir -p /srv/www/my-website

# Navigate to your website files
cd Static-website

# Move all files to the web directory
sudo mv * /srv/www/my-website/

# Set proper permissions
sudo chown -R nginx:nginx /srv/www/my-website
sudo chmod -R 755 /srv/www/my-website
```

**Important:** Ensure `index.html` is present in the directory.

### Step 3: Configure Nginx

Create a new server block configuration:

```bash
sudo vim /etc/nginx/conf.d/my-website.conf
```

Add the following configuration:

```nginx
server {
    listen 80;
    server_name localhost;

    root /srv/www/my-website;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
}
```

### Step 4: Enable and Start Nginx

```bash
# Enable Nginx to start on boot
sudo systemctl enable nginx

# Start Nginx service
sudo systemctl start nginx

# Check service status
sudo systemctl status nginx
```

### Step 5: Test Your Setup

Open a browser and navigate to:
- `http://<your-server-ip>`
- `http://<your-ec2-public-ip>`

You should see your static website's homepage!

---

## ☁️ Amazon Linux Deployment

### Step 1: Update System and Install Nginx

```bash
# Update package lists
sudo yum update -y

# Install Nginx
sudo yum install nginx -y

# Verify installation
sudo systemctl status nginx
```

### Step 2: Host Your Website

You have two options for deploying your website:

#### Option A: Clone from GitHub

```bash
# Remove default Nginx page
sudo rm /var/www/html/index.nginx-debian.html

# Clone repository directly to web root
sudo git clone https://github.com/devilraj98/free-css-website.git /var/www/html
```

#### Option B: Use Website Template

```bash
# Navigate to home directory
cd ~

# Download template
wget https://templatemo.com/download/templatemo_578_first_portfolio

# Install unzip if not available
sudo yum install unzip -y

# Rename and extract
mv templatemo_578_first_portfolio templatemo_578_first_portfolio.zip
unzip templatemo_578_first_portfolio.zip

# Move files to web root
cd templatemo_578_first_portfolio
sudo mv * /usr/share/nginx/html
```

### Step 3: Configure Security Group

Ensure your EC2 security group allows:
- **HTTP (Port 80)** - for web traffic
- **HTTPS (Port 443)** - if using SSL (recommended)

### Step 4: Test Your Website

Navigate to your EC2 instance's public IP address in a web browser.

---

## 🔧 Troubleshooting

### Common Issues and Solutions

#### Nginx Won't Start
```bash
# Check Nginx configuration syntax
sudo nginx -t

# View error logs
sudo journalctl -u nginx -f
```

#### Permission Denied Errors
```bash
# Fix file permissions
sudo chown -R nginx:nginx /srv/www/my-website
sudo chmod -R 755 /srv/www/my-website
```

#### Website Not Loading
1. Check if Nginx is running: `sudo systemctl status nginx`
2. Verify firewall settings: `sudo firewall-cmd --list-all`
3. Check security group rules (Amazon Linux)
4. Verify file paths in Nginx configuration

#### 404 Errors
- Ensure `index.html` exists in the web root
- Check file permissions
- Verify Nginx configuration file paths

### Useful Commands

```bash
# Reload Nginx configuration
sudo systemctl reload nginx

# View Nginx error logs
sudo tail -f /var/log/nginx/error.log

# View Nginx access logs
sudo tail -f /var/log/nginx/access.log

# Test Nginx configuration
sudo nginx -t
```

---

## 🚀 Best Practices

### Security
- Keep Nginx updated regularly
- Use HTTPS with Let's Encrypt certificates
- Implement security headers
- Restrict file permissions
- Use a firewall (firewalld/ufw)

### Performance
- Enable gzip compression
- Use browser caching
- Optimize images and assets
- Consider CDN for static assets

---

## 📝 Next Steps (Optional)

### Add HTTPS with Let's Encrypt

```bash
# Install certbot
sudo zypper install certbot python3-certbot-nginx  # SUSE
sudo yum install certbot python3-certbot-nginx     # Amazon Linux

# Obtain SSL certificate
sudo certbot --nginx -d yourdomain.com
```

### Set Up Auto-Deployment with GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Server
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Deploy to server
        uses: appleboy/ssh-action@v0.1.4
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          key: ${{ secrets.KEY }}
          script: |
            cd /srv/www/my-website
            git pull origin main
            sudo systemctl reload nginx
```

### Custom Domain Setup
1. Purchase a domain name
2. Point DNS A record to your server IP
3. Update Nginx configuration with domain name
4. Obtain SSL certificate for the domain

---

## 📚 Additional Resources

- [Nginx Official Documentation](https://nginx.org/en/docs/)
- [SUSE Linux Documentation](https://www.suse.com/documentation/)
- [Amazon Linux Documentation](https://docs.aws.amazon.com/linux/)
- [Let's Encrypt Documentation](https://letsencrypt.org/docs/)

---

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

