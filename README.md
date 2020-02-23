# Cara mengaktifkan _Access Control_ di **Mongodb** setelah install

Setelah selesai menginstall mongodb server dan menjalankannya maka akan muncul **warning** seperti dibawah ini :

```mongo
WARNING:  Access control Access control is not enabled for the database.
          Access control is not enabled for the database.
```

Buka **MongoDB** melalui `cmd/terminal`. lalu Ketik **`use admin`**

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

Setelah itu buka file config **`mongod.cfg`**. pada bagian **`#security`** ubah seperti dibawah ini:

```cfg
security:
  authorization: enabled
```

Restart Mongodb Server dan coba login dengan mengetikan:

```cmd
mongo -u irfandi
```

lalu masukan passwordnya dan warning sudah tidak terlihat.

untuk mengakses mongodb server nya dengan cara

**`mongodb://irfandi:userpwd@localhost:27017/namadb?authSoure=admin`**
