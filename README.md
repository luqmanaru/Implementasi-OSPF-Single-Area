# Implementasi-OSPF-Single-Area

Proyek routing dinamis menggunakan OSPF Single Area untuk konektivitas jaringan multi-segmen

![Cisco](https://img.shields.io/badge/Cisco-OSPF-blue?style=for-the-badge&logo=cisco&logoColor=white)
![Routing](https://img.shields.io/badge/Routing-Dynamic-green?style=for-the-badge)
![OSPF](https://img.shields.io/badge/OSPF-Single_Area-orange?style=for-the-badge)

---

## 📝 Deskripsi
Proyek ini mengimplementasikan **OSPF (Open Shortest Path First) Single Area** sebagai solusi routing dinamis untuk menghubungkan multiple segmen jaringan. Implementasi mencakup:
- Konfigurasi OSPF pada 3 router Cisco
- Segmentasi jaringan dengan subnetting efisien
- Verifikasi konektivitas end-to-end
- Analisis tabel routing dan neighbor adjacency

---

## 🏗️ Topologi Jaringan
| Perangkat | Interface | IP Address | Subnet | Koneksi |
|-----------|-----------|------------|--------|---------|
| **R1** | Fa0/0 | 192.168.1.1 | /30 | Ke R2 |
| | Fa0/1 | 192.168.10.1 | /29 | Ke PC1, PC2 |
| **R2** | Fa0/0 | 192.168.1.2 | /30 | Ke R1 |
| | Fa0/1 | 192.168.1.5 | /30 | Ke R3 |
| | Fa1/0 | 192.168.20.1 | /29 | Ke PC3, PC4 |
| **R3** | Fa0/0 | 192.168.1.6 | /30 | Ke R2 |
| | Fa0/1 | 192.168.30.1 | /29 | Ke PC5, PC6 |
| **PC1** | - | 192.168.10.2 | /29 | Ke R1 |
| **PC2** | - | 192.168.10.3 | /29 | Ke R1 |
| **PC3** | - | 192.168.20.2 | /29 | Ke R2 |
| **PC4** | - | 192.168.20.3 | /29 | Ke R2 |
| **PC5** | - | 192.168.30.2 | /29 | Ke R3 |
| **PC6** | - | 192.168.30.3 | /29 | Ke R3 |

---

## Topologi
<img width="827" height="538" alt="image" src="https://github.com/user-attachments/assets/b9ed83c7-f96c-45d5-8ce6-f1e2f7d73e12" />

---

## 📊 Output Verifikasi
### Tabel Routing R1
```
R1# show ip route

Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     192.168.1.0/30 is subnetted, 2 subnets
C       192.168.1.0 is directly connected, FastEthernet0/0
O       192.168.1.4 [110/2] via 192.168.1.2, 00:00:05, FastEthernet0/0
     192.168.10.0/29 is subnetted, 1 subnets
C       192.168.10.0 is directly connected, FastEthernet0/1
     192.168.20.0/29 is subnetted, 1 subnets
O       192.168.20.0 [110/2] via 192.168.1.2, 00:00:05, FastEthernet0/0
     192.168.30.0/29 is subnetted, 1 subnets
O       192.168.30.0 [110/3] via 192.168.1.2, 00:00:05, FastEthernet0/0
```

### OSPF Neighbor R2
```
R2# show ip ospf neighbor

Neighbor ID     Pri   State           Dead Time   Address         Interface
192.168.1.1       1   FULL/BDR        00:00:39    192.168.1.1     FastEthernet0/0
192.168.1.6       1   FULL/BDR        00:00:39    192.168.1.6     FastEthernet0/1
```

### OSPF Database R3
```
R3# show ip ospf database

            OSPF Router with ID (192.168.1.6) (Process ID 1)

                Router Link States (Area 0)

Link ID         ADV Router      Age         Seq#       Checksum Link count
192.168.1.1     192.168.1.1     321         0x80000003 0x00C5F3 2
192.168.1.2     192.168.1.2     256         0x80000004 0x00A5B2 3
192.168.1.6     192.168.1.6     198         0x80000003 0x008A91 2

                Net Link States (Area 0)

Link ID         ADV Router      Age         Seq#       Checksum
192.168.1.1     192.168.1.1     321         0x80000001 0x00E7D4
192.168.1.2     192.168.1.2     256         0x80000001 0x00C6A3
192.168.1.5     192.168.1.2     256         0x80000001 0x00A572
```

### Konektivitas End-to-End
```
PC1> ping 192.168.30.2

Pinging 192.168.30.2 with 32 bytes of data:
Reply from 192.168.30.2: bytes=32 time=15ms TTL=125
Reply from 192.168.30.2: bytes=32 time=10ms TTL=125
Reply from 192.168.30.2: bytes=32 time=12ms TTL=125
Reply from 192.168.30.2: bytes=32 time=11ms TTL=125

Ping statistics for 192.168.30.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 10ms, Maximum = 15ms, Average = 12ms
```

---

**luqmanaru**  
