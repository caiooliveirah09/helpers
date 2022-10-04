1. 
```
npm i express@4.17
```

2.
```
npm i eslint@6.8 eslint-config-trybe-backend@1.0 -D
```

3.
```
touch .eslintignore .eslintrc.json
```

4.
```
// .eslintignore

node_modules
```

5.
```
// .eslintrc.json
{
  "env": {
    "es2020": true
  },
  "extends": "trybe-backend",
  "rules": {
    "sonarjs/no-duplicate-string": ["error", 5]
  }
}
```

6.
```
git init && touch .gitignore
```

7.
```
// .gitignore

node_modules
```

8. dentro da pasta src
```
touch app.js server.js
```

9. dentro do app.js
```
// src/app.js
const express = require('express');

const app = express();

module.exports = app;
```

10. dentro do server.js
```
// src/server.js
const app = require('./app');

app.listen(3001, () => console.log('server running on port 3001'));
```

11. instalando o nodemon
```
npm i nodemon -D
``` 

12.
```
app.get('/', (req, res) => res.status(200).json({ message: 'Olá Mundo!' }));
```

* 200: Que quer dizer ‘ok’;
* 500: Que quer dizer erro no servidor;
* 404: Este muitas pessoas já viram, ele quer dizer que a página não foi * encontrada;


* 2° parâmetro (req, res) => {}: Este espera uma função de callback. Esta função pode receber de 2 a 4 parâmetros, sendo eles:
* req: Essa é a Request (ou requisição), é por meio dela que recebemos os dados (envio por query, params e body);
* res: Essa é a Response (ou resposta), é por meio dela que respondemos o que nos é solicitado;
* next: 
* err: 


* GET -  obter/recuperar
* POST - inserir
* PUT -  atualização completa
* PATCH - atualização parcial 
* DELETE - EXCLUIR
13.
```

```

14.
```
```

15.
```
```

16.
```
```

17.
```
```

18.
```
```

19.
```
```
