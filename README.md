# Start SonarQube

```bash
docker-compouse up -d
```

## Install plugins

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

### Add checkmarx plugin

```bash
docker run --rm -it -v sonarqube_sonarqube_extensions:/mnt -v "$(pwd)/sonar-checkmarx-plugin-solidlab-webportal-1.0.jar:/tmp/sonar-checkmarx-plugin-solidlab-webportal-1.0.jar" alpine:3.6 /bin/sh
### inside container
### check uid/gid
ls -n /mnt/plugins/
### chown to uid/gid
chown 999:999 /mnt/plugins/sonar-checkmarx-plugin-solidlab-webportal-1.0.jar
```

Restart SonarQube

```bash
docker-compose restarr sonarqube
```


https://github.com/SonarSource/sonar-scanning-examples/tree/master/sonarqube-scanner-maven