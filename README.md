# grafana-configuration

# *****************************************Install Grafana on Ubuntu

# **************************************** Install InfluxDb

# Ubuntu/Debian AMD64
curl -LO https://download.influxdata.com/influxdb/releases/influxdb2_2.7.10-1_amd64.deb
sudo dpkg -i influxdb2_2.7.10-1_amd64.deb
# Start influx db
sudo service influxdb start

# Verify influx isntalled successfully

sudo service influxdb status

# ***************************************Install telegraf

curl -s https://repos.influxdata.com/influxdata-archive.key > influxdata-archive.key
echo '943666881a1b8d9b849b74caebf02d3465d6beb716510d86a39f6c8e8dac7515 influxdata-archive.key' | sha256sum -c && cat influxdata-archive.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdata-archive.gpg > /dev/null
echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list
sudo apt-get update && sudo apt-get install telegraf

# *************************************** Update URLS with server-ip
[[outputs.influxdb]]
#   ## The full HTTP or UDP URL for your InfluxDB instance.
#   ##
#   ## Multiple URLs can be specified for a single cluster, only ONE of the
#   ## urls will be written to each interval.
#   # urls = ["unix:///var/run/influxdb.sock"]
#   # urls = ["udp://127.0.0.1:8089"]
 urls = ["http://3.110.37.2:8086"]

keep empty telegraf.conf file under /etc/telegraf/ and created input and output conf files under /etc/telegraf/telegraf.d

and I am staring telegraf with below command,

telegraf --config /etc/telegraf/telegraf.conf --config-directory /etc/telegraf/telegraf.d

reload daemon file

systemctl daemon-reload

systemctl restart telegraf.service
systemctl status telegraf.service

