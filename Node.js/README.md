# Node.js

## Hello, world!

1. Vamos começar criando uma nova pasta, chamada hello-world, na qual colaremos nosso código.

2. Uma vez dentro dessa pasta, execute o comando npm init ou npm init -y.

3. Abra a pasta hello-world no VSCode e vamos começar a criar nosso script.

4. Dentro da pasta hello-world, crie um arquivo chamado index.js. Por padrão, esse é o arquivo principal de qualquer aplicação Node.js e é comum darmos esse nome ao arquivo que deve ser executado para iniciar nosso programa.

5. Dentro do index.js, adicione o seguinte código:

```
console.log('Hello, world!');
```

6. Pronto, nosso script de “Hello, world!” está criado! Mas nosso pacote ainda não está pronto. Vamos criar um script start para estarmos aderentes às convenções do Node.js.

7. Como você viu anteriormente, para criar um script precisamos alterar o package.json da nossa aplicação. Sendo assim, abra o package.json da pasta hello-world e altere a linha destacada para criar o script start dessa forma:

```
// {
//   "name": "hello-world",
//   "version": "1.0.0",
//   "description": "",
//   "main": "index.js",
//   "scripts": {
//     "test": "echo \"Error: no test specified\" && exit 1",
       "start": "node index.js"
//   },
//   "author": "Seu nome",
//   "license": "ISC"
// }
```

Agora que temos tudo criado e configurado, chegou a hora de executar nosso Hello, world! Para isso, navegue até a pasta hello-world no terminal e execute npm start.

Pronto! Temos nosso primeiro “Hello, world!” sendo executado com Node.js!
  
## Promise

### Função sem promise 

```
function dividirNumeros(num1, num2) {
  if (num2 == 0) throw new Error("Não pode ser feito uma divisão por zero");

  return num1 / num2;
}

try {
  const resultado = dividirNumeros(2, 1);
  console.log(`resultado: ${resultado}`);
} catch (e) {
  console.log(e.message);
}

```

### Função com promise

```
function dividirNumeros(num1, num2) {
  const promise = new Promise((resolve, reject) => {
    if (num2 == 0) 
      reject(new Error("Não pode ser feito uma divisão por zero"));

    const resultado = num1 / num2;
    resolve(resultado)
  });

  return promise;
}

dividirNumeros(2, 1)
  .then(result => console.log(`sucesso: ${result}`))
  .catch(err => console.log(`erro: ${err.message}`));

```

### Async/await

```
const doSomething = async () => {
  console.log(await dividirNumeros(2,2));
};
```