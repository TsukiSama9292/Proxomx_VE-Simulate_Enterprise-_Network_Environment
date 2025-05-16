# Proxomx VE-模擬企業網路環境

---

## 說明
使用 Proxomx VE 模擬企業網路環境  
為了避免服務暴露  
所以此實驗並沒有實作 DNS 此類服務  
對外使用 Cloudflare CDN，避免被追蹤 IP 或被自動腳本發現服務  

---

## 規格(僅一台路由器和一台電腦)
- IP: 任意 ISP 的固定 IP，但是要確認一下是否有防火牆擋住 Port
- 邊緣路由器: hitron 雙工路由 最大 1000MB/s，必須要有 Port Forwarding 功能  
- 電腦: Proxomx VE (PVE 8.4.1, PVE是滾動更新修復Bug，使用最新版本也可以)
  - CPU: Intel i5-12400F (12) @ 4.400GHz
  - RAM: 32GB DDR4 2133 GHz
  - DISK: CT1000X6SSD9 1TB (讀: 540MB/s)
  - 網卡: RTL8125 2.5GbE Controller (rev 05)
P.S: Linux 具備 NAT 轉發，兩個 VM 在相同 PVE node 中封包不會傳到路由器，直接本地處理。

---

## 網路示意圖

---

## 虛擬機規格
- 外部防火牆(DynFi), 內部防火牆(OPNsense)
  - CPU: 12(共用)
  - RAM: 4G
  - DISK: 100GB(零散)
- DMZ 內部虛擬機
  - WAF(NGINX+模組), Proxy(NGINX), Web(NGINX), API
    - CPU: 12(共用)
    - RAM: 2G
    - DISK: 100GB(零散)
- Staff(s)
  - CPU: 2
  - RAM: 4G
  - DISK: 40GB
