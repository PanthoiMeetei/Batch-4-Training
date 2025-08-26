# Day 4
This project demonstrates how to host a static website using **Nginx** on **SUSE Linux**. It's a lightweight, production-ready setup ideal for portfolios, documentation, or internal dashboards.

---

## 📦 Prerequisites

- SUSE Linux (tested on openSUSE Leap)
- Basic HTML file (e.g., `index.html`)
- Root or sudo access

---

## ⚙️ Installation Steps

### 1. Install Nginx

```bash
sudo zypper refresh
sudo zypper install nginx


- This installs Nginx from SUSE’s repositories.
- Confirm installation: nginx -v

📂 2. Create Your Static Website Directory
Let’s say your site files are in /home/neeraj/my-website.
sudo mkdir -p /srv/www/my-website
cd Static-website
sudo mv * /srv/www/my-website/


- Make sure index.html is present in that directory.

🔧 3. Configure Nginx to Serve Your Site

Edit the default server block or create a new one:
sudo nano /etc/nginx/conf.d/my-website.conf


Paste this configuration:
server {
    listen 80;
    server_name localhost;

    root /srv/www/my-website;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

image.png

You can replace localhost with your domain name if you have one.


🔥 4. Enable and Start Nginx
sudo systemctl enable nginx
sudo systemctl start nginx


- Check status: sudo systemctl status nginx


🧪 5. Test Your Setup
Open a browser and go to:
http://Public-ip of EC2


Or use your server’s IP:
http://<your-server-ip>


You should see your static website’s homepage!
image.png

📝 Pro Tip for Portfolio Hosting(Optional as we are not implementing this as of now)
Since you're building a professional presence, consider:
- Adding HTTPS via Let's Encrypt (certbot-nginx)
- Setting up a GitHub Actions workflow to auto-deploy updates
- Using a custom domain with DNS pointing to your SUSE server




Config file of Nginx in SuseLinux

---------------------------------------------------------------
