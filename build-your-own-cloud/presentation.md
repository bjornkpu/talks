---
defaultTemplate: "[[DefaultTemplate]]"
theme: themes/talks
---

# Build Your Own Cloud

## Dev, DevOps & Ops
>
> Bjørn Kristian Punsvik\
> November, 2025

---
<split even gap="1" no-margin>
![[profile.jpg|400]]

```yaml
bk@crayon:~$ whoami
--------------------
Name:       Bjørn Kristian Punsvik
Role:       Software Developer
Position:   Senior Consultant
Location:   Trondheim
Uptime:     30 years
Experience: 5 years
Education:  B.Sc. Computer Science, NTNU

bk@crayon:~$ ps -a
--------------------
PID   COMMAND                      TIME
1001  /usr/bin/linux-server-admin  9y
1002  /usr/bin/kubernetes          5y
1003  /usr/bin/aws                 2y
1004  /usr/bin/azure               3y
1005  /usr/bin/devops              2y
```
<!-- element style="font-size: 1em;padding-bottom: 10px;" -->
</split>
note:
- Have been on both sides

---
<!-- .slide: data-auto-animate -->
# Development

![[byoc-dev.png|200]]

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::

![[byoc-12-factor.png]]
<https://12factor.net/>
notes:
SaaS
heroku 2011

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
![[byoc-12-factor.png|800]]
:::
<grid drag="20 70" drop="center" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
**I. Codebase**

II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
![[https://12factor.net/images/codebase-deploys.png]]  <!-- element style="background-color: #f0f0f0; border-radius: 10px; padding: 10px;" -->
</grid>
<grid drag="80 20" drop="bottom">
> One codebase tracked in revision control, many deploys
</grid>

notes:
There is always a one-to-one correlation between the codebase and the app

- **GitHub**: Single repository with branches for different deploys
- **.NET**: Solution/project files tracked in git
- **GitHub Actions**: Workflows triggered from the same codebase
- **Docker/K8s**: Same Dockerfile/manifests deployed to different environments

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase

**II. Dependencies**

III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
 **A twelve-factor app never relies on implicit existence of system-wide packages.**
</grid>
<grid drag="80 20" drop="bottom">
> Explicitly declare and isolate dependencies
</grid>

notes:
- **.NET**: `*.csproj` files explicitly declare NuGet packages; `dotnet restore` isolates dependencies
- **Docker**: Multi-stage builds with SDK image downloads and caches dependencies
- **Kubernetes**: Container images are immutable with locked dependencies
- **GitHub Actions**: Lock files ensure consistent dependency versions in CI
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies

**III. Config**

IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
An app’s _config_ is everything that is likely to vary between [deploys](https://12factor.net/codebase) (staging, production, developer environments, etc).

This includes:

- Resource handles to the database, Memcached, and other [backing services](https://12factor.net/backing-services)
- Credentials to external services such as Amazon S3 or Twitter
- Per-deploy values such as the canonical hostname for the deploy

**The twelve-factor app stores config in _environment variables_** (often shortened to _env vars_ or _env_).
</grid>

<grid drag="80 20" drop="bottom">
> Store config in the environment
</grid>

notes:
A litmus test -> open source at any moment

- **.NET**: `appsettings.json` + environment variables; `IConfiguration` reads from env vars
- **Docker**: `ENV` directives and runtime `-e` flags
- **Kubernetes**: ConfigMaps and Secrets injected as environment variables
- **GitHub Actions**: Repository secrets and environment variables in workflows
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config

**IV. Backing services**

V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
 ![[https://12factor.net/images/attached-resources.png]] <!-- element style="background-color: #f0f0f0; border-radius: 10px; padding: 10px;" -->
</grid>
<grid drag="80 20" drop="bottom">
> Treat backing services as attached resources
</grid>

notes:
The code for a twelve-factor app makes no distinction between local and third party services. 

- **.NET**: Connection strings as config; dependency injection for service abstraction
- **Kubernetes**: Services provide stable endpoints; backing services run as separate deployments
- **Docker**: Services linked via networks; no distinction between local/remote databases
- **GitHub Actions**: External services (registries, databases) accessed via config
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services

**V. Build, release, run**

VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
  ![[https://12factor.net/images/release.png]] <!-- element style="background-color: #f0f0f0; border-radius: 10px; padding: 10px;" -->
</grid>
<grid drag="80 20" drop="bottom">
> Strictly separate build and run stages
</grid>

notes:
three stages:\
The build stage,executable bundle.\
The release stage, build + deploy’s current config\
The run stage, runs the app.

The twelve-factor app uses strict separation between the build, release, and run stages.

- **.NET**: `dotnet build` → `dotnet publish` → `dotnet run` separation
- **Docker**: Build stage (`docker build`) separate from run (`docker run`)
- **GitHub Actions**: Build jobs create artifacts, deploy jobs release them
- **Kubernetes**: Image tags as releases; deployments manage running instances

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run

**VI. Processes**

VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
The app is executed in the execution environment as one or more processes.

**Twelve-factor processes are stateless and [share-nothing](http://en.wikipedia.org/wiki/Shared_nothing_architecture).** Any data that needs to persist must be stored in a stateful [backing service](https://12factor.net/backing-services), typically a database.

</grid>
<grid drag="80 20" drop="bottom">
> Execute the app as one or more stateless processes
</grid>

notes:
- **.NET**: Stateless ASP.NET Core apps; session state in Redis/external store
- **Docker**: Containers are stateless; ephemeral filesystem
- **Kubernetes**: Pods are cattle not pets; StatefulSets for stateful workloads
- **GitHub Actions**: Each job runs in isolated, stateless runners

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes

**VII. Port binding**

VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
  The twelve-factor app is completely *self-contained* and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service. The web app exports HTTP as a service by *binding to a port*, and listening to requests coming in on that port.
</grid>
<grid drag="80 20" drop="bottom">
> Export services via port binding
</grid>

notes:
- **.NET**: Kestrel web server binds to port (e.g., `ASPNETCORE_URLS=http://+:8080`)
- **Docker**: `EXPOSE` declares port; self-contained web server in container
- **Kubernetes**: Service exports pod ports; no external web server injection
- **GitHub Actions**: Build and test self-contained services

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding

**VIII. Concurrency**

IX. Disposability\
X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
 ![[https://12factor.net/images/process-types.png]] <!-- element style="background-color: #f0f0f0; border-radius: 10px; padding: 10px;" -->
</grid>
<grid drag="80 20" drop="bottom">
> Scale out via the process model
</grid>

notes:
processes are a first class citizen.\
unix process model for running service daemons. Using this model, HTTP requests may be handled by a web process, and long-running background tasks handled by a worker process.

- **.NET**: Multiple process instances handle load; async/await for I/O concurrency
- **Docker**: Run multiple containers of same image
- **Kubernetes**: Horizontal Pod Autoscaler scales replicas; different deployment types (web, worker)
- **GitHub Actions**: Matrix builds for parallel execution; ARC scales runners

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency

**IX. Disposability**

X. Dev/prod parity\
XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
The twelve-factor app’s processes are disposable, meaning they can be started or stopped at a moment’s notice.
  
Processes should strive to minimize startup time. Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs. 
</grid>
<grid drag="80 20" drop="bottom">
> Maximize robustness with fast startup and graceful shutdown
</grid>

notes:
SIGTERM

- **.NET**: Graceful shutdown handling (`IHostApplicationLifetime`); fast startup optimizations
- **Docker**: Containers handle SIGTERM; lightweight Alpine images for fast starts
- **Kubernetes**: Liveness/readiness probes; rolling updates expect disposability
- **GitHub Actions**: Ephemeral runners start/stop per job

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\

**X. Dev/prod parity**

XI. Logs\
XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
**The twelve-factor app is designed for [continuous deployment](http://avc.com/2011/02/continuous-deployment/) by keeping the gap between development and production small.**
![[byoc-parity-table.png]] <!-- element style="background-color: #f0f0f0; border-radius: 10px; padding: 10px;" -->
Resists the urge to use different backing services between development and production
</grid>
<grid drag="80 20" drop="bottom">
> Keep development, staging, and production as similar as possible
</grid>

notes:
- **.NET**: Same runtime version across environments; configuration difference only
- **Docker**: Same container image runs in dev/staging/prod
- **Kubernetes**: Same manifests applied to different clusters/namespaces
- **GitHub Actions**: Test on same OS/runtime as production; preview environments

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\

**XI. Logs**

XII. Admin processes
</grid>
<grid drag="80 70" drop="right" >
_Logs_ provide visibility into the behavior of a running app.

**A twelve-factor app never concerns itself with routing or storage of its output stream.**
</grid>
<grid drag="80 20" drop="bottom">
> Treat logs as event streams
</grid>

notes:
- **.NET**: `ILogger` writes to stdout/stderr; structured logging (JSON)
- **Docker**: `docker logs` captures stdout/stderr streams
- **Kubernetes**: Aggregates container logs; integrates with logging platforms
- **GitHub Actions**: Job logs captured as streams; can ship to external systems

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
<grid drag="20 70" drop="left" align="left">
I. Codebase\
II. Dependencies\
III. Config\
IV. Backing services\
V. Build, release, run\
VI. Processes\
VII. Port binding\
VIII. Concurrency\
IX. Disposability\
X. Dev/prod parity\
XI. Logs

**XII. Admin processes**

</grid>
<grid drag="80 70" drop="right" >
developers will often wish to do one-off administrative or maintenance tasks for the app, such as:

- Running database migrations
- Running a console (also known as a [REPL](http://en.wikipedia.org/wiki/Read-eval-print_loop) shell) to run arbitrary code or inspect the app’s models against the live database
- Running one-time scripts committed into the app’s repo (e.g. `php scripts/fix_bad_records.php`)

</grid>
<grid drag="80 20" drop="bottom">
> Run admin/management tasks as one-off processes
</grid>

notes:
- **.NET**: `dotnet ef database update` for migrations; console apps for one-off tasks
- **Kubernetes**: Jobs and CronJobs for one-time/scheduled tasks; same image as app
- **Docker**: `docker exec` or run containers with different commands
- **GitHub Actions**: Manual workflow triggers for admin tasks; migration jobs in pipelines

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
# Dotnet

## `10.0.100-rc.2`

```shell
winget install Microsoft.DotNet.SDK.Preview
winget install Microsoft.DotNet.Runtime.Preview
winget install Microsoft.DotNet.AspNetCore.Preview
```

```shell
 dotnet new webapp -lang C# -f net10.0 -n byoc -o . --exclude-launch-settings --no-https
```

note:
October 14, 2025
LTS
change index.html

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# .gitignore
:::
```
# Downloaded content

# Built content

# User files

# Temp files

# Secrets

```

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# .gitignore
:::
```
# Downloaded content

# Built content
bin
obj
# User files
.vscode
.idea
# Temp files
*.log
# Secrets
.env
```

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# .dockerignore
:::
```
# Downloaded content

# Built content
bin
obj
# User files
.vscode
.idea
# Temp files
*.log
# Secrets
.env
# Non production files
```

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# .dockerignore
:::
```
# Downloaded content

# Built content
bin
obj
# User files
.vscode
.idea
# Temp files
*.log
# Secrets
.env
# Non production files
appsettings.Development.json
**/launchSettings.json
```
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Dockerfile
:::
``` [1-16]
FROM
COPY
RUN
CMD
```
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Dockerfile
:::
``` [1-7]
FROM mcr.microsoft.com/dotnet/sdk:10.0-alpine
COPY . .
RUN dotnet restore
RUN dotnet build -c Release
RUN dotnet test -c Release
RUN dotnet publish -c Release -o /dist
CMD
```
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Dockerfile
:::
``` [7-111]
FROM mcr.microsoft.com/dotnet/sdk:10.0-alpine
COPY . .
RUN dotnet restore
RUN dotnet build -c Release
RUN dotnet test -c Release
RUN dotnet publish -c Release -o /dist
ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production
EXPOSE 8080
CMD ["dotnet", "byoc.dll"]
```

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Dockerfile
:::
```[1,2,9,13,14]
FROM mcr.microsoft.com/dotnet/sdk:10.0-alpine AS build
WORKDIR /src
COPY . .
RUN dotnet restore
RUN dotnet build -c Release
RUN dotnet test -c Release
RUN dotnet publish -c Release -o /dist

FROM mcr.microsoft.com/dotnet/aspnet:10.0-alpine
ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production
EXPOSE 8080
WORKDIR /app
COPY --from=build /dist .
CMD ["dotnet", "byoc.dll"]
```
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Dockerfile
:::
```[3-5]
FROM mcr.microsoft.com/dotnet/sdk:10.0-alpine AS build
WORKDIR /src
COPY byoc.csproj .
RUN dotnet restore
COPY . .
RUN dotnet build -c Release
RUN dotnet test -c Release
RUN dotnet publish -c Release -o /dist

FROM mcr.microsoft.com/dotnet/aspnet:10.0-alpine
ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production
EXPOSE 8080
WORKDIR /app
COPY --from=build /dist .
CMD ["dotnet", "byoc.dll"]
```

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Dockerfile
:::
```
FROM mcr.microsoft.com/dotnet/sdk:10.0-alpine AS build
WORKDIR /src
COPY byoc.csproj .
RUN dotnet restore
COPY . .
RUN dotnet build -c Release
RUN dotnet test -c Release
RUN dotnet publish -c Release -o /dist

FROM mcr.microsoft.com/dotnet/aspnet:10.0-alpine
ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production
EXPOSE 8080
WORKDIR /app
COPY --from=build /dist .
CMD ["dotnet", "byoc.dll"]
```

---
<!-- .slide: data-auto-animate -->
# Operations

![[byoc-ops.png|200]]

note:
the cloud

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# CNCF
:::
![[byoc-cncf.png|800]]<!-- element style="border-radius: 10px;margin-top:100px" -->
<https://cncf.io/>

note:
"CNCF's mission is to make cloud native computing ubiquitous..."

Ubiquitous means existing or being everywhere at the same time; it describes something that is constantly encountered or widespread.

https://www.cncf.io/

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Kubernetes (k8s)
:::
![[byoc-k8s.png]]<!-- element style="border-radius: 10px;" -->
notes:
management of containerized applications

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Kubernetes Architecture
:::

![[kubernetes.excalidraw]]<!-- element style="border-radius: 10px;" -->
notes:
- admin path
- user path

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Kubernetes Cluster
:::

![[cluster.excalidraw|600]]<!-- element style="border-radius: 10px;margin-top: 100px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Kubernetes Deployment
:::

![[deployment.excalidraw|300]]<!-- element style="border-radius: 10px;" -->


---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Kubernetes manifest
## `k8s.yml` - Deployment
::: <!-- element style="margin-top:50px" -->
```yml [2,5,18,21,28]
apiVersion: apps/v1
kind: Deployment
metadata:
  namespace: crayon
  name: build-your-own-cloud
spec:
  replicas: 1
  selector:
    matchLabels:
      app: build-your-own-cloud
  template:
    metadata:
      labels:
        app: build-your-own-cloud
        version: IMAGE_LABEL
    spec:
      imagePullSecrets:
        - name: regcred
      containers:
        - name: build-your-own-cloud
          image: ghcr.io/punsvikcloud/build-your-own-cloud:IMAGE_LABEL
          imagePullPolicy: Always
          resources:
            limits:
              memory: "128Mi"
              cpu: "500m"
          ports:
            - containerPort: 8080
```
 <!-- element  style="font-size: 0.9em;height: 70%;width:70%;margin-top:150px;" -->
 
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Kubernetes manifest
## `k8s.yml` - Service
::: <!-- element style="margin-top:50px" -->
```yml [2,8,10]
apiVersion: v1
kind: Service
metadata:
  namespace: crayon
  name: crayon-service
spec:
  selector:
    app: build-your-own-cloud
  ports:
    - port: 8080
```
 <!-- element style="width:40%;" -->
 
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Kubernetes manifest
## `k8s.yml` - Ingress
::: <!-- element style="margin-top:50px" -->
```yml [2,5,11,17,24,26]
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  namespace: crayon
  name: crayon-ingress
  labels:
    name: crayon-ingress
  annotations:
    cert-manager.io/cluster-issuer: lets-encrypt
spec:
  ingressClassName: nginx
  tls:
    - hosts:
        - crayon.punsvik.net
      secretName: tls-secret
  rules:
    - host: crayon.punsvik.net
      http:
        paths:
          - pathType: Prefix
            path: "/"
            backend:
              service:
                name: crayon-service
                port:
                  number: 8080
```
 <!-- element style="height: 75%;width:50%;margin-top:150px;" -->
 
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-dev.png|200]]
:::
::: title
# Kubernetes manifest
## `k8s.yml` - Ingress
::: <!-- element style="margin-top:50px" -->
```yml [9,14,15]
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  namespace: crayon
  name: crayon-ingress
  labels:
    name: crayon-ingress
  annotations:
    cert-manager.io/cluster-issuer: lets-encrypt
spec:
  ingressClassName: nginx
  tls:
    - hosts:
        - crayon.punsvik.net
      secretName: tls-secret
  rules:
    - host: crayon.punsvik.net
      http:
        paths:
          - pathType: Prefix
            path: "/"
            backend:
              service:
                name: crayon-service
                port:
                  number: 8080
```
 <!-- element style="height: 75%;width:50%;margin-top:150px;" -->
 
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# cert-manager
:::
![[cert-manager.svg|600]]<!-- element style="border-radius: 10px;" -->
<https://github.com/cert-manager/cert-manager>

notes:
- certificates and certificate issuers as resource types
- obtaining, renewing, using

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Cloudflare DNS
:::
![[https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fnamecheap.simplekb.com%2FSiteContents%2F2-7C22D5236A4543EB827F3BD8936E153E%2Fmedia%2Fcloudflare_09.png&f=1&nofb=1&ipt=012bb228632a26235471b8da50bf3309981aab44c68d4e0026d6cc91b65d1a89|800]]<!-- element style="border-radius: 10px;margin-top:100px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Let's Encrypt
## Domain Validation
::: <!-- element style="margin-top:50px" -->
![[https://letsencrypt.org/images/howitworks_challenge.png|600]]<!-- element style="border-radius: 10px;margin-top:150px;" -->
![[https://letsencrypt.org/images/howitworks_authorization.png|600]]<!-- element style="border-radius: 10px;" -->


notes:
- Automatic Certificate Management Environment (ACME)
- what do I have to do? challenges. eks. DNS record/HTTP resource.
- provision, all clear, check, ok.

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# Let's Encrypt
## Certificate Issuance
::: <!-- element style="margin-top:50px" -->
![[https://letsencrypt.org/images/howitworks_certificate.png|600]]<!-- element style="border-radius: 10px;" -->

notes:
- ask for cert
- verify and give.

---
<!-- .slide: data-auto-animate -->
# DevOps

![[byoc-devops.png|200]]

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# DevOps
:::
![[devops.png|600]]<!-- element style="border-radius: 10px;" -->

notes:
- CI, CD & CD
- V. Build, release, run

---

![[https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fchristosgalano.github.io%2Fassets%2Fimages%2Fgithub%2Factions%2Fgithub-actions-1.webp&f=1&nofb=1&ipt=2bdf0a87ed24ef66b626f4ae8017fcffbd41728e3258f0969711a91cacb7527a|600]]<!-- element style="border-radius: 10px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-ops.png|100]]
:::
::: title
# GitHub Action Runners
:::
![[https://docs.github.com/assets/cb-497738/mw-1440/images/help/actions/arc-diagram.webp]]<!-- element style="border-radius: 10px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# GitHub Action - Runners
:::
![[byoc-runners.png]]

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# GitHub Action - Secrets
:::
![[byoc-secrets.png|800]]

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# GitHub Action
## `.github/workflows/deploy.yml` - Metadata
:::<!-- element style="margin-top:50px" -->
```yml [1,6,7,16,19]
name: Docker Build & Kubernetes Run

on:
  push:
    branches:
      - main
  workflow_dispatch:

env:
  REGISTRY: ghcr.io
  PLATFORMS: linux/arm64
  K8S_NAMESPACE: crayon

jobs:
  build:
    runs-on: self-hosted
    permissions:
      contents: read
      packages: write
      attestations: write
      id-token: write
    steps:
      ...
```
 <!-- element style="height:70%;width:50%;margin-top:150px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# GitHub Action
## `.github/workflows/deploy.yml` - Build
:::<!-- element style="margin-top:50px" -->
<grid drag="45" drop="left">
```yml [2,4,8,13]
 - name: Checkout Code
	uses: actions/checkout@v4
 - name: Set up Docker Buildx
	uses: docker/setup-buildx-action@v3
	with:
	  driver: kubernetes
 - name: Docker Login
	uses: docker/login-action@v3.3.0
	with:
	  registry: ${{ env.REGISTRY }}
	  username: ${{ github.actor }}
	  password: ${{ secrets.GITHUB_TOKEN  }}
	  logout: true
```
 <!-- element style="height:100%;width:100%;margin-top:150px;" -->
</grid>
<grid drag="50" drop="right" >
```yml [3,10,13]
 - name: Extract metadata (tags, labels) for Docker
	id: meta
	uses: docker/metadata-action@v5
	with:
	  images: ${{ env.REGISTRY }}/${{ github.repository }}
	  flavor: latest=true
	  tags: |
		type=ref,event=branch
		type=raw,value=latest,enable={{is_default_branch}}
		type=raw,value=${{ github.sha }}
 - name: Build and push Docker image
	id: push
	uses: docker/build-push-action@v6
	with:
	  context: .
	  push: true
	  platforms: linux/arm64
	  tags: ${{ steps.meta.outputs.tags }}
	  labels: ${{ steps.meta.outputs.labels }}
```
 <!-- element style="font-size: 0.8em;height:100%;width:100%;margin-top:150px;" -->
</grid>

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# GitHub Action
## `.github/workflows/deploy.yml` - Deploy
:::<!-- element style="margin-top:50px" -->
<grid drag="45" drop="left">
```yml [2,10,13,20]
 deploy:
	runs-on: self-hosted
	needs: build
	permissions:
	  id-token: write
	  actions: read
	  contents: read
	steps:
	  - name: Checkout Code
		uses: actions/checkout@v4
	
	  - name: Log in to the Container registry
		uses: docker/login-action@v3
		with:
		  registry: ${{ env.REGISTRY }}
		  username: ${{ github.actor }}
		  password: ${{ secrets.GITHUB_TOKEN  }}
	
	  - name: Set K8s context
		uses: azure/k8s-set-context@v4
		with:
		  method: service-account
		  k8s-url: ${{ secrets.KUBERNETES_URL }}
		  k8s-secret: ${{ secrets.KUBERNETES_SECRET }}
```
 <!-- element style="font-size: 0.8em;height:100%;width:100%;margin-top:150px;" -->
</grid>
<grid drag="50" drop="right" >
```yml [2,7,11,16,18,21]
  - name: Set kubectl
	uses: azure/setup-kubectl@v4
	id: install
	with:
	  version: "v1.29.9"
  - name: Set imagePullSecret
	uses: azure/k8s-create-secret@v4
	id: create-secret
	with:
	  namespace: ${{ env.K8S_NAMESPACE }}
	  secret-name: regcred
	  container-registry-url: ${{ env.REGISTRY }}
	  container-registry-username: ${{ github.actor }}
	  container-registry-password: ${{ secrets.GHCR_PULL_TOKEN }}
  - name: Set Label
	run: sed -i'' -e 's/IMAGE_LABEL/${{ github.sha }}/g' k8s.yml
  - name: Deploy application
	uses: azure/k8s-deploy@v5
	with:
	  action: deploy
	  manifests: k8s.yml
	  namespace: ${{ env.K8S_NAMESPACE }}
	  images: ${{ env.REGISTRY }}/${{ github.repository }}:${{ github.sha }}
```
 <!-- element style="font-size: 0.8em;height:100%;width:120%;margin-top:150px;" -->
</grid>

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# Action waiting
:::
![[byoc-waiting-for-self-host.png]]<!-- element style="border-radius: 10px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# Action details
:::
![[byoc-action-run-1.png]]<!-- element style="border-radius: 10px;" -->
---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# Packages
:::
![[byoc-package.png]]<!-- element style="border-radius: 10px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# Package Details
:::
![[byoc-package-details.png]]<!-- element style="border-radius: 10px;" -->

---
<!-- .slide: data-auto-animate -->
::: watermark
![[byoc-devops.png|100]]
:::
::: title
# Website
:::
![[byoc-website.png|750]]<!-- element style="border-radius: 10px;" -->

---
<!-- .slide: data-auto-animate -->
<split even>
![[byoc-dev.png|100]]
![[byoc-devops.png|100]]
![[byoc-ops.png|100]]
</split>

---
<!-- .slide: data-auto-animate -->
#