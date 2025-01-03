# Tutorial: Cara Proxy IP Domain Menggunakan Cloudflare

### Catatan
Pastikan sebelum memulai **node kalian sudah berjalan normal**.

---

## Langkah-langkah

### **Pertama**: Mengatur DNS Record
1. Buka [Cloudflare Dashboard](https://dash.cloudflare.com).
2. Pergi ke bagian **DNS Record**.
3. Pilih subdomain panel yang akan kalian proxy kan.
4. Aktifkan **Proxy Mode** (ikon awan oranye).
5. Hapus subdomain node yang sebelumnya sudah ada.

---

### **Kedua**: Membuat Tunnel dengan Cloudflared
1. Masuk ke [Cloudflare Zero Trust](https://one.dash.cloudflare.com).
2. Pergi ke **Network > Tunnels**.
3. Klik **Setup Cloudflared**.
4. Isi nama tunnel (bebas).
5. Pilih OS VPS yang sesuai, lalu salin command yang diberikan.
6. Tempel command tersebut di VPS, jalankan, kemudian simpan konfigurasi dan klik **Next**.
7. Pada **Public Hostname**, isi dengan subdomain node yang tadi dihapus. Pastikan domainnya sesuai.
8. Pada bagian **Service**:
   - Pilih `http`.
   - Isi URL dengan `localhost:8080`.
9. Klik **Save**.

---

### **Ketiga**: Konfigurasi di VPS
1. Jalankan command berikut untuk mengedit konfigurasi:  
   ```bash
   cd /etc/pterodactyl/
   nano config.yml
   ```
2. Cari bagian:
   ```
   ....ssl: true
   ```
   Ubah menjadi:
   ```
   ....ssl: false
   ```
3. Simpan dan keluar:
   - Tekan `Ctrl + O`, lalu `Enter`.
   - Tekan `Ctrl + X`.

4. Restart **Wings** daemon:
   ```bash
   systemctl stop wings
   systemctl start wings
   ```

---

### **Keempat**: Mengatur Daemon Port
1. Di panel Pterodactyl:
   - Pergi ke **Node**.
   - Pilih **Node** yang kalian digunakan.
   - Masuk ke bagian **Settings**.
   - Isi **Daemon Port** dengan `443`.

---

### Selesai
