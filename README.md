Tools Needed:
  - EC2 Ubuntu instance
  - Docker
  - Netdata

Run Netdata via Docker:
docker run -d \
  --name=netdata \
  -p 19999:19999 \
  --cap-add=SYS_PTRACE \
  --security-opt apparmor=unconfined \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  netdata/netdata

Open Port 19999 in EC2 Security Group

  - EC2 → Security Groups → Your Instance's Group → Edit Inbound Rules
  - Add a new rule:
      - Type: Custom TCP
      - Port: 19999
      - Source: 0.0.0.0/0

Access Netdata Dashboard
  - Open in browser:
      - http://your-ec2-public-ip:19999
