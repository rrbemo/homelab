# Create Kubernetes Arma 3 server

I've already set up a remote Arma 3 server in Ubuntu. Why not try and get it working on 
this k3s cluster?

## Build an Arma 3 server docker container

### What does an Arma 3 server need?

Quickly reviewing an arma 3 server install for ubuntu...
- https://wirkijowski.medium.com/hosting-a-dedicated-arma-3-server-on-ubuntu-98cdc86a15a3

- ubuntu/debian
- steamcmd
- screen ?
- non-root user
- folder structure

1. use non-root to install arma3 via steamcmd (username/password required)
2. Create paths for profile files
3. use root to configure server files
  - Server config
  - Network config
4. Mod setup
5. Firewall/docker network/manifest network config
6. Start server
