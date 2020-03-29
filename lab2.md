<font size="5">**Цель работы:**</font><br>
<font size="4">Проанализировать сетевые параметры публичных DNS серверов, сделать мотивированный вывод о предпочтительных серверах.</font><br>
<font size="5">**Исходные данные:**</font><br>
<font size="4">

* `OS Kali Linux`
* `RStudio IDE`

</font>
<font size="5">**️Используемое ПО:**</font><br>
<font size="4">

* `tracert`
* `ping`
* `whois`
    
</font>
<font size="5">**Исследуемые провайдеры DNS:**</font><br>
<font size="4">

* `MTS PJSC`
* `Google Public DNS`
* `Cloudflare DNS`
* `OpenDNS`

</font>
<font size="5">**Ход работы:**</font><br>
<font size="4">

1. По исследуемым серверам собрать следующие данные: 
    * маршрут;
    * местоположение каждого узла маршрута к DNS-серверу;
    * организацию, владеющую каждым узлом маршрута к DNS-серверу;
    * среднюю RTT к DNS-серверу.
2. Выделить те узлы маршрута, которые вносят наибольшую временную задержку при передаче;
3. Сравнить сетевые параметры DNS серверов.

</font>

<font size="5">**Данные DNS серверов:**</font><br>
<center>**[62.112.96.14] DNS MTS PJSC**</center>

№  | ping #1  | ping #2  | ping #3  |                      Узел                             | Местоположение | Организация
:--|:---------|:---------|:---------|:------------------------------------------------------|:---------------|:------------
1  |<1ms      |1ms       |<1ms      |192.168.100.1                                          |Москва, Россия  |Роутер 
2  |3ms       |3ms       |3ms       |10.215.240.105                                         |Los Angeles, US |IANA
3  |*         |*         |*         |N/A                                                    |N/A             |N/A
4  |4ms       |12ms      |4ms       |10.215.240.109                                         |Los Angeles, US |IANA
5  |4ms       |4ms       |4ms       |62.112.96.13                                           |Москва, Россия  |MGTS adsl-rfc Client
6  |3ms       |3ms       |3ms       |62.112.96.14                                           |Москва, Россия  |MGTS adsl-rfc Client

**RTT=3ms**

<center>**[8.8.8.8] Google Public DNS**</center>

№  | ping #1  | ping #2  | ping #3  |                      Узел                             | Местоположение      | Организация
:--|:---------|:---------|:---------|:------------------------------------------------------|:--------------------|:------------
1  |1ms       |<1ms      |< 1ms     |192.168.100.1                                          |Москва, Россия       |Роутер 
2  |3ms       |3ms       |3ms       |mpts-ss-51.msk.mts-internet.net[212.188.1.6]           |Москва, Россия       |MTS PJSC [former ZAO MTU-Intel]
3  |3ms       |3ms       |3ms       |mag9-cr01-be12.51.msk.mts-internet.net[212.188.1.5]    |Москва, Россия       |MTS PJSC [former ZAO MTU-Intel]
4  |3ms       |4ms       |3ms       |72.14.223.74                                           |Mountain View, US    |Google LLS
5  |4ms       |3ms       |4ms       |108.170.250.99                                         |Mountain View, US    |Google LLS
6  |21ms      |22ms      |21ms      |172.253.66.116                                         |Mountain View, US    |Google LLS
7  |**29ms**  |**42ms**  |**19ms**  |**172.253.66.108**                                     |**Mountain View, US**|**Google LLS**
8  |21ms      |21ms      |20ms      |216.239.62.107                                         |Mountain View, US    |Google LLS
9  |*         |*         |*         |N/A                                                    |N/A                  |N/A
10 |*         |*         |*         |N/A                                                    |N/A                  |N/A
11 |*         |*         |*         |N/A                                                    |N/A                  |N/A
12 |*         |*         |*         |N/A                                                    |N/A                  |N/A
13 |*         |*         |*         |N/A                                                    |N/A                  |N/A
14 |*         |*         |*         |N/A                                                    |N/A                  |N/A
15 |*         |*         |*         |N/A                                                    |N/A                  |N/A
16 |*         |*         |*         |N/A                                                    |N/A                  |N/A
17 |*         |*         |*         |N/A                                                    |N/A                  |N/A
18 |21ms      |21ms      |21ms      |dns.google[8.8.8.8]                                    |Mountain View, US    |Google LLS

**RTT=21ms**

<center>**[1.1.1.1] Cloudflare DNS**</center>

№  | ping #1  | ping #2  | ping #3  |                      Узел                             | Местоположение                  | Организация
:--|:---------|:---------|:---------|:------------------------------------------------------|:--------------------------------|:------------
1  |<1ms      |<1ms      |< 1ms     |192.168.100.1                                          |Москва, Россия                   |Роутер 
2  |3ms       |4ms       |3ms       |mpts-ss-51.msk.mts-internet.net[212.188.1.6]           |Москва, Россия                   |MTS PJSC [former ZAO MTU-Intel]
3  |3ms       |3ms       |2ms       |mag9-cr01-be12.51.msk.mts-internet.net[212.188.1.5]    |Москва, Россия                   |MTS PJSC [former ZAO MTU-Intel]
4  |4ms       |3ms       |4ms       |m9-cr04-be8.77.msk.mts-internet.net[212.188.54.213]    |Москва, Россия                   |MTS PJSC [former ZAO MTU-Intel]
5  |5ms       |4ms       |3ms       |m9-cr05-ae3.77.msk.mts-internet.net[195.34.53.185]     |Москва, Россия                   |MTS PJSC [former ZAO MTU-Intel]
6  |**25ms**  |**22ms**  |**31ms**  |**172.68.8.254**                                       |**San Francisco, US**            |**Cloudflaire Inc.**
7  |**27ms**  |**24ms**  |**21ms**  |**one.one.one.one[1.1.1.1]**                           |**South Brisbane, Australia**    |**Cloudflaire DNS**                

**RTT=28ms**

<center>**[208.67.220.220] OpenDNS**</center>

№      | ping #1  | ping #2  | ping #3  |                      Узел                                 | Местоположение         | Организация
:--    |:---------|:---------|:---------|:----------------------------------------------------------|:-----------------------|:------------------------
1      |<1ms      |<1ms      |< 1ms     |192.168.100.1                                              |Москва, Россия          |Роутер 
2      |3ms       |3ms       |3ms       |mpts-ss-51.msk.mts-internet.net[212.188.1.6]               |Москва, Россия          |MTS PJSC [former ZAO MTU-Intel]
3      |3ms       |3ms       |2ms       |mag9-cr01-be12.51.msk.mts-internet.net[212.188.1.5]        |Москва, Россия          |MTS PJSC [former ZAO MTU-Intel]
4      |4ms       |4ms       |3ms       |a197-cr04-be10.77.msk.mts-internet.net[195.34.50.73]       |Москва, Россия          |MTS PJSC [former ZAO MTU-Intel]
5      |**109ms** |**110ms** |**109ms** |**che-cr02-ae1.63.sam.mts-internet.net[212.188.29.26]**    |**Москва, Россия**      |**MTS PJSC [former ZAO MTU-Intel]**
6      |36ms      |36ms      |36ms      |psshag-cr01-ae10.63.chel.mts-internet.net[212.188.42.130]  |Москва, Россия          |MTS PJSC [former ZAO MTU-Intel]
7      |54ms      |54ms      |54ms      |bhm-cr01-ae12.74.nsk.mts-internet.net[195.34.50.154]       |Москва, Россия          |MTS PJSC [former ZAO MTU-Intel]                
8      |**110ms** |**110ms** |**112ms** |**sem275-cr01-ae5.24.krsk.mts-internet.net[212.188.29.10]**|**Москва, Россия**      |**MTS PJSC [former ZAO MTU-Intel]**
9      |**109ms** |**110ms** |**109ms** |**akd-cr01-ae8.38.irk.mts-internet.net[212.188.29.138]**   |**Москва, Россия**      |**MTS PJSC [former ZAO MTU-Intel]**
10     |**109ms** |**109ms** |**109ms** |**psskv-cr01-ae6.28.skv.mts-internet.net[212.188.28.213]** |**Москва, Россия**      |**MTS PJSC [former ZAO MTU-Intel]**
11     |**109ms** |**110ms** |**109ms** |**teat-cr01-ae0.28.blag.mts-internet.net[212.188.2.106]**  |**Москва, Россия**      |**MTS PJSC [former ZAO MTU-Intel]**
12     |*         |*         |*         |N/A                                                        |N/A                     |N/A
**13** |**243ms** |**243ms** |**243ms** |**resolver2.opendns.com[208.67.220.220]**                  |**San Francisco, US**   |**Cisco OpenDNS, LLC**                 
  
**RTT=242ms**


















