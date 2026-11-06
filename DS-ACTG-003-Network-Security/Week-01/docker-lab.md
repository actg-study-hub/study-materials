# Reproducible three-container network lab

## Prerequisites

- Windows with WSL 2 and Docker Desktop, or another Linux-compatible Docker Engine.
- Docker Engine running.
- Wireshark for reading packet captures.
- Work only on your own authorized lab.

Commands below are suitable for **PowerShell** unless noted otherwise.

## Start the lab

```powershell
docker network create --driver bridge --subnet 172.28.50.0/24 ns-lab
docker run -d --name linux1 --network ns-lab --ip 172.28.50.11 alpine:3.22 tail -f /dev/null
docker run -d --name linux2 --network ns-lab --ip 172.28.50.12 alpine:3.22 tail -f /dev/null
docker run -d --name linux3 --network ns-lab --ip 172.28.50.13 alpine:3.22 tail -f /dev/null
docker ps
docker network inspect ns-lab
```

If the network name or containers already exist, inspect and reuse them instead of blindly recreating them.

## Observe connectivity and addressing

```powershell
docker exec -u 0 linux1 apk add --no-cache iproute2 net-tools traceroute tcpdump
docker exec linux1 ip addr
docker exec linux1 ping -c 4 172.28.50.12
docker exec linux1 arp -a
docker exec linux1 ip neigh show
docker exec linux1 traceroute -n -m 5 -w 1 172.28.50.13
docker exec linux1 ip route
```

Record actual commands and output, not assumed results. ARP cache contents depend on recent traffic.

## Capture ICMP in Wireshark

First PowerShell window (leave running):

```powershell
docker exec -it linux1 tcpdump -i eth0 -n -c 8 -w /tmp/icmp.pcap icmp
```

Second PowerShell window:

```powershell
docker exec linux2 ping -c 4 172.28.50.11
docker cp linux1:/tmp/icmp.pcap "$env:USERPROFILE\Downloads\ns-lab-icmp.pcap"
```

Open the resulting PCAP in Wireshark. Look for ICMP Echo Request (Type 8), Echo Reply (Type 0), IP addresses and sequence numbers.

## Observe automatic Docker IP allocation

```powershell
docker network create --driver bridge --subnet 172.28.60.0/24 ns-auto
docker run -d --name linux-auto --network ns-auto alpine:3.22 tail -f /dev/null
docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' linux-auto
docker exec linux-auto ip route
docker exec linux-auto nslookup example.com
```

Docker IPAM assigns an address without a manual `--ip` flag. This does **not** show a DHCP Discover/Offer/Request/Acknowledge exchange.

## Isolated network check

```powershell
docker exec linux1 ping -c 2 -W 1 172.28.60.2
```

Verify the assigned address first. Interpret loss carefully: failure alone does not identify the exact filtering mechanism.

## Cleanup (destructive: remove only this named lab)

```powershell
docker rm -f linux1 linux2 linux3 linux-auto
docker network rm ns-lab ns-auto
```

## Troubleshooting

- `docker` not recognized: open a fresh PowerShell and verify PATH.
- Docker API unavailable: start Docker Desktop.
- `tcpdump` missing: install it in the particular container with `apk add --no-cache tcpdump`.
- No ARP reply captured: ARP may be cached, or the packet capture stopped too early.
- MAC addresses may change when network endpoints are recreated: inspect current values.
