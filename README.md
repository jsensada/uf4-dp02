# uf4-dp02

## How to deploy in a linux machine
```
sudo apt update
sudo apt install nginx -y
sudo apt install python3
sudo apt install python3-pip
sudo mkdir /opt/app
sudo chown -R jsensada:jsensada /opt/app
cd /opt/app
git clone git@github.com:jsensada/uf4-dp02.git
cd uf4-dp02
pip3 install -r requirements.txt
sudo python3 app.py -instance test -port 5001
export INSTANCE=test
export LOGFILE=test.log
gunicorn -w 4 -b 0.0.0.0:5001 app-production:app
gunicorn -w 4 -b 0.0.0.0:5002 app-production:app
sudo cp service-app1.service /etc/systemd/system/
sudo systemctl enable service-app1
sudo systemctl start service-app1
sudo cp /etc/systemd/system/service-app1.service /etc/systemd/system/service-app2.service
sudo systemctl enable service-app2
sudo systemctl start service-app2
sudo cp nginx.conf /etc/nginx/sites-enabled/default
sudo service nginx restart
curl htpp://127.0.0.1/
curl http://127.0.0.1/app1/
curl http://127.0.0.1/app2/
```
