# Relatorio de evidencias - Trabalho Pratico Integrador 01-06

Nome: ___Gustavo Couto______   Data: ___24/11/2026___
URL do repositorio Git: https://github.com/GustavoCou/trabalho-avaliacao-devops


## Estrutura
- app.py + requirements*.txt + tests/: API FastAPI e testes ja fornecidos.
- Dockerfile + .dockerignore: completar no Exercicio 01.
- compose.yaml: completar no Exercicio 02.
- incidente.yaml: overlay defeituoso para o Exercicio 03 (nao corrigir antes desse passo).
- Jenkinsfile: completar no Exercicio 05.
- RELATORIO.md: evidencias e registo curto a entregar.


## E01 - Ambiente (1 valor)
Comandos e versoes observadas:

| Ferramenta | Versão observada |
|---|---|
| Docker | 29.9.3 |
| Docker Compose | v5.7.1 |
| Git | 2.56.1.windows.1 |

**Evidências de execução:**

```console
PS> docker --version
Docker version 29.9.3, build 5457199

PS> docker compose version
Docker Compose version v5.7.1

PS> git --version
git version 2.56.1.windows.1

PS> docker info
Client:
 Version: 29.9.3
 Context: desktop-linux

Server:
 Server Version: 29.9.3
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
```

O daemon Docker encontra-se operacional, tendo respondido com sucesso ao comando `docker info` (saída resumida).

## E02 - Dockerfile e container (3 valores)
Tag da imagem; docker ps; HTTP /health; utilizador efetivo do container:


## E02 — Dockerfile e execução de um container

**Construção da imagem:**

```console
PS> docker build -t natixis-support:1.0 .
[+] Building 1.2s (12/12) FINISHED
=> naming to docker.io/library/natixis-support:1.0
```

**Execução do container:**

```console
PS> docker run -d --name tp-api -p 127.0.0.1:18080:8000 natixis-support:1.0

PS> docker ps
CONTAINER ID   IMAGE                 STATUS   PORTS                       NAMES
bc29c2532873   natixis-support:1.0   Up       127.0.0.1:18080->8000/tcp   tp-api
```

**Validação da API:**

```console
PS> curl.exe http://127.0.0.1:18080/health
{"status":"ok","service":"support-api","version":"1.0"}
```

**Validação do utilizador:**

```console
PS> docker exec tp-api id
uid=999(appuser) gid=999(appgroup) groups=999(appgroup)
```

| Parâmetro | Resultado |
|---|---|
| Tag da imagem | `natixis-support:1.0` |
| Porta do host | `18080` |
| Porta do container | `8000` |
| Utilizador | `appuser` (UID 999) |
| Estado da API | `ok` |

**Conclusão:** A imagem foi construída com sucesso e o container executa a aplicação com um utilizador não privilegiado. O endpoint `/health` respondeu corretamente após a inicialização da aplicação.


## E03 - Compose, DNS, healthcheck e volume (4 valores)
Resultado de docker compose config; health; teste checker -> api; contador antes/depois da recriacao:

## E04 - Incidente Docker (3 valores)
Sintoma, comandos de investigacao, causa-raiz, alteracao realizada, prova da recuperacao e contador preservado:

## E05 - Git (3 valores)
Branch, hashes de commits, merge e tag v1.0.0:

## E06 - Jenkins SUCCESS (4 valores)
URL/numero do build, etapas e identificador da imagem construida:

## E07 - Jenkins FAILURE e recuperacao (2 valores)
Build FAILURE, etapa que falhou e excerto relevante do log; build SUCCESS apos correcao:

## Verificacao final
[ ] Dockerfile [ ] compose.yaml [ ] app.py [ ] tests/ [ ] Jenkinsfile
[ ] Historico Git [ ] Tag v1.0.0 [ ] Evidencias E01-E07
