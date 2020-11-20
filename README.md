# Node.js + SSL Deployment with Caddy server

> Steps to deploy a Node.js app to your own (home) server using Caddy as a reverse proxy with automatic SSL certificate 

## 1. Open port 80 on your router
You might need to do this through your internet provider. Optimum has that function on their website in your profile.

## 2. Port Forward port 80 (http) on your router to port 80 on your server IP and same for port 443 (https)
 You can do this by accessing your router settings through a browser.

## 3. Point your godaddy domain to cloudflare

Open cloudflare and add the domain that you bought from godaddy.
In DNS settings create CNAME. Put the name of the prefix that you want. Content should be "yourdomaion.com".
Go to SSL/Tls and set to strict.
Go to overview. Cloudflare should request you to add two dns addresses to godaddy. 
Go to godaddy -> manage dns of your domain -> and switch those to addresses.
Once its done, cloudflare should send you a confirmation email after its active.

## 4. Clone Caddyfile with Docker setup from Github
Clone the caddy and docker compose setup files with:

```
git clone https://github.com/nvoevodin/caddyServer_documentation.git
```
You do not need to touch the docker-compose.yaml
Go to the env -> caddy.env and add your email and your cloudflare global api key
For the api key: Go to profile in your cloudflare account -> api tokens -> and copy your global api key to the caddy.env
Go into the caddyfile and follow the instructions there


## 5. Clone test server from Github
Clone your project. Here is a simple node.js server:
https://github.com/nvoevodin/LetsEncrypt_Documentation.git

```
git clone https://github.com/nvoevodin/LetsEncrypt_Documentation.git #clone

```

It is a hello world server running on port 5000

Once you have docker and docker-compose installed, run:
```
docker-compose up
```

the container will expose a hello world server running on port 5000



### 5. Test if the server app is running

Go to the localhost:5000 in your browser to see 'hello world'


## 6. Setup ufw firewall
On your server computer:

```
sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)
```

## 7. Excecute caddy docker file

Open terminal at the folder with caddyfile and run:

```
docker-compose up
```
You might have to use sudo if it complains about permissions

```
sudo docker-compose up
```

Caddy server will start and will begin requesting cerificates for your domains.

If all goes well it will print your endpoints in the end



### You should now be able to visit your IP with no port (port 80) and see your app. Now let's add a domain


Now, ctrl+C out of the script and do:


```
docker-compose up -d
```

It will launch the server in the background.

Now visit https://yourprefix.yourdomain.com and you should see your Node app
