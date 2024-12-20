Dokumentasi Konfigurasi Nginx dan Server

Bagian 1: Pengaturan Nginx
1.1 Direktori Root
Direktori proyek: /var/www/ainash.my.id/
File utama: index.html
File pendukung: style.css, gambar (FotoDiri.png, dll.).
1.2 File Konfigurasi Nginx
Lokasi file: /etc/nginx/sites-available/ainash.my.id
Isi konfigurasi:
nginx
Salin kode
server {
    listen 80;
    server_name ainash.my.id www.ainash.my.id;

    root /var/www/ainash.my.id;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
1.3 Aktivasi Konfigurasi
Perintah untuk membuat symlink:
bash
Salin kode
sudo ln -s /etc/nginx/sites-available/ainash.my.id /etc/nginx/sites-enabled/
Periksa validitas konfigurasi:
bash
Salin kode
sudo nginx -t
Restart Nginx:
bash
Salin kode
sudo systemctl restart nginx
Bagian 2: Penggunaan Crontab
2.1 Pengaturan Reverse Proxy dengan Crontab
Lokasi file crontab:
bash
Salin kode
crontab -e
Contoh entri Crontab untuk reverse proxy:
bash
Salin kode
* * * * * ssh -NR 44433:localhost:80 root@your-server-ip -p 22
2.2 Kegunaan Crontab
Membantu memelihara koneksi SSH untuk reverse proxy.
Memastikan akses server tetap aktif secara otomatis.
Bagian 3: Pengelolaan DNS
3.1 Cloudflare
A Records: Mengarahkan ainash.my.id ke IP server.
CNAME Records: Untuk subdomain jika diperlukan.
3.2 DNS Checker
Verifikasi bahwa domain diarahkan dengan benar ke server Anda.
Bagian 4: Proyek GitHub
4.1 Proyek yang Digunakan
Repository GitHub: aulia-s-portfolio
Folder proyek disimpan di /var/www/ainash.my.id/.
4.2 Perintah Git untuk Update Proyek
Clone repository:
bash
Salin kode
git clone https://github.com/aulins/aulia-s-portfolio.git /var/www/ainash.my.id
Update repository:
bash
Salin kode
cd /var/www/ainash.my.id
git pull origin main
Bagian 5: Troubleshooting
Error 404: Pastikan file index.html ada di root direktori proyek.
Nginx gagal start: Periksa konfigurasi dengan nginx -t.
