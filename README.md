#!/bin/bash

# Limpiar reglas previas
sudo iptables -F
sudo iptables -X

# Crear cadena para permitir pings solo desde las IPs autorizadas
sudo iptables -N ALLOW_PING

# Agregar IPs permitidas a la cadena
sudo iptables -A ALLOW_PING -s 67.220.85.186 -j ACCEPT
sudo iptables -A ALLOW_PING -s 38.52.182.224 -j ACCEPT
sudo iptables -A ALLOW_PING -s 181.119.93.90 -j ACCEPT

# Permitir pings solo desde esas IPs
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ALLOW_PING

# Bloquear pings desde cualquier otra IP
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
