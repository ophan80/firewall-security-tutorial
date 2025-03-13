# 🔥 Firewall & Keamanan Jaringan: Proteksi MikroTik + IDS/IPS Suricata + Auto-Block 🚀

## 📌 Pendahuluan
Tutorial ini menjelaskan **cara membangun sistem keamanan jaringan otomatis** menggunakan:
✅ **MikroTik Firewall** untuk proteksi dari DDoS, botnet, & brute-force login  
✅ **Suricata IDS/IPS** untuk mendeteksi & menganalisis serangan jaringan  
✅ **Integrasi Telegram & Email** untuk notifikasi serangan real-time  
✅ **Auto-Block di MikroTik** untuk otomatis memblokir IP berbahaya  
✅ **Dashboard Monitoring** menggunakan **Grafana & ELK Stack**  

---

# **📌 Bagian 1: Proteksi MikroTik dari DDoS & Botnet**
```bash
/ip firewall filter
add chain=input connection-limit=100,32 action=drop comment="Limit max 100 koneksi per IP"
add chain=input protocol=tcp tcp-flags=syn connection-limit=50,32 action=drop comment="Blok SYN Flood"
add chain=input protocol=udp limit=10,5 action=drop comment="Blok UDP Flood"
add chain=input protocol=tcp dst-port=22,8291,21 connection-state=new action=add-src-to-address-list     address-list=BruteForce address-list-timeout=1h comment="Deteksi Brute Force"
add chain=input src-address-list=BruteForce action=drop comment="Blokir IP Brute Force"
```

---

# **📌 Bagian 2: Setup IDS/IPS dengan Suricata di Debian**
```bash
apt update && apt install suricata -y
nano /etc/suricata/suricata.yaml
systemctl restart suricata
```

### **Integrasi dengan MikroTik untuk Auto-Block**
```bash
nano /usr/local/bin/suricata-mikrotik.py
python3 /usr/local/bin/suricata-mikrotik.py &
```

---

# **📌 Bagian 3: Monitoring Serangan dengan Grafana & ELK Stack**
```bash
apt install elasticsearch logstash kibana grafana -y
systemctl enable elasticsearch logstash kibana grafana-server
systemctl start elasticsearch logstash kibana grafana-server
```

---

# **📌 Bagian 4: Notifikasi Otomatis ke Telegram & Email**
```bash
nano /usr/local/bin/suricata-telegram.sh
nohup bash /usr/local/bin/suricata-telegram.sh &
```

---

# **📌 Bagian 5: Auto-Block IP Berbahaya di MikroTik**
```python
nano /usr/local/bin/suricata-mikrotik.py
python3 /usr/local/bin/suricata-mikrotik.py &
```

---

## 🔥 **Kesimpulan**
✅ **MikroTik Firewall** melindungi dari serangan DDoS & botnet  
✅ **Suricata IDS** mendeteksi & memonitor serangan jaringan  
✅ **Notifikasi real-time ke Telegram & Email** jika ada ancaman  
✅ **Auto-Block IP penyerang di MikroTik tanpa campur tangan manual**  
✅ **Dashboard ELK & Grafana untuk analisis lalu lintas & serangan**  

🚀 **Siap diupload ke GitHub!**  
