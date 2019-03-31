---
layout: post
title:  "p2p原理"
date:   2015-09-06 13:21:30
categories: kong
---

### NAT/NAPT

```
                 Server S1                 
             18.181.0.31:1235                 
                     |
^ Session 1 (A-S1)   ^
| 18.181.0.31:1235   |
v 155.99.25.11:62000 v   
                     |
                    NAT
               155.99.25.11
                     |
  ^ Session 1 (A-S1) ^
  | 18.181.0.31:1235 |
  v   10.0.0.1:1234  v
                     |
                  Client A
               10.0.0.1:1234
```

### Cone NAT
```
  Server S1                         Server S2
18.181.0.31:1235                     138.76.29.7:1235
    |                               |
    |                               |
    +----------------------+----------------------+
                    |
^Session 1 (A-S1)   ^     |     ^ Session 2 (A-S2)   ^
|18.181.0.31:1235   |     |     | 138.76.29.7:1235   |
v155.99.25.11:62000 v     |     v 155.99.25.11:62000 v
                    |
                  Cone NAT
                155.99.25.11
                    |
 ^ Session 1 (A-S1) ^     |     ^ Session 2 (A-S2) ^
 | 18.181.0.31:1235 |     |     | 138.76.29.7:1235 |
 v   10.0.0.1:1234  v     |     v   10.0.0.1:1234  v
                    |
                 Client A
               10.0.0.1:1234
```

|    |                             |
|:---|:----------------------------|
| 1  | Full Cone NAT               |
| 2  | Address-Restricted Cone NAT |
| 3  | Port-Restricted Cone NAT    |
| 4  | Symmetric NAT               |

