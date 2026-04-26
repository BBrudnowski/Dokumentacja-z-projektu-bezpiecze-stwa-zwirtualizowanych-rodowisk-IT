# 🛡️ Bezpieczeństwo zwirtualizowanego środowiska IT

Krótki projekt przedstawiający wysokodostępną infrastrukturę aplikacyjną opartą o wirtualizację, współdzielone zasoby oraz mechanizmy failover.

---

## 🧱 Architektura

Środowisko zbudowane na platformie **VMware vSphere**:

* **ESXi (10.82.4.190)** – host zarządzający
* **vCenter Server** – centralne zarządzanie klastrem
* **Linux1 & Linux2 (Ubuntu)** – serwery aplikacyjne (klaster)

---

## 💾 Współdzielona pamięć (NFS)

* **Serwer NFS:** `10.82.4.58`
* **Mount point:** `/mnt/nfs`
* Automatyczne montowanie przez `/etc/fstab`
* Przechowywanie plików aplikacji (wspólne dane dla obu węzłów)

---

## 🌐 Warstwa aplikacyjna

Architektura **Reverse Proxy**:

* **Apache HTTP Server**

  * Obsługa hosta: `fruit-blog.local`
  * Proxy → `http://127.0.0.1:3000`
* **Node.js (fruit-blog)**

  * Zarządzanie przez **PM2**
  * Auto-restart i monitoring aplikacji

---

## 🔁 High Availability

Realizacja przez **Keepalived**:

* **VIP:** `10.82.4.155`
* Tryb **MASTER/BACKUP**
* Automatyczny failover przy awarii
* Eliminacja pojedynczego punktu awarii (SPOF)

---

## 🌍 Adresacja IP

| Komponent         | Adres IP    | Opis                   |
| ----------------- | ----------- | ---------------------- |
| ESXi              | 10.82.4.190 | Host fizyczny          |
| NFS Server        | 10.82.4.58  | Współdzielony storage  |
| Linux1            | 10.82.4.154 | Węzeł klastra          |
| Linux2            | 10.82.4.194 | Węzeł klastra          |
| VIP (WWW Cluster) | 10.82.4.155 | Publiczny adres usługi |

---

## ✅ Podsumowanie

Projekt zapewnia:

* wysoką dostępność (HA)
* współdzielone dane (NFS)
* skalowalność (klaster)
* odporność na awarie (failover)

---

## 🚀 Technologie

* VMware vSphere / ESXi
* Ubuntu Linux
* Apache HTTP Server
* Node.js + PM2
* NFS
* Keepalived

---
