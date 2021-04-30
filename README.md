# EqEmu-Docker
A docker-compose configuration for quickly bringing up a fresh EqEmu server, with or without a loginserver, using the eqemu_server.pl linux installer.

## Quickstart

**FIRST:** Update usernames and passwords contained in the `.env` file. These values will be used to configure the server. Even though the default configuration is only accessible locally it is **STRONGLY ADVISED** to update these values.

Build docker, and start by bringing up the database:
```
docker-compose build && docker-compose up -d
```

Instruct docker to run the EqEmu installer:
```
docker-compose run eqemu-server "perl eqemu_server.pl new_server"
```
Alternately you can specify new_server_with_bots if you know you want bots

Now bring up the server:
```
docker-compose up eqemu-server -d
```

Update `eqhost.txt` in your EQ directory to point to localhost port 5998 for Titanium or 5999 for SoD+:

```
[LoginServer]
Host=127.0.0.1:5998
```

Launch EQ and log in with a new username / password.  The server will auto-provision an account for you.  Proceed through character creation to create account, then logout and flag the account as a GM.

```
docker exec eqemu-server /bin/bash -c "cd /root/server && ./world flag \<username> 250"
```

Login and play!

## Info
... Uses the official linux installer
... Add a blurb about configuration
... Add a blurb about all-in-one vs individual services
... Logs folder / other volumes?
... How to export things
... How to start without loginserver?

## Database Volume
The database in the eqemu-db container persists via a docker volume. If you want to delete this database for any reason just run

```
docker volume rm eqemudocker_db_data
```

# TODO:
pass in server/port
secrets?
all-in-one with mysql installed locally?
Config as volume?
Different docker images for build vs run?
Maybe reuse the .devcontainer's image from the official build server?
peqeditor?
Pass in IpAddress for remote access?

Do we need any of the following packages?

Could NOT find LuaJit (missing: LUAJIT_LIBRARIES LUAJIT_INCLUDE_DIR)
Could NOT find PkgConfig (missing: PKG_CONFIG_EXECUTABLE)

 * PkgConfig
 * LuaJit
 * mbedTLS
