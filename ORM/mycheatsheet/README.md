# ORM 
## Sequelize

1. ➡️ Para começar a usar o **Sequelize**, é preciso iniciar uma aplicação **Node**.js e instalar essa biblioteca **ORM** utilizando os seguintes comandos:

```
mkdir app-with-sequelize && cd app-with-sequelize

npm init -y

npm install sequelize
```

2. ➡️ O próximo passo para utilizar o Sequelize é instalar um CLI, que é responsável por gerar e executar as operações. Além de instalar o CLI, também precisamos instalar o mysql2, uma dependência necessária para usarmos o MySQL com o Sequelize. Na pasta raiz da aplicação, rode os comandos:

```
npm install sequelize-cli

npm install mysql2

mkdir src
```

3. ➡️ Depois que instalamos o CLI, precisamos iniciar um projeto com o Sequelize. Para isso, vamos executar o seguinte comando dentro da pasta src:

```
cd src

npx sequelize-cli init
```

Esse comando vai criar as seguintes pastas:

* **config**: contém um arquivo de configuração, com orientações para o CLI se * **conectar** com o nosso banco de dados;

* **models**: contém todos os modelos da nossa aplicação;

* **migrations**: contém todos os arquivos de migração da nossa aplicação;

* **seeders**: contém todos os arquivos de “seeds” (sementes que são usadas para popular o banco).

➡️ Agora precisamos configurar o arquivo config.json gerado pelo init do CLI. Ao alterar esse arquivo, estamos configurando o acesso da aplicação ao nosso banco de dados.

➡️ Note que no nosso arquivo config.json, dentro da pasta config, as informações sensíveis, como credenciais de acesso ao banco de dados, estão todas expostas no nosso código. Uma boa prática é usar variáveis de ambiente para controlar o que estiver relacionado à configuração geral da aplicação. Então, bora fazer isso do jeito certo!

4. ➡️ Vamos fazer a instalação do pacote dotenv:

```
npm install dotenv
```

➡️ Mudaremos o nome do nosso arquivo **config**.json para **config**.**js**

5. ➡️ Retiraremos todo o conteúdo de **config**.js e substituíremos pelo código abaixo:

> src/config/config.js


```
// src/config/config.js

require('dotenv').config();

const config = {
  username: process.env.MYSQL_USER,
  password: process.env.MYSQL_PASSWORD,
  database: process.env.MYSQL_DATABASE,
  host: process.env.MYSQL_HOST,
  dialect: 'mysql',
};

module.exports = {
  development: config,
  test: config,
  production: config,
};
```

> Note que vamos assumir que os três ambientes vão utilizar configurações semelhantes. Em aplicações mais complexas, no entanto, é possível que você utilize bancos de dados e configurações diferentes para cada ambiente. Nesses casos, elas devem ser configuradas por meio de variáveis de ambiente.

* **Usuário** de acesso ao banco de dados;

* **Senha** de acesso ao banco de dados;

* **Nome** do banco de dados no qual queremos conectar;

* **Host** que estamos conectando - por ser local, utilizamos o 127.0.0.1;

* **Dialect**, que se refere a qual banco estamos utilizando. Nesse caso, “mysql”.

6. ➡️ Crie o arquivo .**env** na raiz do projeto e preencha as variáveis com as suas credenciais para acessar o **MySQL**:

```
MYSQL_USER=root
MYSQL_PASSWORD=senha_mysql
MYSQL_DATABASE=orm_example
MYSQL_HOST=localhost
```

7. ➡️ Modifique a linha 8 do arquivo src/models/index.js para apontar para o arquivo config.js:

```
const config = require(__dirname + '/../config/config.json')[env]; // configuração antiga
const config = require(__dirname + '/../config/config.js')[env];   // configuração nova
```

➡️ O arquivo **.sequelizerc**

Por padrão, ao rodar um comando Sequelize os arquivos dentro das pastas de **migrations**, **models**, **seeders** e **config** seriam procurados somente na camada em que estivéssemos executando o comando. No nosso caso, como estamos utilizando a pasta **src** para abrigar os arquivos do Sequelize, caso executássemos um comando diretamente na raiz da aplicação, iríamos no deparar com um erro.

Podemos entrar na pasta **src** e executar estes comandos, como fizemos anteriormente, pois assim teremos êxito. Mas caso fosse uma aplicação maior, com mais camadas, aumentaríamos a complexidade de subir e configurar a aplicação.

É neste momento que entra em cena o arquivo .**sequelizerc**. Ele é um arquivo de configuração que podemos utilizar caso seja preciso substituir o caminho padrão das pastas **migrations**, **models**, **seeders** ou **config**. Dessa forma, podemos construir um código com uma arquitetura mais organizada. ⭐

8. ➡️ Para configurar este arquivo, crie um arquivo com o nome .**sequelizerc** na raiz da aplicação com o seguinte conteúdo:

```
const path = require('path');

module.exports = {
  'config': path.resolve('src', 'config', 'config.js'),
  'models-path': path.resolve('src', 'models'),
  'seeders-path': path.resolve('src', 'seeders'),
  'migrations-path': path.resolve('src', 'migrations'),
};
```

* path: é um módulo interno do Node que nos fornece alguns utilitários para trabalharmos com caminhos de arquivos e diretórios;

* **config**: é um caminho para o arquivo de configuração;

* **models**-**path**: é um caminho para o diretório de models;

* **seeders**-**path**: é um caminho para o diretório de seeders;

* **migrations**-**path**: é um caminho para o diretório de migrations.

9. ➡️ Agora que iniciamos uma aplicação do **Sequelize**, podemos criar o banco de dados **orm_example** (que nomeamos no .**env**) através deste comando:

```
npx sequelize db:create
```
No seu terminal, o Sequelize vai avisar que o database foi criado. Você pode verificar isso no próprio MySQL utilizando os comandos abaixo:

```
mysql -u root -p
```
➡️ Digite a sua senha de acesso ao mysql e em seguida rode o comando abaixo:

```
show databases;
```

➡️ Perceba que, a partir desses passos, o banco orm_example foi criado e você não precisou escrever nenhuma linha de SQL para isso. Essa é uma das primeiras vantagens que o Sequelize nos oferece. ⭐

## ERRO 

* Cria um container docker e xD

```
docker run -p 3306:3306 --name mysql-sequelize -e MYSQL_ROOT_PASSWORD=root -d mysql:8.0.23
```

* Tem que mudar o password do mysql no seu .env também xD

## criando uma tabela

```
// src/models/user.model.js

const UserModel = (sequelize, DataTypes) => {
  const User = sequelize.define('User', {
    fullName: DataTypes.STRING,
    email: DataTypes.STRING,
  });

  return User;
};

module.exports = UserModel;
```

## Migrations 

1. ➡️ Agora vamos gerar um novo arquivo, com apenas o “esqueleto” de uma migration, usando o seguinte comando no terminal:

```
npx sequelize migration:generate --name create-user
```

* exemplo do up

```
// src/migrations/[timestamp]-create-user.js

// 'use strict';

// module.exports = {
//   up: async (queryInterface, Sequelize) => {
       await queryInterface.createTable('Users', {
         id: {
           allowNull: false,
           autoIncrement: true,
           primaryKey: true,
           type: Sequelize.INTEGER
         },
         fullName: {
           type: Sequelize.STRING
         },
         email: {
           type: Sequelize.STRING
         },
         createdAt: {
           allowNull: false,
           type: Sequelize.DATE
         },
         updatedAt: {
           allowNull: false,
           type: Sequelize.DATE
         }
       });
//   },

//   down: async (queryInterface, Sequelize) => {
      /**
       * Add reverting commands here.
       *
       * Example:
       * await queryInterface.dropTable('users');
       */
//   }
// };
```

* exemplo do down

```
// src/migrations/[timestamp]-create-user.js

//  'use strict';

//  module.exports = {
//    up: async (queryInterface, Sequelize) => {
//      ...
//    },
//    down: async (queryInterface, Sequelize) => {
        await queryInterface.dropTable('Users');
//    }
//  };
```
* **allowNull**: Define se o campo pode ou não receber um valor null;
* **autoIncrement**: Define se o campo vai ter incremento automático;
* **primaryKey**: Define se o campo é uma chave primária;
* **type**: Define o tipo do campo, por exemplo STRING, INTEGER, DATE, etc.

➡️ Com a migration criada, basta executarmos o seguinte comando pelo CLI:

```
npx sequelize db:migrate
```

➡️ Caso queira reverter uma migration use o seguinte comando:

```
npx sequelize db:migrate:undo
```

## Seeders

```
npx sequelize seed:generate --name users
```

```
// src/seeders/[timestamp]-users.js

'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => queryInterface.bulkInsert('Users',
    [
      {
        fullName: 'Leonardo',
        email: 'leo@test.com',
        // usamos a função CURRENT_TIMESTAMP do SQL para salvar a data e hora atual nos campos `createdAt` e `updatedAt`
        createdAt: Sequelize.literal('CURRENT_TIMESTAMP'),
        updatedAt: Sequelize.literal('CURRENT_TIMESTAMP'),
      },
      {
        fullName: 'JEduardo',
        email: 'edu@test.com',
        createdAt: Sequelize.literal('CURRENT_TIMESTAMP'),
        updatedAt: Sequelize.literal('CURRENT_TIMESTAMP'),
      },
    ], {}),

  down: async (queryInterface) => queryInterface.bulkDelete('Users', null, {}),
};
```
* Para executar a seed
  
```
npx sequelize db:seed:all
```

* Para reverter a seed

```
npx sequelize db:seed:undo:all
```


