# Init

```bash
git clone
git submodule init
```

## Start SonarQube

```bash
docker-compose up -d
```

### Install plugins

```bash
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=crowd"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=scmgit"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=gitlab"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=kotlin"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=ldap"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=csharp"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=cssfamily"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=flex"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=go"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=web"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=javascript"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=java"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=php"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=python"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=typescript"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=xml"
curl -X POST  -u admin:admin "http://localhost:9000/api/plugins/install?key=scmsvn"
```

#### Add checkmarx plugin

```bash
docker run --rm -it -v sonarqube_sonarqube_extensions:/mnt -v "$(pwd)/sonarqube-checkmarx-solidlab-plugin-1.0.jar:/tmp/sonarqube-checkmarx-solidlab-plugin-1.0.jar" alpine:3.6 /bin/sh
### inside container
### copy jar file
cp /tmp/sonarqube-checkmarx-solidlab-plugin-1.0.jar /mnt/plugins/
### check uid/gid
ls -n /mnt/plugins/
### chown to uid/gid
chown -R 999:999 /mnt/plugins/
```

Restart SonarQube

```bash
docker-compose restart sonarqube
```

#### Scanning

```bash
docker run -it --network=sonarqube_sonarnet --rm --name my-maven-project -v ~/.m2/repository:/root/.m2  -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven/sonar-scanning-examples/sonarqube-scanner-maven/ maven:3.6-jdk-8 mvn clean verify sonar:sonar -Dsonar.host.url=http://sonarqube:9000
```