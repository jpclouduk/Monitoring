# Monitoring
Repo to maintain all monitoring deployments


armv6

===== Build Pi For Ansible =====
Add ansible user and provide sudo

===== Setup Users / Mounts
Create monitor user/group

Mount USB
/dev/sda1 /data ext4 errors=remount-ro,noatime 0 2

mkdir -p /monitor/software



=====  INSTALL PROMETHEUS =====
wget https://github.com/prometheus/prometheus/releases/download/v2.21.0/prometheus-2.21.0.linux-armv6.tar.gz
tar -xf /monitor/software/prometheus-2.21.0.linux-armv6.tar.gz -d /monitor
ln -s /monitor/prometheus-2.21.0.linux-armv6 /monitor/prometheus

Push prometheus.service to /etc/systemd/system
systemctl enable prometheus
systemctl start prometheus



=====  INSTALL NODE_EXPORTER =====
wget https://github.com/prometheus/node_exporter/releases/download/v1.0.1/node_exporter-1.0.1.linux-armv6.tar.gz
tar -xf /monitor/software/node_exporter-1.0.1.linux-armv6.tar.gz -d /monitor
ln -s /monitor/node_exporter-1.0.1.linux-armv6 /monitor/node_exporter
Push node_exporter.service to /etc/systemd/system
systemctl enable node_exporter
systemctl start node_exporter


===== Install Graphana =====
wget https://dl.grafana.com/oss/release/grafana-rpi_7.1.5_armhf.deb
dpkg -i grafana-rpi_7.1.5_armhf.deb

Edit /etc/grafana/grafana.ini
data = /data/grafana
plugins = /data/grafana/plugins
