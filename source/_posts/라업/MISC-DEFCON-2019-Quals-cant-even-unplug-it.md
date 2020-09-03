---
title: '[MISC] DEFCON 2019 Quals - cant_even_unplug_it'
date: 2019-05-21 00:00:00
category:
  - CTF
  - DEFCON 2019 Quals
tags:
  - CTF
  - DEFCON
  - Archive
---

정석적인 CTF문제라기보다는 하나의 재미있는 수수께끼였던 것 같습니다.

심심해서 팀들이 어떠한 문제를 많이 풀었을까 살펴 봤는데,
<!-- more -->

| Type                     	| Challenges          	| # of team solved 	|
|--------------------------	|---------------------	|-----------------:	|
| Welcoming                	| welcome_to_the_game 	|             1252 	|
| **Intro, Recon, Web**        	| **cant_even_unplug_it** 	|              **390** 	|
| Pwn                      	| speedrun-001        	|              195 	|
| Pwn                      	| speedrun-002        	|              167 	|
| Shellcode                	| speedrun-003        	|              140 	|
| Misc                     	| know_your_mem       	|              122 	|
| Misc                     	| redacted-puzzle     	|              102 	|
| Pwn                      	| speedrun-004        	|               95 	|
| Pwn                      	| babyheap            	|               88 	|
| Pwn                      	| speedrun-009        	|               81 	|
| Reverse                  	| babytrace           	|               76 	|
| Shellcoding              	| speedrun-009        	|               66 	|
| Pwn, Web                 	| noob                	|               61 	|
| Pwn                      	| speedrun-005        	|               56 	|
| Pwn                      	| speedrun-008        	|               53 	|
| Pwn                      	| speedrun-010        	|               30 	|
| Web                      	| Return_to_shellQL   	|               45 	|
| Android, Crypto, Reverse 	| vitor               	|               40 	|
| Shellcoding              	| speedrun-011        	|               39 	|
| Pwn, Reverse             	| gloryhost           	|               36 	|
| Web                      	| ooops               	|               34 	|
| Pwn                      	| speedrun-007        	|               34 	|
| Reverse                  	| mamatrace           	|               31 	|
| Pwn                      	| rtooos              	|               30 	|
| Reverse, Shellcode       	| LCARS000            	|               24 	|
| Pwn                      	| shitorrent          	|               22 	|
| Pwn                      	| speedrun-012        	|               20 	|
| Crypto                   	| tania               	|               17 	|
| Shellcoding              	| Hotel-California    	|               16 	|
| Crypto, Reverse          	| ASRybaB             	|               14 	|
| Crypto, Reverse          	| chainedrsa          	|               10 	|
| Pwn                      	| LCARS022            	|                9 	|
| Pwn, Reverse             	| election_coin       	|                8 	|
| Reverse                  	| papatrace           	|                2 	|
| Pwn                      	| LCARS333            	|                1 	|

이 문제는 두번째로 많이 푼 문제네요...

시작합시다.

# 문제 파악

문제의 설명은 다음과 같습니다.

> You know, we had this up and everything. Prepped nice HTML5, started deploying on a 
military-grade-secrets.dev subdomain, got the certificate, the whole shabang. 
Boss-man got moody and wanted another name, we set up the new names and all. 
Finally he got scared and unplugged the server. Can you believe it? Unplugged. Like
 that can keep it secret…

얻을 수 있는 내용을 요약하자면,

* 원래 military-grade-secrets.dev 라는 사이트가 있었음.
* 서브도메인에 뭔가가 있었음 (아마 flag일겁니다).
* 지금은 서버 다운시켜놔서 접속 안됨.

해당 서버에서 제공하던 웹서비스에 대한 정보를 얻으면 될 것 같습니다.

그런데 문제에는 첨부파일로 힌트가 하나 딸려나옵니다.

## HINT
> Hint: these are HTTPS sites. Who is publicly and transparently logging the info you 
need?
Just in case: all info is freely accessible, no subscriptions are necessary. The 
names cannot really be guessed.

* 인터넷 어디선가 찾을 수 있음.
* 다운시킨 HTTPS 사이트가 어디선가는 로깅이 되어있음 
이라는 정보를 가지고 문제를 풀어봅시다.

# 풀이
서버가 다운되기 전 기록을 남기는 곳을 찾으면 된다고 생각했을때, 떠올랐던 선택지는 [구글](www.google.com)과 [아카이브 사이트](https://archive.org)였습니다.

그리고 military-grade-secrets.dev의 서브도메인들을 알기 위해서 서브도메인 알려주는 아무 [사이트](https://securitytrails.com/list/apex_domain/military-grade-secrets.dev)에나 가서 물어봅시다.

검색 결과 실제로 결과로 나오는 서브도메인은

* military-grade-secrets.dev
* secret-storage.military-grade-secrets.dev
* now.under.even-more-militarygrade.pw.military-grade-secrets.dev
입니다.

두번째와 세번째 서브도메인이 심히 의심스러우니 접속을 하려고 하지만 역시 서버가 다운되었으니 접속될 리가 없습니다.

일단 구글에 military-grade-secrets.dev을 검색했을 때는 별 다른 내용이 없으니 바로 아카이브 사이트를 이용합시다.

[아카이브 사이트](archive.org)에 now.under.even-more-militarygrade.pw.military-grade-secrets.dev의 snapshot을 찾아보니 실제로 존재하고, forget-me-not.even-more-militarygrade.pw로 redirect 시켜줍니다.

실제로 forget-me-not.even-more-militarygrade.pw의 snapshot에는 flag가 존재합니다.

![](/images/DEFCON2019/misc_1.png)

**flag : OOO{DAMNATIO_MEMORIAE}**

