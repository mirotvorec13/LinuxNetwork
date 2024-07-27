# Сети в Linux

Настройка сетей в Linux на виртуальных машинах.

- [Part 1. Инструмент ipcalc](#part-1-инструмент-ipcalc)
    - [1.1. Сети и маски](#11-сети-и-маски)
    - [1.2. localhost](#12-localhost)
    - [1.3. Диапазоны и сегменты сетей](#13-диапазоны-и-сегменты-сетей)
- [Part 2. Статическая маршрутизация между двумя машинами](#part-2-статическая-маршрутизация-между-двумя-машинами)
    - [Добавление статического маршрута вручную](#добавление-статического-маршрута-вручную)
    - [Добавление статического маршрута с сохранением](#добавление-статического-маршрута-с-сохранением)
- [Part 3. Утилита iperf3](#part-3-утилита-iperf3)
    - [Скорость соединения](#скорость-соединения)
    - [Утилита iperf3](#утилита-iperf3)
- [Part 4. Сетевой экран](#part-4-сетевой-экран)
    - [Утилита iptables](#утилита-iptables)
    - [Утилита nmap](#утилита-nmap)
- [Part 5. Статическая маршрутизация сети](#part-5-статическая-маршрутизация-сети)
    - [Настройка адресов машин](#настройка-адресов-машин)
    - [Включение переадресации IP-адресов](#включение-переадресации-ip-адресов)
    - [Установка маршрута по-умолчанию](#установка-маршрута-по-умолчанию)
    - [Добавление статических маршрутов](#добавление-статических-маршрутов)
    - [Построение списка маршрутизаторов](#построение-списка-маршрутизаторов)
    - [Использование протокола ICMP при маршрутизации](#использование-протокола-icmp-при-маршрутизации)
- [Part 6. Динамическая настройка IP с помощью DHCP](#part-6-динамическая-настройка-ip-с-помощью-dhcp)
- [Part 7. NAT](#part-7-nat)
- [Part 8. Дополнительно. Знакомство с SSH Tunnels](#part-8-дополнительно-знакомство-с-ssh-tunnels)


## Part 1. Инструмент ipcalc
<br/>

### 1.1. Сети и маски

<table>
    <tr>
        <th width=400><br />ip: 192.167.38.54/13<br /></th>
    </tr>
    <tr>
        <td>адрес сети 192.160.0.0</td>
        <td width=800><br />
        
![report](Screenshots/ipcalc/ipcalc192_167_38_54_13%20command%20output.png)<br /></td>
    </tr>
</table><br />

<table>
    <tr>
        <th width=400><br />перевод маски: 255.255.255.0<br /></th>
    </tr>
    <tr>
        <td>в префиксную и двоичную запись:<br /></td>
        <td width=800><br />
        
![report](Screenshots/ipcalc/ipcalc255_255_255_0_per%20command%20output.png)<br /></td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />перевод маски: /15<br /></th>
    </tr>
    <tr>
        <td>в обычную и двоичную запись</td>
        <td width=800><br />
        
![report](Screenshots/ipcalc/ipcalc_15%20command%20output.png)<br /></td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />перевод маски:<br />
        11111111.11111111.11111111.11110000<br /></th>
        </tr>
        <tr>
        <td>в обычную и префиксную запись</td>
        <td width=800><br />
        
![report](Screenshots/ipcalc/ipcalc_28%20command%20output.png)<br /></td>
</tr>
    </tr>
</table><br />

<table>
    <tr>
        <th width=400><br />минимальный и максимальный хост в сети<br />
        12.167.38.4<br /></th>
        </tr>
        <tr>
        <td>маски: /8, /16, /23, /4</td>
        <td width=800><br />

<code>netmask: 8</code><br />
![report](Screenshots/ipcalc/ipcalc_min_max_host_8%20command%20output.png)<br />
<code>netmask: 16</code><br />
![report](Screenshots/ipcalc/ipcalc_min_max_host_16%20command%20output.png)<br />
<code>netmask: 23</code><br />
![report](Screenshots/ipcalc/ipcalc_min_max_host_23%20command%20output.png)<br />
<code>netmask: 4</code><br />
![report](Screenshots/ipcalc/ipcalc_min_max_host_4%20command%20output.png)<br />
</td>
</tr>
    </tr>
</table><br />

### 1.2. localhost

<br />
<table>
    <tr>
        <th width=400><br />
        127.0.0.1<br />
        </th>
    </tr>
    <tr>
    <td><br />
        Localhost (так называемый, «местный» от англ. local,<br />
        или «локальный хост», по смыслу — этот компьютер)<br />
        — в компьютерных сетях, стандартное, официально<br />
        зарезервированное доменное имя для частных<br />
        IP-адресов (в диапазоне 127.0.0.1 — 127.255.255.254)<br />
        <br />
        Соответственно 127.0.0.2, 127.1.0.1,<br />
        адреса с которых есть возможность обращаться<br />
        к приложению работающему на localhost.<br />
        194.34.23.100, 128.0.0.1 адреса<br /> с которых нет такой возможности.<br />
        </td>
    <td width=800><br />

![report](Screenshots/ipcalc/ipcalc_localhost%20command%20output.png)<br /></td>
    </tr>
</table>
<br />

---
### 1.3. Диапазоны и сегменты сетей

<br />
<table>
    <tr>
        <th width=400><br />
        IP можно использовать в качестве публичного<br />
        </th>
        <th width=400><br />
        IP можно использовать в качестве частных<br /></th>
    </tr>
    <tr>
    <td><br />134.43.0.2<br />
    172.0.2.1<br />
    192.172.0.1<br />
    172.68.0.2<br />
    192.169.168.1<br /></td>
    <td><br />10.0.0.45<br />
    192.168.4.2<br />
    172.20.250.4<br />
    172.16.255.255<br />
    10.10.10.10<br /></td>
    </tr>

</table><br />

<table>
    <tr>
        <th width=400><br />
        IP адреса шлюза возможны у сети 10.10.0.0/18<br /></th>
        <th width=400><br />
        IP адреса шлюза невозможны у сети 10.10.0.0/18<br /></th>
    </tr>
    <tr>
    <td><br />
    10.10.0.2<br />
    10.10.10.10<br />
    10.10.1.255<br />
    </td>
    <td><br />
    10.0.0.1<br />
    10.10.100.1<br />
    </td>
    </tr>

</table><br />

---
## Part 2. Статическая маршрутизация между двумя машинами

<br />
<table>
    <tr>
        <th width=400><br />
        static gateway <kbd>ws1</kbd> <kbd>ws2</kbd><br /></th>
    </tr>
    <tr>
        <td><code>ws1 - </code><kbd>ip a</kbd><br />
        <br />
        <code>ws2 - </code><kbd>ip a</kbd><br />
        </td>
        <td width=800><br />

<code>ws1 - ip a</code><br />
![report](Screenshots/ws1-ws2/ip_a_ws1%20command%20output.png)<br />
<br />

<code>ws2 - ip a</code><br />
![report](Screenshots/ws1-ws2/ip_a_ws2%20command%20output.png)<br/></td>
    </tr>
</table><br />

<table>
    <tr>
        <th width=400><br />
        Описать сетевой интерфейс<br />
        <kbd>vim etc/netplan/00-installer-config.yaml</kbd><br />
        </th>
    </tr><br />
    <tr>
        <td>ws1 - 192.168.100.10, маска /16</td>
        <td width=800><br />
        
![report](Screenshots/ws1-ws2/1_netplan_ws1%20command%20output.png)<br />
<code>netplan apply</code><br />

![report](Screenshots/ws1-ws2/netplan_apply_ws1%20command%20output.png)<br />
</td>
</tr>
<tr><td>ws2 - 172.24.116.8, маска /12</td>
<td width=800><br />

![report](Screenshots/ws1-ws2/1_netplan_ws2%20command%20output.png)<br />
<code>netplan apply</code><br />

![report](Screenshots/ws1-ws2/netplan_apply_ws2%20command%20output.png)<br />
</td>
</tr>
</table><br />

### Добавление статического маршрута вручную

<br />
<table>
    <tr>
        <th width=400><br />
        <kbd>ip r add</kbd><br />
        </th>
        </tr>
        <tr>
        <td>ws1<br />
        <br />
        ping 172.24.116.8</td>
        <td width=800><br />
<code>ws1: ip route add - ws2</code><br />
![report](Screenshots/ws1-ws2/ip_r_add_ws1%20command%20output.png)<br />

![report](Screenshots/ws1-ws2/ping_ip_route_add_ws1%20command%20output.png)<br />
</td>
<tr>
        <td>ws2<br />
        <br />
        ping 192.168.100.10</td>
        <td width=800><br />

<code>ws2: ip route add - ws1</code><br />
![report](Screenshots/ws1-ws2/ip_r_add_ws2%20command%20output.png)<br />


![report](Screenshots/ws1-ws2/ping_ip_route_add_ws2%20command%20output.png)<br />
</td>
</tr>
</table><br />

### Добавление статического маршрута с сохранением

<br />
<table>
    <tr>
        <th width=400><br /><kbd>vim etc/netplan/00-installer-config.yaml</kbd><br /></th>
        </tr>
        <tr>
        <td>1. ws1<br />
        2. netplan apply<br />
        3 .ping 172.24.116.8</td>
        <td width=800><br />

<code>add static gateway ws1</code><br />
![report](Screenshots/ws1-ws2/netplan_ws1%20command%20output.png)<br />

![report](Screenshots/ws1-ws2/ping_netplan_edit_ws1%20command%20output.png)<br />
</td>
</tr>
<tr>
    <td>1. ws2<br />
    2. netplan apply<br />
    3. ping 192.168.100.10</td>
    <td width=800><br />

<code>add static gateway ws2</code><br />
![report](Screenshots/ws1-ws2/netplan_ws2%20command%20output.png)<br />

![report](Screenshots/ws1-ws2/ping_ip_route_add_ws2%20command%20output.png)<br />
</td>
</tr>
</table><br />

---

## Part 3. Утилита iperf3

<br />

### Скорость соединения
<br />
<table>
    <tr>
        <th width=400><br />
        Перевести<br />
        </th>
        </tr>
        <tr>
        <td><br />8 Mbps = 1 MB/s<br />
        <br />
        100 MB/s = 800000 Kbps<br />
        <br />
        1 Gbps = 1000 Mbps<br />
        </td>
        <td width=800><br />1 Mbit = 0.125 MB<br />
        <br />
        1 MB = 8192 Kbit<br />
        <br />
        1 Gbit = 1000 Mbit</td>
</tr>
</table><br />

### Утилита iperf3
<br />
<table>
    <tr>
        <th width=400><br />
        Измерение скорости соединения между ws1 и ws2<br />
        </th>
        </tr>
<tr>
    <td>start iperf3 <kbd>-s</kbd> <kbd>--server</kbd><br />
    <br />
    <br />
    start connect <kbd>-c</kbd> <kbd>--client</kbd> <kbd><code>host</code></kbd><br />
    </td>
    <td width=800><br />

<code>server ws2</code><br />

![report](Screenshots/iperf3/iperf3_-s_%20ws2%20command%20output.png)<br />
<br />

<code>client ws1</code><br />

![report](Screenshots/iperf3/iperf3_-c_%20ws1%20command%20output.png)<br />
</td>
</tr>
</table><br />

---

## Part 4. Сетевой экран
<br />

### Утилита iptables
<br />
<table>
    <tr>
        <th width=400><br /><kbd>/etc/firewall.sh</kbd><br /></th>
        </tr>
        <tr>
        <td><br /><code>ws1</code><br />
        Правило запрещающее "пинговать" машину<br />
        стоит выше по списку,<br />
        чем разрешающее правило.<br />
        Второе игнорируется.<br /><br />
        Что-бы открыть порты - <br />
        были установлены  <code>apache2</code> и <code>OpenSSH</code><br />
        <br />
        </td>
        <td width=800><br />

<code>/etc/firewall.sh</code> <kbd>ws1</kbd><br />
![report](Screenshots/iptables/iptables_%20ws1%20command%20output.png)<br />
<kbd>/chmod +x /etc/firewall.sh</kbd> и <kbd>/etc/firewall.sh</kbd><br />

![report](Screenshots/iptables/sudo_chmod_run_bash_%20ws1%20command%20output.png)<br />
</td>
<tr>
        <td><br /><code>ws2</code><br />
        Правило разрешающее "пинговать" машину<br />
        стоит выше по списку,<br />
        чем запрещающее правило.<br />
        Второе игнорируется.<br />
        </td>
        <td width=800><br />

<code>/etc/firewall.sh</code> <kbd>ws2</kbd><br />
![report](Screenshots/iptables/iptables_%20ws2%20command%20output.png)<br />
<kbd>/chmod +x /etc/firewall.sh</kbd> и <kbd>/etc/firewall.sh</kbd><br />

![report](Screenshots/iptables/sudo_chmod_run_bash_%20ws2%20command%20output.png)<br />
</td>
</tr>
</table><br />
<table>
    <tr>
        <th width=400><br /><kbd>iptables -L</kbd><br /></th>
        </tr>
        <tr>
        <td><br /><code>ws1</code><br />
        Порты:<br />
        </td>
        <td width=800><br />

![report](Screenshots/iptables/iptables_L_%20ws1%20command%20output.png)<br />
</td>
<tr>
        <td><br /><code>ws2</code><br />
        Порты:<br/>
        </td>
        <td width=800><br />

![report](Screenshots/iptables/iptables_L_%20ws2%20command%20output.png)<br />
</td>
</tr>
</table><br />

### Утилита nmap
<br />

<table>
    <tr>
        <th width=400><br />Команды <kbd>ping</kbd> и
        <kbd>nmap</kbd><br /></th>
        </tr>
        <tr>
        <td><br /><code>ws1: ping - ws2</code><br />
        на ws2 не стоит запрещающего правила.<br />
        машина отвечает на запросы.
        <br /></td>
        <td width=800><br />

![report](Screenshots/iptables/ws1_ping_ws2%20command%20output.png)<br />
</td>
<tr>
        <td><br /><code>ws2: ping - ws1</code><br />
        на ws1 стоит запрет echo reply<br />
        <br />
        </td>
        <td width=800><br />

![report](Screenshots/iptables/ws2_ping_ws1%20command%20output.png)

<br />
</td>
</tr><br />
<tr>
        <td><br /><code>ws1: nmap - ws2</code><br />
        Host is up<br />
        </td>
        <td width=800><br />

![report](Screenshots/iptables/ws1_nmap_ws2%20command%20output.png)<br />
</td>
<tr>
        <td><br /><code>ws2: nmap - ws1</code><br />
        Host is up<br />
        </td>
        <td width=800><br />

![report](Screenshots/iptables/ws2_nmap_ws1%20command%20output.png)<br />
</td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />Сохраняем дампы образов виртуальных машин</th><br />
        </tr>
        <tr>
        <td><code>dump ws1, ws2</code><br />
        <br /></td>
        <td width=800><br />

![report](Screenshots/iptables/dump%20command%20output.png)<br />
</td>
</tr>
</table><br />

---
## Part 5. Статическая маршрутизация сети



<br />
<table>
    <tr>
        <th width=400><br />

### Настройка адресов машин
<br />
        </th>
    </tr>
    <tr>
        <td><kbd>/etc/netplan/*.yaml</kbd> редактируем файл<br />
        <br />
        <kbd>ip -4 a</kbd> - проверяем ip<br />
        <br />
        <kbd>ping 10.10.0.2</kbd> <code>ws11</code><br />
        </td>
        <td width=800><br />

<code>r1 - /etc/netplan/*.yaml</code><br />

![report](Screenshots/net%20routing/r1_netplan%20command%20output.png)<br />

<code>r1 ip -4 a</code><br />

![report](Screenshots/net%20routing/r1_netplan_apply%20command%20output.png)<br />

<code>r1: ping - ws11</code><br />

![report](Screenshots/net%20routing/r1_ping_ws11%20command%20output.png)<br />

<br />
</td>
</tr>
    <tr>
        <td><kbd>/etc/netplan/*.yaml</kbd> редактируем файл<br />
        <br />
        <kbd>ip -4 a</kbd> - проверяем ip<br />
        <br />
        </td>
        <td width=800>

<code>r2 - /etc/netplan/*.yaml</code><br />

![report](Screenshots/net%20routing/r2_netplan%20command%20output.png)
<br />
<code>r2</code><br />

![report](Screenshots/net%20routing/r2_netplan_apply%20command%20output.png)<br />
<br />
</td>
</tr>
    <tr>
        <td><kbd>/etc/netplan/*.yaml</kbd> редактируем файл<br />
        <br />
        <kbd>ip -4 a</kbd> - проверяем ip<br />
        <br />
        </td>
        <td width=800>

<code>ws11 - /etc/netplan/*.yaml</code><br />

![report](Screenshots/net%20routing/ws11_netplan%20command%20output.png)
<br />
<code>ws11</code><br />

![report](Screenshots/net%20routing/ws11_netplan_apply%20command%20output.png)<br />
<br />
</td>
</tr>
    <tr>
        <td><kbd>/etc/netplan/*.yaml</kbd> редактируем файл<br />
        <br />
        <kbd>ip -4 a</kbd> - проверяем ip<br />
        <br />
        </td>
        <td>

```ws21 /etc/netplan/*.yaml```<br />

![report](Screenshots/net%20routing/ws21_netplan%20command%20output.png)<br/>
```ws21```<br />

![report](Screenshots/net%20routing/ws21_netplan_apply%20command%20output.png)<br/>
<br />
</td>
</tr>
    <tr>
        <td><kbd>/etc/netplan/*.yaml</kbd> редактируем файл<br />
        <br />
        <kbd>ip -4 a</kbd> - проверяем ip<br />
        <br />
        <kbd>ping 10.20.0.10</kbd> <code>ws21</code>
        </td>
        <td width=800>

<code>ws22 /etc/netplan/*.yaml</code><br />

![report](Screenshots/net%20routing/ws22_netplan%20command%20output.png)<br/>
<code>ws22</code><br />

![report](Screenshots/net%20routing/ws22_netplan_apply%20command%20output.png)<br/>
<code>ws22: ping - ws21</code><br />

![report](Screenshots/net%20routing/ws22_ping_ws21%20command%20output.png)<br/>
</td>
    </tr>
</table><br />


<table>
    <tr>
        <th width=400><br />

### Включение переадресации IP-адресов
<br /></th>
    </tr><br />
    <tr>
        <td><kbd>sysctl -w net.ipv4.ip_forward=1</kbd><br />
        <code>r1</code><br />
        Редактирование файла <code>/etc/sysctl.conf</code><br />
        Убираем '#' комментарий.<br />
        </td>
        <td width=800><br />

![report](Screenshots/net%20routing/r1_net_ipv4_ipforward%20command%20output.png)<br />

![report](Screenshots/net%20routing/r1_net_ipv4_ipforward_syscrl_conf%20command%20output.png)<br />
</td>
</tr>
<tr>
<td><kbd>sysctl -w net.ipv4.ip_forward=1</kbd><br />
        <code>r2</code><br />
        Редактирование файла <code>/etc/sysctl.conf</code><br />
        <br />
        </td>
        <td width=800><br />

![report](Screenshots/net%20routing/r2_net_ipv4_ipforward%20command%20output.png)<br />

![report](Screenshots/net%20routing/r2_net_ipv4_ipforward_syscrl_conf%20command%20output.png)<br />
</td>
</tr>
</table><br />

<br />
<table>
    <tr>
        <th width=400><br />

### Установка маршрута по-умолчанию
<br /><kbd>etc/netplan/00-installer-config.yaml.</kbd><br />
        </th>
    </tr>
    <tr>
        <td><code>ws11</code><br />
        ip r<br />
        ping <br />
        <br />
        Утилита tcpdump позволяет проверять<br />
        заголовки пакетов TCP/IP и выводить<br />
        одну строку для каждого из пакетов. Она<br />
        будет делать это до тех пор, пока не нажать - <br />
        <kbd>Ctrl + C</kbd><br />
        </td>
        <td width=800><br /> 

<code>netplan ws11</code><br />

![report](Screenshots/net%20routing/ws11_default_netplan%20command%20output.png)<br />
<code>ip r</code><br />

![report](Screenshots/net%20routing/ip_r_ws11%20command%20output.png)<br />
<code>ws11: ping -r2</code><br />

![report](Screenshots/net%20routing/ws11_ping_r2%20command%20output.png)<br />
<br />
<code>r2: tcpdump -tn -i enp0s3</code><br />

![report](Screenshots/net%20routing/r2_tcpdump_tn_i_enp0s3%20command%20output.png)<br />
</td>
</tr>
<tr><td><code>ws21</code></td>
<td width=800></br>

<code>netplan ws21</code><br />

![report](Screenshots/net%20routing/ws21_default_netplan%20command%20output.png)<br />

![report](Screenshots/net%20routing/ip_r_ws21%20command%20output.png)
<br />
</td>
</tr>
<tr><td><code>ws22</code></td>
<td width=800></br>
<code>netplan ws22</code><br />

![report](Screenshots/net%20routing/ws22_default_netplan%20command%20output.png)<br />

![report](Screenshots/net%20routing/ip_r_ws22%20command%20output.png)
<br />
</td>
</tr>
</table><br />

<br />
<table>
    <tr>
        <th width=400><br />

### Добавление статических маршрутов
<br />
        <kbd>etc/netplan/00-installer-config.yaml</kbd><br />
        </th>
        </tr>
        <tr>
        <td><code>r1 netplan</code><br />
        <br />
        <kbd>ip r</kbd></td>
        <td width=800><br />
<code>r1 netplan</code>

![report](Screenshots/net%20routing/r1_static_gateway_netplan%20command%20output.png)<br />

![report](Screenshots/net%20routing/r1_ip_r_static_gateway%20command%20output.png)<br />
</td>
<tr>
        <td><code>r2 netplan</code><br />
        <br />
        <kbd>ip r</kbd></td>
        <td width=800><br />
<code>r2 netplan</code>

![report](Screenshots/net%20routing/r2_static_gateway_netplan%20command%20output.png)<br />
<code>r2 ip r</code>

![report](Screenshots/net%20routing/r2_ip_r_static_gateway%20command%20output.png)<br />
</td>
</tr><tr><td><code>ws11</code> - <kbd>ip r list<br />
10.10.0.0/[маска сети]</kbd> и<br />
<kbd>ip r list 0.0.0.0/0</kbd><br />
<br />

- маршрутизатор выбирает маршрут с <br />
«самой длинной маской», поскольку это <br />
более точное решение. По этому, <br />
маршрут по умолчанию никогда <br />
не будет выбран, если есть <bt />
альтернативные решения.<br />
</td><td width=800><br />

![report](Screenshots/net%20routing/ws11_ip_r_list%20command%20output.png)<br />
</td></tr>
</table><br />


<br />
<table>
    <tr>
        <th width=400><br />

### Построение списка маршрутизаторов
<br/><kbd>traceroute - tcpdump</kbd><br /></th>
        </tr>
        <tr>
        <td><code>r1</code> - <kbd>tcpdump -tnv -i enp0s3</kbd><br />
        <br /><br />
        <code>ws11</code> - <kbd>traceroute 10.20.0.10</kbd><br />
        из скринов видно что <code>ws11</code><br />
        обращается через роутер к <code>r2</code><br />
        получает ответ от роутера, через интерфейс enp0s3<br />
        после того как роутер <code>r2</code> проложил путь до <code>ws21</code><br />
        машина посылает ответные пакеты.<br />

- -i интерфейс<br />
    - Задает интерфейс, с которого необходимо<br />
    анализировать трафик (без указания<br />
    интерфейса - анализ "первого попавшегося").<br />
    <br />
- -n
    - Отключает преобразование IP в доменные<br />
    имена. Если указано -nn, то запрещается<br />
    преобразование номеров портов в название<br />
    протокола.<br />
    <br />
- -e
    - Включает вывод данных канального уровня<br />
    (например, MAC-адреса).<br />
    <br />
- -v
    - Вывод дополнительной информации (TTL,<br />
    опции IP).<br />
    <br />
- -s размер
    - Указание размера захватываемых пакетов.<br />
    (по-умолчанию - пакеты больше 68 байт)<br />
    <br />
- -w имя_файла
    - Задать имя файла, в который сохранять<br />
    собранную информацию.<br />
    <br />
- -r имя_файла
    - Чтение дампа из заданного файла.<br />
    <br />
- -p
    - Захватывать только трафик, предназначенный<br />
    данному узлу. (по-умолчанию - захват всех<br />
    пакетов, например в том числе широковещательных).<br />
    <br />
- -q
    -Переводит tcpdump в "бесшумный режим", в котором<br />
    пакет анализируется на транспортном уровне<br />
    (протоколы TCP, UDP, ICMP), а не на сетевом (протокол IP).<br />
    <br />
- -t
    - Отключает вывод меток времени.
        </td>
        <td width=800><br />
        
![report](Screenshots/net%20routing/r1_tcpdump_tnv_i_enp0s3%20command%20output.png)<br />

![report](Screenshots/net%20routing/r1_tcpdump_tn_i_enp0s3%20command%20output.png)<br />

![report](Screenshots/net%20routing/r1_tcpdump_tnv_i_whohas_enp0s3%20command%20output.png)<br />

![report](Screenshots/net%20routing/ws11_trceroute_ws21%20command%20output.png)<br />
</td>
</tr>
</table><br />

### Использование протокола ICMP при маршрутизации
<br />
<table>
    <tr>
        <th width=400><br /><kbd>tcpdump - ping</kbd><br /></th>
        </tr>
        <tr>
        <td><code>r1</code><br />
        <kbd>tcpdump -n -i enp0s3</kbd><br />
        <br />
        <code>ws11</code><br />
        <br />
        ping -c 1 10.30.0.111<br />
        </td>
        <td width=800><br />
        
![report](Screenshots/net%20routing/r1_tcpdump_n_i_enp0s3_icmp%20command%20output.png)<br />

![report](Screenshots/net%20routing/ws11_ping_notexist_apm%20command%20output.png)<br />
</td>
</tr>
</table><br />

---

## Part 6. Динамическая настройка IP с помощью DHCP
<br />
<table>
    <tr>
        <th width=400><br />Настройки DHCP<br /></th>
        </tr>
        <tr>
        <td>1. Для установки пакета<br /> DCHP-сервера нужно выполнить<br />
        команду: <kbd>sudo apt install isc-dhcp-server</kbd><br />
        <br />
        адрес маршрутизатора по-умолчанию<br />
        редактируем<kbd>/etc/dhcp/dhcpd.conf</kbd><br />
        <br />
        <br /></td>
        <td width=800><br />

<code>dhcpd.conf</code><br />

![report](Screenshots/dhcp/vim_etc_dhcp_dhcpconf%20command%20output.png)<br />

<code>resolv.conf</code><br />

![report](Screenshots/dhcp/vim_etc_resolvconf%20command%20output.png)<br />
</td>
</tr>
</table><br />

<br />
<table>
    <tr>
        <th width=400><br />DHCP ws21, ws22<br /></th>
        </tr>
        <tr>
        <td>Перезагрузка dhcp командой<br />
        <kbd>systemctl restart isc-dhcp-server</kbd><br />
        <br />
        <code>ws21</code><br />
        <kbd>/etc/dhcp/dhcpd.conf</kbd><br />
        <br />
        <br /></td>
        <td width=800><br />

<code>r2 restart dhcp</code><br />
![report](Screenshots/dhcp/systemctl_restart_isc-dhcp-server%20command%20output.png)<br />

<code>ws22: ping - ws21</code><br />
![report](Screenshots/dhcp/ws22_ping_ws21%20command%20output.png)<br />
</td>
</tr>
</table><br />

<br />
<table>
    <tr>
        <th width=400><br />macaddress<br /></th>
        </tr>
        <tr>
        <td>прописываем <code>macaddress</code> netplan<br />
        <br />
        <br />
        <code>r2</code><br />
        <kbd>/etc/dhcp/dhcpd.conf</kbd><br />
        <br />
        <br /></td>
        <td width=800><br />

<code>ws11</code><br />
![report](Screenshots/dhcp/ws11_macadres_netplan%20command%20output.png)<br />

<code>r1 задаем статический ip для mac адреса</code><br />
![report](Screenshots/dhcp/r1_vim_etc_dhcp_dhcpconf%20command%20output.png)<br />

<code>r1 resolv.conf</code><br />
![report](Screenshots/dhcp/r1_resolv_conf%20command%20output.png)<br />

<code>ws11: ping - ws21, ws22</code><br />
![report](Screenshots/dhcp/ws11_ping_ws21_ws22%20command%20output.png)<br />
</td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />Запрашиваем новый ip у dhcp<br /></th>
        </tr>
        <tr>
        <td>отчищаем наши ip <code> sudo dhclient -r</code><br />
        <br />
        запрашиваем новый ip <code>sudo dhclient enp0s3</code><br />
        <br />
        <br /></td>
        <td width=800><br />

<code>ws21</code><br />
![report](Screenshots/dhcp/ws21_ip_a_1%20command%20output.png)<br />

<code>ws21</code><br />
![report](Screenshots/dhcp/ws21_ip_a_new_old_dhclient%20command%20output.png)<br />


</td>
</tr>
</table><br />

---
## Part 7. NAT

<table>
    <tr>
        <th width=400><br />apache2<br /></th>
        </tr>
        <tr>
        <td>для установки sudo apt install apache2<br />
        <code>/etc/apache2/ports.conf</code><br />
        <br />
        <code>service apache2 start</code><br />
        </td>
        <td width=800><br />

<code>r1</code><br />
![report](Screenshots/NAT/r1_apache_ports%20command%20output.png)<br />
<br />
<code>service apache2 start<><br />
![report](Screenshots/NAT/r1_apache_start%20command%20output.png)<br />

<code>ws22</code><br />
![report](Screenshots/NAT/ws22_apache_ports%20command%20output.png)<br />

<code>service apache2 start</code><br />
![report](Screenshots/NAT/ws22_apache_start%20command%20output.png)<br />


</td>
</tr>
</table><br />


<table>
    <tr>
        <th width=400><br />Редактирование правил iptables для файла /firewall.sh<br />
        </th>
        </tr>
        <tr>
        <td>Редактируем файл <kbd>/etc/firewall.sh</kbd><br />
        <br />
        <br /></td>
        <td width=800><br />

<code>отбрасываем все маршрутизируемые пакеты</code><br />
![report](Screenshots/NAT/r2_firewall%20command%20output.png)<br />

<code>соединение между ws22 и r1</code><br />
![report](Screenshots/NAT/ws22_ping_r1%20command%20output.png)<br />

<code>маршрутизация всех пакетов протокола ICMP</code><br />
![report](Screenshots/NAT/r2_firewall_forward_accept%20command%20output.png)<br />

<code>соединение между ws22 и r1</code><br />
![report](Screenshots/NAT/ws22_ping_r1_accept%20command%20output.png)<br />

<code>включить SNAT, DNAT</code><br />
![report](Screenshots/NAT/r2_firewall_dnat_snat%20command%20output.png)<br />
<code>применить правила для iptables</code><br />
![report](Screenshots/NAT/r2_firewall_apply%20command%20output.png)<br />


</td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />telnet<br /></th>
        </tr>
        <tr>
        <td>
        Перечень опций:<br />
        -4 – вручную включить поддержку стандарта IPv4;<br />
        -6 – то же самое относительно IPv6;<br />
        -8 – применять 8-битную кодировку вроде Unicode;<br />
        -E – отключить поддержку Escape-последовательностей;<br />
        -a – автоматическое подключение под логином из переменного окружения USER;<br />
        -b – использовать локальный сокет;<br />
        -d – активировать режим отладки;<br />
        -p – включить эмуляцию rlogin;<br />
        -l – указание пользователя авторизации.<br />
        <br />
        Команды консоли telnet:<br />
        CLOSE – отключиться от удаленного сервера;<br />
        ENCRYPT – включить шифрование информации;<br />
        LOGOUT – выйти из программы с закрытием соединения;<br />
        MODE – переключение режима со строчного на символьный или наоборот;<br />
        STATUS – отобразить текущий статус соединения;<br />
        SEND – отправить один из специальных символов telnet;<br />
        SET – установить значение параметра;<br />
        OPEN – открыть соединение с удаленным сервером;<br />
        DISPLAY – отобразить применяемые спецсимволы;<br />
        SLC – изменить используемые спецсимволы.<br />
        <br /></td>
        <td width=800><br />

<code>соединение между r1 и ws22</code><br />

![report](Screenshots/NAT/r1_telnet_ws22%20command%20output.png)<br />

<code>соединение между ws22 и r1</code><br />

![report](Screenshots/NAT/ws22_telnet_r1%20command%20output.png)<br />


</td>
</tr>
</table><br />


## Part 8. Дополнительно. Знакомство с SSH Tunnels
<br />
<table>
    <tr>
        <th width=400><br />iptables<br /></th>
        </tr>
        <tr>
        <td>Применить<br />
        <br /></td>
        <td width=800><br />

<code>r2 правила</code><br />

![report](Screenshots/sshtunels/r2_rules_iptables_firewall%20command%20output.png)<br />

<code>применить правила для firewall - iptables</code><br />

![report](Screenshots/sshtunels/r2_rules_iptables_firewall_apply%20command%20output.png)<br />


</td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />iptables<br /></th>
        </tr>
        <tr>
        <td>сменить порт <br />
        <br /></td>
        <td width=800><br />

<code>ws22 - /etc/apache2/ports.conf</code><br />

![report](Screenshots/sshtunels/ws22_apache_localhost%20command%20output.png)<br />


</td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />Local TCP forwarding с ws21 до ws22<br /></th>
        </tr>
        <tr>
        <td>Local TCP forwarding<br />
        <br /></td>
        <td width=800><br />

<code>ws21/1 терминал</code><br />

![report](Screenshots/sshtunels/ws21_Local_TCP_forwarding_ws22%20command%20output.png)<br />

<code>ws21/2 терминал</code><br />

![report](Screenshots/sshtunels/ws21_telnet9999_ws22%20command%20output.png)<br />

</td>
</tr>
</table><br />

<table>
    <tr>
        <th width=400><br />Remote TCP forwarding c ws11 до ws22<br /></th>
        </tr>
        <tr>
        <td>Remote TCP forwarding<br />
        <br /></td>
        <td width=800><br />

<code>вводим команду</code><br />

![report](Screenshots/sshtunels/ws11_telnet_1999_1%20command%20output.png)<br />

<code>ws11/1 терминал</code><br />

![report](Screenshots/sshtunels/ws11_Remote_TCP_forwarding_ws22%20command%20output.png)<br />

<code>ws11/2 терминал</code><br />

![report](Screenshots/sshtunels/ws11_telnet_1999_2%20command%20output.png)<br />

</td>
</tr>
</table><br />