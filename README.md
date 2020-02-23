# Cara mengaktifkan _Access Control_ di **Mongodb** setelah install

Setelah selesai menginstall mongodb server dan menjalankannya maka akan muncul **warning** seperti dibawah ini :

```mongo
WARNING:  Access control Access control is not enabled for the database.
          Access control is not enabled for the database.
```

&nbsp;
&nbsp;

## Windows

Buka **MongoDB** melalui `cmd/powershell`. lalu Ketik **`use admin`**

Lalu Ketik :

```mongo
db.createUser(
  {
    user: "irfandi",
    pwd: "userpwd",
    roles: [
          { role: "userAdminAnyDatabase", db: "admin" },
          "readWriteAnyDatabase"
          ]
  }
)  
```

Setelah menambahkan user, lakukan pengecekan user dengan perintah di bawah ini, apabila keluarannya 1 maka sudah berhasil, dan jika 0 maka restart terlebih dahulu mongodb nya.

```mongo
db.auth("irfandi", "userpwd")
```

Lalu itu buka file config **`mongod.cfg`**. pada bagian **`#security`** ubah seperti dibawah ini:

```cfg
security:
  authorization: enabled
```

Restart Mongodb Server dan coba login dengan mengetikan:

```cmd
mongo -u irfandi
```

Lalu masukan passwordnya dan warning sudah tidak terlihat.

Untuk mengakses mongodb server nya dengan cara

**`mongodb://irfandi:userpwd@localhost:27017/namadb?authSoure=admin`**

&nbsp;
&nbsp;

## Distro Ubuntu

Buka **MongoDB** melalui `terminal`. lalu Ketik **`use admin`**

Lalu Ketik :

```mongo
db.createUser(
  {
    user: "irfandi",
    pwd: "userpwd",
    roles: [
          { role: "userAdminAnyDatabase", db: "admin" },
          "readWriteAnyDatabase"
          ]
  }
)  
```

Setelah menambahkan user, lakukan pengecekan user dengan perintah di bawah ini, apabila keluarannya 1 maka sudah berhasil, dan jika 0 maka restart terlebih dahulu mongodb nya.

```mongo
db.auth("irfandi", "userpwd")
```

Lalu itu buka file config **`mongod.cfg`**.

```bash
sudo nano /etc/mongod.conf
```

Pada bagian **`#security`** ubah seperti dibawah ini:

```cfg
security:
  authorization: enabled
```

Restart Mongodb Server

```bash
sudo systemctl restart mongod
```

Coba login dengan mengetikan:

```bash
mongo -u irfandi
```

Lalu masukan passwordnya dan warning sudah tidak terlihat.

Untuk mengakses mongodb server nya dengan cara :

**`mongodb://irfandi:userpwd@localhost:27017/namadb?authSoure=admin`**
