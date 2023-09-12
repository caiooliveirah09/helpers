# 1 - Oh My Bash

```
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

or

```
bash -c "$(wget https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh -O -)"
```

# 2 - Git

```
sudo apt-get install git-all
```

* rename de branch for main

```
git config --global init.defaultBranch main
```

## add SSH key
  
* [documentation git](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

# Npm, Nvm and Node.js

* install [nvm](https://github.com/nvm-sh/nvm)

* install NodeJs

``` nvm install VERSION ```

* instal Npm for install packagers Example: npm install Express

```
sudo apt install npm
```

# Docker
INSTALAÇÃO DESATUALIZAD MELHOR USAR A [DOCUMENTAÇÃO](https://docs.docker.com/engine/install/ubuntu/)
* Instalando as dependências iniciais

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

##  Adicionando a chave pública do repositório Docker em nossa máquina

Este passo é necessário pois precisamos obter uma chave pública dos servidores da empresa Docker Inc para garantir que qualquer pacote obtido através da Internet esteja assinado por esta chave, evitando assim possíveis ataques de segurança.

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Se tudo der certo, você não deve receber nenhum retorno visual.

## Adicionando o repositório remoto na lista do apt

Para finalmente adicionar o repositório oficial do Docker no apt, execute o seguinte comando:

```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

*Perceba que adicionamos o repositório stable (em $(lsb_release -cs) stable), isso significa que teremos somente o repositório com as versões estáveis do Docker.*

## Instalando o Docker no Linux

* Vamos instalar a última versão estável do Docker Engine - Community, que é uma versão mantida pela própria comunidade, já que o Docker é open source.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Adicionando seu usuário ao grupo de usuários Docker

Para evitar o uso de sudo em todos os comandos Docker que formos executar, vamos dar as devidas permissões ao nosso usuário.

* Primeiro crie um grupo chamado docker:

```
sudo groupadd docker
```

Caso ocorra uma mensagem: groupadd: grupo 'docker' já existe, é só prosseguir

* Então, use o comando abaixo para adicionar seu usuário a este novo grupo:

```
sudo usermod -aG docker $USER
```

* Para ativar as alterações realizadas nos grupos, você pode realizar logout e login de sua sessão ou executar o seguinte comando no terminal:

```
newgrp docker
```

##  Inicie o Daemon do Docker

O Daemon é um serviço que fica no background, ou seja, é um serviço que sempre está em execução e aguarda por comandos feitos por meio do CLI. Entretanto, para que este serviço fique sempre disponível, precisamos ativá-lo, até mesmo após reiniciarmos nosso computador.

* Para consultar o status atual do daemon do Docker, execute o seguinte comando:

```
sudo systemctl status docker
```

* Caso o parâmetro Active esteja como stop/waiting ou no nosso caso, como inactive, rode o comando start para iniciá-lo:

```
sudo systemctl start docker
```

Ao consultar o status novamente, o processo deverá estar como start/running/active.

* Agora, vamos habilitar o daemon do Docker para iniciar durante o boot:

```
sudo systemctl enable docker
```

## Valide a instalação

Para validar se tudo ocorreu como deveria na instalação, vamos executar o tão esperado hello world do Docker:

```
docker run hello-world
```

## Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Por padrão, binários baixados da Internet não possuem permissão de execução. Logo, basta usar o programa chmod para aplicar a permissão de execução (+x) ao binário que acabamos de baixar. Execute o seguinte comando no seu terminal:

```
sudo chmod +x /usr/local/bin/docker-compose
```

# MySql

[link download](https://dev.mysql.com/downloads/workbench/)

## MySql Server

```
sudo apt install mysql-server
```
