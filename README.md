# How to create an Nginx website using your own domain

This will be a walkthrough of how you can set up a website (with your own domain) using AWS EC2 instance and Nginx.

<br>

## 1. Creating and Launching an EC2 Instance

(Note: Perform the following using a non-root account on AWS. **This is best practice**)

1a. Log in to the AWS console `https://aws.amazon.com`.

1b. Navigate to EC2 and click on Launch Instance.

1c. Configure your instance with Amazon Linux AMI and allow inbound traffic through port 22 (SSH) and port 80 (HTTP).

1d. Launch the instance.

<br>

## 2. Installing Nginx

Once you have launched into the instance, on your EC2 instance terminal:

2a. Update the repository for your instance and install Nginx:
   ```bash
   sudo yum update
   sudo yum install nginx
   ```

2b. Start and enable Nginx:
   ```bash
   sudo systemctl enable nginx
   sudo systemctl start nginx
   ```

2c. Verify NGINX is running by accessing your EC2's public IP in a browser.\
(If you are unable to connect to your EC2 instance this way, it is likely that you do not have your security group setup corrected. It should allow inbound HTTP from any IP address)

<br>


## 3. Purchasing a domain

There are many Domain Registrars that can be used here such namecheap, GoDaddy, etc.

For this walkthrough, we will be using CloudFlare.

### Here's what you will do:
3a. Create an account on Cloudflare `https://www.cloudflare.com`.

3b. Go to the "Registrar" section to purchase and register a domain.

<br>

## 4. Configuring your Domain DNS settings on Cloudflare

On the Cloudflare website, go to **> DNS > Records** and do the following:

4a. Create an **A Record** with your domain name and the EC2 public IP.

4b. Create a **CNAME record** using nginx as the input for the 'Name' box and your domain name in the 'Target' box.

Your Fully Qualified Domain Name (FQDN) will look something like this: `nginx.yourdomain`

---

<br>

### And that should be it

It may take some time for everything to sync up, but within a few minutes you should be able to access your EC2 instance through your domain i.e. `yourdomain` and the CNAME i.e. `nginx.yourdomain`

<br>

|Here is what it will look like:|
|-------|
| ![Nginx Site](https://raw.githubusercontent.com/JunedConnect/Custom-Domain-Nginx/main/images/NginxSite.png) |
