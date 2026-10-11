# Bài 2: Đóng gói ứng dụng Web Backend bằng Single-stage Dockerfile

```bash
dev_docker@ip-172-31-42-200:~$ cd ~/PTIT_CNTT1_IT209_TestDeploy-VPS
dev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker compose down -v
[+] down 4/4
 ✔ Container backend-app                             Removed                                                        1.4s ✔ Container demo-deploy-vps                         Removed                                                        3.9s ✔ Volume ptit_cntt1_it209_testdeploy-vps_mysql-data Removed                                                        0.0s ✔ Network ptit_cntt1_it209_testdeploy-vps_default   Removed                                                        0.1sdev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker compose build --no-cache
[+] Building 91.7s (16/16) FINISHED
 => [internal] load local bake definitions                                                                         0.0s
 => => reading from stdin 624B                                                                                     0.0s
 => [internal] load build definition from Dockerfile                                                               0.0s
 => => transferring dockerfile: 339B                                                                               0.0s
 => [internal] load metadata for docker.io/library/gradle:9.4.1-jdk17-alpine                                       0.8s
 => [internal] load metadata for docker.io/library/eclipse-temurin:17-jre-alpine                                   0.8s
 => [internal] load .dockerignore                                                                                  0.0s
 => => transferring context: 2B                                                                                    0.0s
 => [build 1/5] FROM docker.io/library/gradle:9.4.1-jdk17-alpine@sha256:0cf1585fde964bdcd4551019c52b9f4f4a611d5b0  0.1s
 => => resolve docker.io/library/gradle:9.4.1-jdk17-alpine@sha256:0cf1585fde964bdcd4551019c52b9f4f4a611d5b031d659  0.0s
 => [stage-1 1/3] FROM docker.io/library/eclipse-temurin:17-jre-alpine@sha256:3c472129dc75a8d1d7a3f2df5b2093a8077  0.1s
 => => resolve docker.io/library/eclipse-temurin:17-jre-alpine@sha256:3c472129dc75a8d1d7a3f2df5b2093a8077e4493def  0.0s
 => [internal] load build context                                                                                  0.1s
 => => transferring context: 3.23kB                                                                                0.0s
 => CACHED [stage-1 2/3] WORKDIR /app                                                                              0.0s
 => CACHED [build 2/5] WORKDIR /app                                                                                0.0s
 => [build 3/5] COPY . .                                                                                           0.3s
 => [build 4/5] RUN chmod +x gradlew                                                                               0.6s
 => [build 5/5] RUN ./gradlew clean bootJar --no-daemon                                                           80.7s
 => [stage-1 3/3] COPY --from=build /app/build/libs/*.jar app.jar                                                  0.3s
 => exporting to image                                                                                             3.4s
 => => exporting layers                                                                                            2.6s
 => => exporting manifest sha256:46c7cd1399304866349eef73cbfa8bcd8e78d72a6b08d20d4d2df9e951d91d4a                  0.0s
 => => exporting config sha256:29ae322404c70f5bc53f3d2c47751273f39dd820b95c5d19b72e5c8cdb65bab1                    0.0s
 => => exporting attestation manifest sha256:75b2426ff4e7f67f722356c581b0678048b3b6d5e0a62c53e46a87cadf758b0f      0.0s
 => => exporting manifest list sha256:93d2a9903accf54bf74246ae3008eceae9cc5715932e2dda2e44e4208c561fd7             0.0s
 => => naming to docker.io/library/ptit_cntt1_it209_testdeploy-vps-backend:latest                                  0.0s
 => => unpacking to docker.io/library/ptit_cntt1_it209_testdeploy-vps-backend:latest                               0.5s
 => resolving provenance for metadata file                                                                         0.4s
[+] build 1/1
 ✔ Image ptit_cntt1_it209_testdeploy-vps-backend Built                                                             92.1sdev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker compose up -d
[+] up 4/4
 ✔ Network ptit_cntt1_it209_testdeploy-vps_default   Created                                                        0.1s ✔ Volume ptit_cntt1_it209_testdeploy-vps_mysql-data Created                                                        0.0s ✔ Container demo-deploy-vps                         Started                                                        0.7s ✔ Container backend-app                             Started                                                        0.8s
 
 dev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ docker logs backend-app

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/

 :: Spring Boot ::                (v4.1.1)

2026-10-10T17:02:09.310Z  INFO 1 --- [demo-deploy-vps] [           main] m.d.DemoDeployVpsApplication             : Starting DemoDeployVpsApplication v0.0.1-SNAPSHOT using Java 17.0.20.1 with PID 1 (/app/app.jar started by root in /app)
2026-10-10T17:02:09.339Z  INFO 1 --- [demo-deploy-vps] [           main] m.d.DemoDeployVpsApplication             : No active profile set, falling back to 1 default profile: "default"
2026-10-10T17:02:11.844Z  INFO 1 --- [demo-deploy-vps] [           main] o.s.boot.tomcat.TomcatWebServer          : Tomcat initialized with port 8089 (http)
2026-10-10T17:02:11.880Z  INFO 1 --- [demo-deploy-vps] [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2026-10-10T17:02:11.881Z  INFO 1 --- [demo-deploy-vps] [           main] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/11.0.24]
2026-10-10T17:02:11.940Z  INFO 1 --- [demo-deploy-vps] [           main] b.w.c.s.WebApplicationContextInitializer : Root WebApplicationContext: initialization completed in 2417 ms
2026-10-10T17:02:12.827Z  INFO 1 --- [demo-deploy-vps] [           main] o.s.boot.tomcat.TomcatWebServer          : Tomcat started on port 8089 (http) with context path '/'
2026-10-10T17:02:12.866Z  INFO 1 --- [demo-deploy-vps] [           main] m.d.DemoDeployVpsApplication             : Started DemoDeployVpsApplication in 4.931 seconds (process running for 7.465)
dev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ curl -i http://localhost:8089/
HTTP/1.1 404
Content-Type: application/json
Transfer-Encoding: chunked
Date: Sat, 10 Oct 2026 17:03:43 GMT

{"timestamp":"2026-10-10T17:03:43.672Z","status":404,"error":"Not Found","path":"/"}dev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ curl -i http://localhost:8080/
curl: (7) Failed to connect to localhost port 8080 after 0 ms: Could not connect to server
dev_docker@ip-172-31-42-200:~/PTIT_CNTT1_IT209_TestDeploy-VPS$ curl -i http://localhost:8089/api/v1/app
HTTP/1.1 200
Content-Type: application/json
Content-Length: 36
Date: Sat, 10 Oct 2026 17:04:49 GMT

["String 1","String 02","String 03"]
```