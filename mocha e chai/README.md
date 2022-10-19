# mocha e chai

```
npm install -D mocha@10.0 chai@4.3
```

```
const chai = require('chai');
const { expect } = chai;

const calculaSituacao = require('../examples/calculaSituacao');

describe('Quando a média for menor que 7', function () {
  it('retorna "reprovação"', function () {
    const resposta = calculaSituacao(4);

    expect(resposta).equals('reprovação');
  });
});
```
# package.json
```
    "scripts": {
    "test": "mocha tests/**/*.test.js --exit"
  },
```

## [chai](https://www.chaijs.com/api/bdd/)

## chai-htpp

```
npm install -D chai-http@4.3
```

```
// tests/integration/chocolates.test.js

const chai = require('chai');
const chaiHttp = require('chai-http');

const { expect } = chai;

chai.use(chaiHttp);

describe('Testando a API Cacao Trybe', function () {
  describe('Usando o método GET em /chocolates', function () {
    it('Retorna a lista completa de chocolates!', async function () {
      const output = [
        { id: 1, name: 'Mint Intense', brandId: 1 },
        { id: 2, name: 'White Coconut', brandId: 1 },
        { id: 3, name: 'Mon Chéri', brandId: 2 },
        { id: 4, name: 'Mounds', brandId: 3 },
      ];

      const response = await chai
        .request(app)
        .get('/chocolates');
      expect(response.status).to.be.equal(200);
      expect(response.body.chocolates).to.deep.equal(output);
    });
  });
});
```

### post = chai.request(app).post('/*).send(mock);
