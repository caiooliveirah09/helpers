# sinon 

```
npm install sinon@14.0.0 -D
```
## sinon with fs

### readFile

```
const sinon = require('sinon');

const fs = require('fs');

const mockMissions = JSON.stringify([{name: test, id: 0}])


beforeEach
sinon.stub(fs.promises, 'readFile').resolves(mockMissions);

afterEach
sinon.restore();
```

### writeFile 

```
sinon.stub(fs.promises, 'writeFile').resolves();
await chai.request(app).post('/missions).send(mockMission);
expect(fs.promises.writeFile.called).to.be.equal(true);
sinon.restore();
```

### before and after Each

```
beforeEach( function () {
  sinon.stub(fs.promises, 'writeFile').resolves();
});

afterEach(sinon.restore);
```