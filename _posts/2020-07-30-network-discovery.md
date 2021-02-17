---
layout: post
categories: posts
title: "NETWORK DISCOVERY"
featured-image: /images/2016-11-19/abstract-1.2.jpg
date-string: JULY 30, 2020
---

## COMMONS TOOLS FOR NETWORK DISCOVERY

### Netdiscover commands

> Netdiscover is an active/passive arp reconnaissance tool


```netdiscover -p``` Sniffing network trafic, Netdiscover sent anything 


```netdiscover -r 192.168.X.X/24``` Scan of subnetwork 192.168.X.X/24 by sending ARP frames


### Nmap commands

```nmap -sL 192.168.X.X/24``` Permet de scanner les hôtes d'un sous réseau

```nmap -sP 192.168.X.X/24``` Lister les hôtes du réseau qui répondent à l'ICMP

```nmap -sU 192.168.X.X``` Scan d'une machine pour lister ses ports ouverts en UDP

```nmap -Pn -A 192.168.X.X(/24) --open``` Scan des machines ou réseau avec la liste des ports ouverts

```nmap -Pn --script=smb-enum-shares -p 445 192.168.X.X```

### DIG COMMANDS

> Un transfert de zone complet (AXFR) consiste pour un serveur DNS esclave à demander une copie de zone de à un serveur maitre qui le permet. Cette fonctionnalité est reprise par l'attaquant pour découvrir des sous domaines.

#### Résolution

```dig axfr @dns-server nom-de-domaine``` 


### SMB COMMANDS

```smbclient -U guest //192.168.X.X/share``` Télécharge les fichiers sur un serveur SMB

```smbget -U guest -R smb://192.168.X.X/share ``` Télécharge les fichiers sur un serveur SMB

