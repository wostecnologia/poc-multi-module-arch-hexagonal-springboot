<div align="center">

![](https://img.shields.io/badge/Status-Em%20Desenvolvimento-orange)
</div>

<div align="center">

# POC Multi Modulos- Ports & Adapters Architecture ou Arquitetura Hexagonal
![](https://img.shields.io/badge/Autor-Wesley%20Oliveira%20Santos-brightgreen)
![](https://img.shields.io/badge/Language-java-brightgreen)
![](https://img.shields.io/badge/Framework-springboot-brightgreen)
![](https://img.shields.io/badge/Arquitetura-Hexagonal-brightgreen)
</div> 

<div align="center">

## Arquitetura

</div>

<div align="center">

## Sonar
[![Quality gate](https://sonarcloud.io/api/project_badges/quality_gate?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)

[![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=ncloc)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=coverage)](https://sonarcloud.io/summary/new_code?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Duplicated Lines (%)](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=duplicated_lines_density)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)

[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=security_rating)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)

[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=vulnerabilities)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=bugs)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=code_smells)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)
[![Technical Debt](https://sonarcloud.io/api/project_badges/measure?project=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot&metric=sqale_index)](https://sonarcloud.io/dashboard?id=wesleyosantos91_poc-multi-module-arch-hexagonal-springboot)

</div>

## Fundamentos teóricos

> Ports & Adapters Architecture ou Arquitetura Hexagonal: A arquitetura hexagonal, ou arquitetura de portas e adaptadores, é um padrão arquitetural usado no design de software. O objetivo é criar componentes de aplicativos fracamente acoplados que possam ser facilmente conectados ao ambiente de software por meio de portas e adaptadores.

##  Pré -requisitos

- [ `Java 11+` ](https://www.oracle.com/java/technologies/downloads/#java11)
- [ `Docker` ](https://www.docker.com/)
- [ `Docker-Compose` ](https://docs.docker.com/compose/install/)

## Stack
- **Sonar** para analise de qualidade e cobertura de testes
- **Elasticsearch** Busca e análise de dados
- **Logstash** Pipeline de dados
- **Kibana** Visualização de dados
- **Filebeat**  Log shipper

## Portas
| Aplicação          | Porta      |
|--------------------|------------|
| Ms-Launcher        | 8080       |
| Sonarqube          | 9000       |
| Postgres Sonarqube | 5432       |
| Elasticsearch      | 9200, 9300 |
| Logstash           | 5044       |
| Kibana             | 5601       |


## Links

- Sonar Cloud
  - http://localhost:9000
- Kibana (Criar index pattern - filebeat-*)
  - http://localhost:5601

## Setup

- ### Variáveis de ambiente

| Variável de Ambiente  | Descrição                                                                       |
|-----------------------|---------------------------------------------------------------------------------|
| `MYSQL_HOST`          | Especifique o host do banco de dados `MySQL` a ser usado (padrão `localhost` )  |
| `MYSQL_PORT`          | Especifique a porta do banco de dados `MySQL` a ser usada (padrão `3306` )      |

### Build da aplicação
- Entre no diretorio dos scripts `cd scripts`
- Execute o seguinte comando: 
  ```
  /bin/bash build.sh
  ```

### Executando a aplicação com maven
- Execute o seguinte comando:
  ```
  ./mvnw clean spring-boot:run --projects ms-launcher
  ```
  > **Nota:** Se você quiser mudar para "non-json-logs" (talvez durante o desenvolvimento seja útil), execute
  > ```
  > ./mvnw clean spring-boot:run --projects ms-launcher -Dspring-boot.run.jvmArguments="-Dspring.profiles.active=non-json-logs"
  > ```

### Executar docker-compose para subur aplicação com container docker
- Execute o seguinte comando para subir os containers: 
  ```
  docker-compose up
  ```
- Execute o seguinte comando para verificar os status do containers docker:
  ```
  docker-compose ps
  ```
  
### Sonarqube

- Realize o Login com user: admin password: admin para uma nova senha
- Clique na opção Manually
- Crie os Project display name/project key: `poc-multi-module-arch-hexagonal-springboot`
- Clique na opção Locally
- Preencha com `wos` e clique em Generate
- Subtitua o project key e token do arquivo `scripts/sonar.sh` pelos criado agora
- Entre no diretorio dos scripts `cd scripts`
- Execute o seguinte comando: 
  ```
  /bin/bash sonar.sh
  ```

### Kibana

- Na página principal, clique no ícone do menu *"hambúrguer"* e, em seguida, clique em `Discover`
- Clique no botão `Create index pattern`
- No campo `Name`, defina `filebeat-*`
- No campo `Timestamp field` selecione `@timestamp`
- Clique no botão `Create index pattern`
- Clique no ícone do menu "hambúrguer"Discover novamente e depois clique para iniciar as pesquisas

## Deletar todos containers Docker

- Entre no diretorio dos scripts `cd scripts`
- Execute o seguinte comando:
  ```
  /bin/bash remove-docker-images.sh
  ```

## TODO List

- [x] Qualidade de código
  - [x] Sonarqube
- [ ] Observabilidade
  - [x] Logs ELK (Elasticsearch, Logstash, Kibana) e Filebeat
  - [ ] Prometheus e Grafana
  - [ ] 