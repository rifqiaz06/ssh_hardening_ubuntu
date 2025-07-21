# 🔐 SSH Hardening di Ubuntu Server 22.04 (README Version)

Panduan ini bertujuan mengamankan akses SSH ke server agar tidak mudah disusupi.

## 🔧 Langkah-Langkah Hardening

1. **Cek status SSH**

```bash
sudo systemctl status ssh
```

2. **Nonaktifkan Root Login**

```bash
sudo nano /etc/ssh/sshd_config
# PermitRootLogin no
```

3. **Ganti Port Default**

```bash
#Port 22
Port 2222

sudo ufw allow 2222/tcp
```

4. **Batasi User**

```bash
AllowUsers devops
```

5. **Aktifkan SSH Key**

```bash
ssh-keygen -t rsa -b 4096
ssh-copy-id -p 2222 devops@ip
```

6. **Nonaktifkan Login Password (Opsional)**

```bash
PasswordAuthentication no
```

7. **Restart SSH**

```bash
sudo systemctl restart ssh
```

8. **Tes Akses**

```bash
ssh -p 2222 devops@ip
```

## 🧯 Troubleshooting

- `Permission denied (publickey)` → Periksa key & permission
- Port baru tidak aktif → Cek firewall atau konflik port
- SSH service gagal → Revert config via console

---

## 📚 Referensi

- https://man.openbsd.org/sshd_config
- https://www.digitalocean.com/community/tutorials/how-to-harden-openssh-on-ubuntu-20-04
