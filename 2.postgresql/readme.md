# 1. Install PostgreSQL
```
sudo dnf install postgresql-server -y
sudo postgresql-setup --initdb
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

# 2. Setup
Create user
```
psql -u postgres psql

CREATE ROLE devops WITH LOGIN SUPERUSER PASSWORD '<password>';
```

Allow authentication
/var/lib/pgsql/data/pg_hba.conf
```
local   all             all                             scram-sha-256
host    all             all     127.0.0.1/32            scram-sha-256
host    all             all     0.0.0.0/0               scram-sha-256
```

Listen on network
/var/lib/pgsql/data/postgresql.conf
```
listen_addresses = '*' 
```

```
systemctl restart postgresql
firewall-cmd --add-port=5432/tcp --permanent
firewall-cmd --reload
```