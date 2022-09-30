## readline-sync 

1. basta executarmos o comando npm i readline-sync dentro da pasta hello-world.
   
2. Uma vez instalado o pacote, podemos utilizá-lo em nosso script. Para isso, precisamos, primeiro, importá-lo desse jeito:

```
const readline = require('readline-sync');

// console.log('Hello, world!');
```

3. Agora, com o pacote em mãos, podemos utilizar as funções question e questionInt disponibilizadas por ele para perguntar à pessoa usuária seu nome e idade:
   
```
// const readline = require('readline-sync');

const name = readline.question('Qual seu nome? ');
const age = readline.questionInt('Qual sua idade? ');

// console.log('Hello, world!');
```

4. Pronto, agora o último passo é utilizarmos essas novas variáveis para compor nossa mensagem de olá. Bora fazer isso então:

```
// const readline = require('readline-sync');

// const name = readline.question('What is your name? ');
// const age = readline.questionInt('How old are you? ');

console.log(`Hello, ${name}! You are ${age} years old!`);
```

5. Execute novamente o script com npm start para vê-lo em ação!