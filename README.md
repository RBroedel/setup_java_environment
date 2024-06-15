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
```

Para configurar a identificação do usuário, execute os seguintes comandos:

```bash
git config --global user.name "<nome>"
git config --global user.email <email>
```
Para ver as configurações, execute:

```bash
git config --list
```

## SSH
Para gerar uma chave SSH, execute:

```bash
ssh-keygen
```
Aperte enter até concluir a geração. Para pegar o valor da chave gerada, execute:

```bash
cat ~/.ssh/id_rsa.pub
```
Backend
JDK 11
Para instalar o JDK 11, abra o terminal e execute:

bash
Copiar código
sudo apt install openjdk-11-jdk
Adicionando JAVA_HOME ao PATH
Para adicionar a variável JAVA_HOME ao PATH, edite o arquivo de configuração de perfil da máquina:

bash
Copiar código
sudo gedit /etc/profile
Adicione as seguintes linhas ao final do arquivo e salve:

bash
Copiar código
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
Reinicie a máquina para aplicar as alterações.

Eclipse
Faça o download do Eclipse pelo link oficial. Extraia o arquivo baixado e navegue até a pasta eclipse-installer. Abra a pasta no terminal e execute:

bash
Copiar código
./eclipse-inst
Escolha a opção "Eclipse IDE for Enterprise Java and Web Developers" e siga com a instalação.

Configuração Eclipse
Encode
Abra o Eclipse e selecione o menu Window -> Preferences. Vá para General -> Workspace e selecione UTF-8 em "Text file encoding".

Formatter
No menu Window -> Preferences, vá para Java -> Code Style -> Formatter, clique em Import... e selecione o arquivo eclipse-DEFAULT_IDENTATION.xml.

Correções ao Salvar
No menu Window -> Preferences, vá para Java -> Editor -> Save Actions e marque todas as opções.

JBoss Tools
No Eclipse, vá para Help -> Eclipse Marketplace, busque por jboss e siga com a instalação do JBoss Tools.

Importar Projetos
Para importar projetos no Eclipse, vá para File -> Import…, selecione Maven -> Existing Maven Projects e clique em Next >. Navegue até o diretório que contém o arquivo pom.xml do projeto e clique em Finish.

WildFly
Faça o download da versão 15.0.1 FINAL do WildFly pelo link oficial. Extraia o arquivo para a pasta desejada.

Driver PostgreSQL
Extraia o conteúdo do arquivo postgresql.zip para o diretório /modules/system/layers/base/org dentro da pasta do WildFly.

Driver MySQL
Extraia o conteúdo do arquivo mysql.zip para o diretório /modules/system/layers/base/com dentro da pasta do WildFly.

Adicionando WildFly ao Eclipse
No Eclipse, vá para Window -> Preferences, selecione Server -> Runtime Environments e clique em Add…. Selecione WildFly 15 Runtime, clique em Next >, e no campo Home Directory, clique em Browse… e selecione o diretório do WildFly. Em Runtime JRE -> Execution Environment, selecione JavaSE-11, clique em Finish e em Apply and Close.

Para exibir a aba Servers, vá para Window -> Show View -> Others…, selecione Servers e clique em Open.

Clique em No servers are available. Click this link to create a new server…, selecione WildFly 15 e siga com a configuração.

Configurar Standalone
O arquivo standalone.xml do servidor WildFly pode ser acessado no Eclipse. Adicione a tag <system-properties></system-properties> entre as tags <extensions> e <management> e adicione as propriedades necessárias.

Adicionando Projeto ao WildFly
Para adicionar um projeto ao WildFly, arraste o projeto EAR para dentro do servidor no Eclipse. Para iniciar, clique em Run ou Debug.

Lombok
Faça o download do Lombok pelo site oficial. Permita a execução do arquivo:

bash
Copiar código
chmod 777 lombok.jar
Execute o arquivo lombok.jar, selecione o diretório do Eclipse e clique em Install/Update.

Docker Engine
Para instalar o Docker no Ubuntu, execute:

bash
Copiar código
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
Adicione a chave GPG oficial do Docker:

bash
Copiar código
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
Adicione o repositório estável do Docker:

bash
Copiar código
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Instale o Docker Engine:

bash
Copiar código
sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io
Para expor o Docker ao usuário não sudo, execute:

bash
Copiar código
sudo groupadd docker
sudo usermod -aG docker $USER
Reinicie a máquina.

Docker Compose
Para instalar o Docker Compose, siga as instruções no site oficial.

Criar Container via CLI
Para criar um container Docker, execute:

bash
Copiar código
docker run [parâmetros]
Exemplo para criação de container PostgreSQL:

bash
Copiar código
docker run --name postgresserver -e POSTGRES_PASSWORD=itix.123 -p 5432:5432 -d -v postgres-volume:/var/lib/postgresql/data postgres:latest
Criar Container via Docker-Compose
Crie um arquivo .yml (ex.: postgres.yml) com o seguinte conteúdo:

yaml
Copiar código
version: '3.1'

services:
  postgresserver:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: itix.123
    ports:
      - 5432:5432
Execute no terminal:

bash
Copiar código
docker-compose -f <nome_arquivo>.yml up
DBeaver
Para instalar o DBeaver, procure na Ubuntu Software. Após abrir o DBeaver, para conectar a um servidor, clique em New Database Connection, selecione o SGBD desejado e clique em Next >. Preencha os dados de conexão e clique em Test Connection….

Frontend
VSCode
Para instalar o VSCode, procure na Ubuntu Software.

NPM
Para instalar o npm, execute:

bash
Copiar código
sudo apt install npm
NVM
Para instalar o NVM, execute:

bash
Copiar código
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
Para verificar a instalação:

bash
Copiar código
command -v nvm
Angular CLI
Para instalar o Angular CLI, execute:

bash
Copiar código
npm install -g @angular/cli
Download Dependências
Para baixar as dependências do projeto Angular, navegue até a pasta do projeto e execute:

bash
Copiar código
npm install
Rodar Projeto
Para rodar o projeto Angular, execute:

bash
Copiar código
ng serve
Abra o navegador e navegue até localhost:4200.

css
Copiar código

Este guia foi elaborado para fornecer um passo a passo claro e conciso para configurar o ambiente de desenvolvimento ITIX em um sistema Ubuntu, garantindo que todas as ferramentas necessárias estejam instaladas e configuradas corretamente.
