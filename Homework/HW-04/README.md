


```bash
Cdevdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker network create app-net
b056b63cf7ba64ef464b94292eee6b8a3ed6503157f5d221de06bfcd579756e7
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker volume create db-data
db-data
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker run -d \
>   --name db-server \
>   --network app-net \
>   -v db-data:/var/lib/postgresql/data \
>   -e POSTGRES_USER=postgres \
>   -e POSTGRES_PASSWORD=postgres \
>   -e POSTGRES_DB=testdb \
>   postgres:15-alpine
Unable to find image 'postgres:15-alpine' locally

15-alpine: Pulling from library/postgres
277e2289225f: Pull complete
2c2e40dd947e: Pull complete
2e9987a42d41: Pull complete
4f83103187f5: Pull complete
6ba2251a51ae: Pull complete
3f49193fd82d: Pull complete
bc2205dd5a3a: Pull complete
c020dab2e853: Pull complete
0976f43b012c: Pull complete
e9516be90840: Pull complete
697de61d3cc1: Download complete
d3e3f1b947dc: Download complete
Digest: sha256:f7d23353e1b15400d22ebe31189f4d314b87a4c129cc400c8c2d8d4ca127bf81
Status: Downloaded newer image for postgres:15-alpine
0519bfbcc785f94240b42a3a0eebfd4f9ee31e7f56a9e50571844856f461590d
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ sleep 5
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ sleep 5
;"
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -i db-server psql -U postgres -d testdb -c "SELECT * FROM users;"
ERROR:  relation "users" does not exist
LINE 1: SELECT * FROM users;
                      ^
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -i db-server psql -U postgres -d testdb -c "SELECT * FROM users;"
ERROR:  relation "users" does not exist
LINE 1: SELECT * FROM users;
                      ^
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -i db-server psql -U postgres -d testdb -c "CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(50), email VARCHAR(50)); INSERT INTO users (name, email) VALUES ('Nguyen Van A', 'a@example.com'), ('Tran Van B', 'b@example.com');"
CREATE TABLE
INSERT 0 2
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -i db-server psql -U postgres -d testdb -c "SELECT * FROM users;"
 id |     name     |     email
----+--------------+---------------
  1 | Nguyen Van A | a@example.com
  2 | Tran Van B   | b@example.com
(2 rows)

devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -i db-server psql -U postgres -d testdb -c "CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(50), email VARCHAR(50)); INSERT INTO users (name, email) VALUES ('Nguyen Van A', 'a@example.com'), ('Tran Van B', 'b@example.com');"
ERROR:  relation "users" already exists
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker rm -f db-server
db-server
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker run -d \
>   --name db-server \
>   --network app-net \
>   -v db-data:/var/lib/postgresql/data \
>   -e POSTGRES_USER=postgres \
>   -e POSTGRES_PASSWORD=postgres \
>   -e POSTGRES_DB=testdb \
>   postgres:15-alpine
b22ad428cece68d9510b3b1df276edb078e276d022bf1dc660af6a652485c277
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ sleep 5
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -i db-server psql -U postgres -d testdb -c "SELECT * FROM users;"
 id |     name     |     email
----+--------------+---------------
  1 | Nguyen Van A | a@example.com
  2 | Tran Van B   | b@example.com
(2 rows)

devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker network ls | grep app-net
b056b63cf7ba   app-net                                   bridge    local
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker volume ls | grep db-data
local     db-data
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker volume ls | grep db-data
local     db-data
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker network inspect app-net
[
    {
        "Name": "app-net",
        "Id": "b056b63cf7ba64ef464b94292eee6b8a3ed6503157f5d221de06bfcd579756e7",
        "Created": "2026-10-11T11:31:43.872313045Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Options": {},
        "Labels": {},
        "Containers": {
            "b22ad428cece68d9510b3b1df276edb078e276d022bf1dc660af6a652485c277": {
                "Name": "db-server",
                "EndpointID": "b27b4aed3a9d40487a0af4c081fcc38b6f0a9212af2584b357a8efe2d8778216",
                "MacAddress": "c6:f0:1d:00:55:72",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            }
        },
        "Status": {
            "IPAM": {
                "Subnets": {
                    "172.19.0.0/16": {
                        "IPsInUse": 4,
                        "DynamicIPsAvailable": 65532
                    }
                }
            }
        }
    }
]
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker run -d \
>   --name app-container \
>   --network app-net \
>   -e DB_HOST=db-server \
>   -e DB_PORT=5432 \
>   -e DB_NAME=testdb \
>   -e DB_USER=postgres \
>   -e DB_PASSWORD=postgres \
>   alpine sh -c "while true; do sleep 3600; done"
4f42c7c46476f75c71cd2e3a87c1805fb736c03026c54fa71d7e1fe16c4190e6
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker network inspect app-net
[
    {
        "Name": "app-net",
        "Id": "b056b63cf7ba64ef464b94292eee6b8a3ed6503157f5d221de06bfcd579756e7",
        "Created": "2026-10-11T11:31:43.872313045Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Options": {},
        "Labels": {},
        "Containers": {
            "4f42c7c46476f75c71cd2e3a87c1805fb736c03026c54fa71d7e1fe16c4190e6": {
                "Name": "app-container",
                "EndpointID": "dbbeaec2dc564aa35b2cfe6b68ab1be90c175b0dca9c040ecdf785634f05dcfd",
                "MacAddress": "76:fe:1e:ce:4b:08",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            },
            "b22ad428cece68d9510b3b1df276edb078e276d022bf1dc660af6a652485c277": {
                "Name": "db-server",
                "EndpointID": "b27b4aed3a9d40487a0af4c081fcc38b6f0a9212af2584b357a8efe2d8778216",
                "MacAddress": "c6:f0:1d:00:55:72",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            }
        },
        "Status": {
            "IPAM": {
                "Subnets": {
                    "172.19.0.0/16": {
                        "IPsInUse": 5,
                        "DynamicIPsAvailable": 65531
                    }
                }
            }
        }
    }
]
``` 

**Kết quả**:
```bash
devdocker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker exec -it app-container ping -c 2 db-server
PING db-server (172.19.0.2): 56 data bytes
64 bytes from 172.19.0.2: seq=0 ttl=64 time=0.092 ms
64 bytes from 172.19.0.2: seq=1 ttl=64 time=0.072 ms

--- db-server ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.072/0.082/0.092 ms
```