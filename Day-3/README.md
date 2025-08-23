# Day 3: EC2, Web Servers, and Nginx

Today's session covers the fundamentals of cloud computing with AWS EC2, the role of web servers, and how to deploy a live website using Nginx.

## What is Amazon EC2?

Amazon Elastic Compute Cloud (EC2) is a web service from Amazon Web Services (AWS) that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.

Key features of EC2 include:
- **Virtual Servers (Instances):** You can create and manage virtual machines.
- **Scalability:** You can easily scale the number of instances up or down to handle changes in demand.
- **Variety of Instance Types:** EC2 offers various instance types optimized for different tasks (e.g., compute-optimized, memory-optimized).
- **Pay-as-you-go:** You only pay for the compute time you actually use.

## What are Web Servers?

A web server is software and underlying hardware that accepts requests via HTTP (Hypertext Transfer Protocol) or its secure variant HTTPS. A user agent, commonly a web browser or web crawler, initiates communication by making a request for a specific resource using HTTP, and the server responds with the content of that resource or an error message.

Essentially, a web server's primary job is to store website files (like HTML, CSS, JavaScript, and images) and deliver them to a user's web browser upon request.

### Types of Web Servers

There are many different web servers available. Some of the most popular ones include:
- **Nginx:** Known for its high performance, stability, and low resource consumption.
- **Apache HTTP Server:** One of the oldest and most widely used web servers.
- **Microsoft Internet Information Services (IIS):** A web server for Windows Server.
- **LiteSpeed:** A high-performance, Apache-drop-in replacement.

## Installing Nginx Web Server on Ubuntu

Here are the steps to install Nginx on an Ubuntu EC2 instance.

1.  **Update Package Lists:** First, update your package manager's cache to ensure you get the latest versions of software.
    ```bash
    sudo apt update
    ```

2.  **Install Nginx:** Install the Nginx package. The `-y` flag automatically confirms the installation.
    ```bash
    sudo apt install nginx -y
    ```

3.  **Verify Nginx Status:** Check if the Nginx service is running correctly.
    ```bash
    sudo systemctl status nginx
    ```
    You should see an `active (running)` status.

## Hosted Website on EC2 using Nginx

After installation, Nginx is active and serving a default HTML page. By navigating to your EC2 instance's public IP address in a web browser, you can see the default Nginx welcome page.

To host your own website, you can replace the default files located in `/var/www/html/` with your own website's files (e.g., `index.html`, CSS, and JavaScript files).

Once your files are in place, your website is live and accessible to anyone on the internet via your EC2 instance's public IP address.

