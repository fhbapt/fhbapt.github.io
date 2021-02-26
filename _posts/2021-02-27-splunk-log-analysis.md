---
layout: post
title: "Log Analysis - Splunk"
author: "fhbapt"
comments: false
tags: Forensic
---

Analyses de logs - Splunk

## Identification de machines 

Identifier les machines d'un réseau qui ont discuté avec un autre réseau :
```
index=network X.X.X.* X.X.X.* | stats count by src_ip, dest_ip
```

Trouver l'hostname de la machine correspondant à l'ip X.X.X.X :
```
index=os host=X.X.X.X 
```
Date du premier échanges entre deux machines :
```
index=network X.X.X.* X.X.X.*
| stats count, min(_time) as first_time by src_ip, dest_ip 
| convert ctime(first_time)
```
Date du dernier échanges entre deux machines :
```
index=network X.X.X.* X.X.X.*
| stats count, max(_time) as first_time by src_ip, dest_ip 
| convert ctime(first_time)
```

## Analyse machine

Identifier les utilisateurs et les services qui se sont connectés à une machine :
```
index=os host=X.X.X.X SubjectUserName=* | stats count by SubjectUserName
```
Lister les processus lancé sur un machine avec l'utilisateur Toto :
```
index=os host=X.X.X.X SubjectUserName=Toto 
|rare NewProcessName
```
Trouver les exécutables (parents/enfants) qui ont exécutés dans le répertoire C:\Users\ :
```
index=os host=X.X.X.X "C:\\Users\\*" | stats count by ParentProcessName, NewProcessName
```
Trouver les actions effectués sur la machine par un processus :
```
index=os host=X.X.X.X ParentProcessName="C:\\\\Program Files (x86)\\\\Internet Explorer\\\\toto.exe" 
| stats count by ParentProcessName, NewProcessName
```
