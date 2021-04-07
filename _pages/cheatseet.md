---
layout: post
title: "Cheatseet"
author: "fhbapt"
permalink: /cheatseet/
---

## Table of Contents


### [Network](#network)  
 * [Network discovery](#network-discovery)
    * [Netdiscover](#netdiscover) 
    * [Nmap](#nmap)
  * [Services enumerations](#services)
    * [53 - DNS](#dns)
    * [139/445 - SMB](#smb)

## Common tools for network discovery <a name="network-discovery"></a>
In this chapter, the most common tools and commands use to dicover network architecture are presented. 

### Netdiscover commands <a name="netdiscover"></a>

> Netdiscover is an active/passive arp reconnaissance tool


```netdiscover -p``` Sniffing network trafic, Netdiscover sent anything 


```netdiscover -r 192.168.X.X/24``` Scan of subnetwork 192.168.X.X/24 by sending ARP frames


### Nmap commands <a name="nmap"></a>

```nmap -sL 192.168.X.X/24``` Permet de scanner les hôtes d'un sous réseau

```nmap -sP 192.168.X.X/24``` Lister les hôtes du réseau qui répondent à l'ICMP

```nmap -sU 192.168.X.X``` Scan d'une machine pour lister ses ports ouverts en UDP

```nmap -Pn -A 192.168.X.X(/24) --open``` Scan des machines ou réseau avec la liste des ports ouverts

```nmap -Pn --script=smb-enum-shares -p 445 192.168.X.X```

## Services enumerations <a name="services"></a>

### 53 - DNS <a name="dns"></a>

> Un transfert de zone complet (AXFR) consiste pour un serveur DNS esclave à demander une copie de zone de à un serveur maitre qui le permet. Cette fonctionnalité est reprise par l'attaquant pour découvrir des sous domaines.

Commands DIG :

```dig axfr @dns-server nom-de-domaine``` 

### 139/445 - SMB <a name="smb"></a>

SMB Commands :

```smbclient -U guest //192.168.X.X/share``` Télécharge les fichiers sur un serveur SMB

```smbget -U guest -R smb://192.168.X.X/share ``` Télécharge les fichiers sur un serveur SMB

