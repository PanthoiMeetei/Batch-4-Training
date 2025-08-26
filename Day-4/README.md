# Day 4
This project demonstrates how to host a static website using **Nginx** on **SUSE Linux** and **Amazon Linux** . It's a lightweight, production-ready setup ideal for portfolios, documentation, or internal dashboards.

---

## 📦 Prerequisites for Suse Linux

- SUSE Linux 
- Basic HTML file (e.g., `index.html`)
- Root or sudo access

---

## ⚙️ Installation Steps

### 1. Install Nginx on Suse Linux

```bash
sudo zypper refresh
sudo zypper install nginx



After installation, Nginx is active and serving a default HTML page. By navigating to your EC2 instance's public IP address in a web browser, you can see the default Nginx welcome page.

To host your own website, you can replace the default files located in `/var/www/html/` with your own website's files (e.g., `index.html`, CSS, and JavaScript files).


📂 2. Create Your Static Website Directory
Let’s say your site files are in /home/neeraj/my-website.
sudo mkdir -p /srv/www/my-website
cd Static-website
sudo mv * /srv/www/my-website/


- Make sure index.html is present in that directory.

🔧 3. Configure Nginx to Serve Your Site

Edit the default server block or create a new one:
sudo vim /etc/nginx/conf.d/my-website.conf


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



---------------------------------------------------------------

## Installing Nginx Web Server on Amazon Linux 

Here are the steps to install Nginx on an Ubuntu EC2 instance.

1.  **Update Package Lists:** First, update your package manager's cache to ensure you get the latest versions of software.
    ```bash
    sudo yum update
    ```

2.  **Install Nginx:** Install the Nginx package. The `-y` flag automatically confirms the installation.
    ```bash
    sudo yum install nginx -y
    ```

3.  **Verify Nginx Status:** Check if the Nginx service is running correctly.
    ```bash
    sudo systemctl status nginx
    ```
    You should see an `active (running)` status.

## Hosted Website on EC2 using Nginx

After installation, Nginx is active and serving a default HTML page. By navigating to your EC2 instance's public IP address in a web browser, you can see the default Nginx welcome page.

To host your own website, you can replace the default files located in `/var/www/html/` with your own website's files (e.g., `index.html`, CSS, and JavaScript files).

### Hosting Your Own Website: Step-by-Step

You can either clone a repository from GitHub or download a template.

#### Option 1: Clone from GitHub

You can clone a pre-existing website repository directly into the web server's root directory.

```bash
# First, remove the default Nginx file
sudo rm /var/www/html/index.nginx-debian.html

# Then, clone the repository
sudo git clone https://github.com/devilraj98/free-css-website.git /var/www/html
```

#### Option 2: Use a Website Template

1.  Navigate to the home directory and download the template files.
    ```bash
    cd ~
    wget https://templatemo.com/download/templatemo_578_first_portfolio
    ```

2.  Install the `unzip` utility if it's not already installed.
    ```bash
    sudo yum install unzip -y
    ```

3.  The downloaded file may not have an extension. Rename it to a `.zip` file.
    ```bash
    mv templatemo_578_first_portfolio templatemo_578_first_portfolio.zip
    ```

4.  Unzip the file.
    ```bash
    unzip templatemo_578_first_portfolio.zip
    ```

5.  Move the contents of the unzipped folder to the Nginx web root directory.
    ```bash
    cd templatemo_578_first_portfolio
    sudo mv * /usr/share/nginx/html

    ```
    
Once your files are in place, your website is live and accessible to anyone on the internet via your EC2 instance's public IP address.

