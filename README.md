# Configuração do Ambiente ITIX

Este guia fornece instruções detalhadas para configurar o ambiente de desenvolvimento ITIX em um sistema operacional Linux - Ubuntu. Alguns passos podem diferir em outras distribuições e devem ser consultados nos sites oficiais.

## Sumário

- [GIT](#git)
- [SSH](#ssh)
- [Backend](#backend)
  - [JDK 11](#jdk-11)
  - [Adicionando JAVA_HOME ao PATH](#adicionando-java_home-ao-path)
  - [Eclipse](#eclipse)
    - [Configuração Eclipse](#configuração-eclipse)
      - [Encode](#encode)
      - [Formatter](#formatter)
      - [Correções ao Salvar](#correções-ao-salvar)
  - [JBoss Tools](#jboss-tools)
  - [Importar Projetos](#importar-projetos)
  - [WildFly](#wildfly)
    - [Driver PostgreSQL](#driver-postgresql)
    - [Driver MySQL](#driver-mysql)
    - [Adicionando WildFly ao Eclipse](#adicionando-wildfly-ao-eclipse)
    - [Configurar Standalone](#configurar-standalone)
    - [Adicionando Projeto ao WildFly](#adicionando-projeto-ao-wildfly)
  - [Lombok](#lombok)
- [Docker Engine](#docker-engine)
  - [Docker Compose](#docker-compose)
  - [Criar Container via CLI](#criar-container-via-cli)
  - [Criar Container via Docker-Compose](#criar-container-via-docker-compose)
- [DBeaver](#dbeaver)
- [Frontend](#frontend)
  - [VSCode](#vscode)
  - [NPM](#npm)
  - [NVM](#nvm)
  - [Angular CLI](#angular-cli)
  - [Download Dependências](#download-dependências)
  - [Rodar Projeto](#rodar-projeto)

## GIT

Para instalar o Git, execute o seguinte comando:
```bash
sudo apt install git
