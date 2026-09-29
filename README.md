# cara-install-dan-konfigurasi-samba
# setting adapter 2 menjadi host-only dan setting ip nya
# download samba di debian :
apt update && apt install samba samba-common-bin -y

# pastikan status samba "running" 
systemctl status smbd
# lalu buat backup an settingan smb.conf
cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
# masuk ke settingan smb.conf
nano /etc/samba/smb.conf
# jika anda adalah windows 11 maka di bawah kategori global ketik ini
server min protocol = SMB2
server max protocol = SMB3

# lanjut buat kategori direction file share nya dipaling bawah smb.conf contoh :
[Shareabby]
path = /server/samba/belajar_samba
browseable = yes
guest ok = no
writable = yes
valid users = jamaludin

# ctrl x dan tekan y lalu restart smbd
systemctl restart smbd

# lalu buat direktori dan rule share data nya
mkdir -p /server/samba/belajar_samba
chown nobody:nogroup /server/samba/belajar_samba
chmod 777 /server/samba/belajar_samba
systemctl restart smbd

# lalu tambahkan user
adduser jamaludin
smbpasswd -a jamaludin
systemctl restart smbd

# PENTING!!! pergi di ncpa.cpl sambungkan ip dengan kelompok yang sama dan matikan properties client for microsoft networks BAGI WINDOWS 10/11
