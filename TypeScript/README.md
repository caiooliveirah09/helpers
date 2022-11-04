# TypeScript

```
npm install -g typescript
```

## tsconfig.json

```
npm i -D typescript
```

```
tsc --init
```

**ou**

```
npx tsc --init
```

* module: especifica o sistema de módulo a ser utilizado no código JavaScript que será gerado pelo compilador como sendo o CommonJS;
* target: define a versão do JavaScript do código compilado como ES6;
* rootDir: define a localização raiz dos arquivos do projeto;
* outDir: define a pasta onde ficará nosso código compilado;
* esModuleInterop: habilitamos essa opção para ser possível * compilar módulos ES6 para módulos CommonJS;
* strict: habilitamos essa opção para ativar a verificação estrita de tipo;
* include: essa chave vai depois do objeto CompilerOptions e com ela conseguimos incluir na compilação os arquivos ou diretórios mencionados; e
* exclude: essa chave também vai depois do objeto CompilerOptions e com ela conseguimos excluir da compilação os arquivos mencionados.


## exemplo node 16

```
npm i -D @tsconfig/node16
```

### tsconfig.json 

```
{
  "extends": "@tsconfig/node16/tsconfig.json",
  "compilerOptions": {
    "target": "es2016",                                 
    "module": "commonjs",
    "rootDir": "./",
    "outDir": "./dist",
    "preserveConstEnums": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  },
  "include":["src/**/*"], /* aqui estamos incluindo todos os arquivos dentro da pasta src */
  "exclude": ["node_modules", "**/*.spec.ts"] /* aqui estamos excluindo a pasta node_modules e os arquivos de teste */
}
```

## @types/node

```
npm install -D @types/node
```

## class 

```
class Person {
    name: string;
    birthDate: Date;
    age?: number;

    constructor(name: string, birthDate: Date, age?: number) {
        this.name  = name;
        this.birthDate  = birthDate;
        this.age  = age;
    }

    speak(): void {
        console.log(`${this.name} está falando.`);
    }

    eat(): void {
        console.log(`${this.name} está comendo.`)
    }

    walk(): void {
        console.log(`${this.name} está andando.`)
    }
}
```

## interfaces

```
interface Employee {
    firstName: string;
    lastName: string;
    fullName(): string;
}
```

```
let employee: Employee = {
    firstName : "John",
    lastName: "Doe",
    fullName(): string {
        return this.firstName + " " + this.lastName; // usamos o "this" para acessar as propriedades da interface
    }
}

employee.firstName = 10;  // Error: Type "number" is not assignable to type "string"
```

```
interface Teacher extends Employee {
    subject: string;
    sayHello(): string;
}
```

```
let teacher: Teacher = {
    firstName: "John",
    lastName: "Doe",
    subject: "Matemática",
    fullName(): string {
        return this.firstName + " " + this.lastName;
    },
    sayHello(): string {
        return `Olá, eu sou ${this.fullName()} e leciono ${this.subject}`;
    }
}
```

## type assertion

```
type Address = {
  street: string,
  number: number | null,
}

type User = {
  name: string,
  email: string,
  password: string,
}

// função que converte de string para json
function stringToJson(str: string): unknown {
  const result = JSON.parse(str);
  return result;
}

// utilizando o "as" para converter de unknown para User
const user = stringToJson('{"name":"André Soares","email":"andre@trybe.com","password":"senha_secreta"}') as User

// Outra forma de usar o Assertion. A sintaxe é diferente mas tem o mesmo objetivo
const address = <Address> stringToJson('{"street":"Rua Tamarindo","number":1}')

user.name;
address.street;
```

## generics 

```
/ [...]
function stringToJson<T>(str: string): T {
  const result = JSON.parse(str);
  return result;
}

const user = stringToJson<User>('{"name":"André Soares","email":"andre@trybe.com","password":"senha_secreta"}');

const address = stringToJson<Address>('{"street":"Rua Tamarindo","number":1}')

user.name;
address.street;
```

```
// [...]
function stringToJson<T, U>(str: string, id: U ): T & { id: U } {
  // const result = JSON.parse(str);
  result.id = id;
  // return result;
}

const user = stringToJson<User, number>('{"name":"André Soares","email":"andre@trybe.com","password":"senha_secreta"}', Date.now());

const address = stringToJson<Address, string>('{"street":"Rua Tamarindo","number":1}', '#01')

user.id;
address.id;
```

```
function identity<T, U> (value: T, message: U) : T {
    console.log(message);
    return value
}

const returnNumber = identity<number, string>(100, "Olá");
const returnString = identity<string, string>("100", "Mundo");
const returnBoolean = identity<boolean, string>(true, "Olá, Mundo!");
```

```
function getArray<T>(items : T[]) : T[] {
  return new Array<T>().concat(items); // construindo um Array que só pode conter elementos do tipo T
}

const numberArray = getArray<number>([5, 10, 15, 20]);
numberArray.push(25);
numberArray.push("This is not a number"); // Isto vai gerar um erro de compilação

const stringArray = getArray<string>(["Cats", "Dogs", "Birds"]);
stringArray.push("Rabbits");
stringArray.push(30); // Isto vai gerar um erro de compilação
```