# Installation

Official documentation:
https://docs.mongodb.com/manual/administration/install-community/

# Running
```bash
sudo systemctl enable mongod
sudo systemctl start mongod
sudo systemctl status mongod
mongo
```
# Authorization
Run shell, switch to admin db:
```
use admin
```

Create root account:
```
db.createUser( { user: 'root', pwd: 'INSERT_ROOT_PASSWORD', roles: [ 'root' ] } )
```

Switch to some other db:
```
use myDB
```

Create regular db user:
```
db.createUser( { user: 'myDBUser', pwd: 'INSERT_USER_PASSWORD', roles: [ { role: 'dbOwner', db: 'myDB' } ] } )
```

Edit /etc/mongod.conf to enable authorization, restart mongod.

Log in as root:
```
mongo -u root
```

Log in as a regular user:
```
mongo -u "myDBUser" -p "INSERT_USER_PASSWORD" --authenticationDatabase myDB myDB
```
