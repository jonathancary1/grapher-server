# Grapher Server

The deployment configuration for Grapher.

## Dependencies
```
sudo yum update
```
```
sudo yum install git
```
```
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
sudo chkconfig docker on
sudo reboot
```
```
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## Deployment
```
git clone --recurse-submodules https://github.com/jonathancary1/grapher-server
cd grapher-server
docker-compose build
docker-compose up --detach
```
```
docker exec -it nginx sh
apk add certbot certbot-nginx
certbot --nginx -d grapher.caryjonathan.com
crontab -l | { cat; echo "0 0,12 * * * certbot renew --post-hook \"nginx -s reload\""; } | crontab -
```
