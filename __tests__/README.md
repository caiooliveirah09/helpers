# __tests__

## renderWithRouter 

```
import React from 'react';
import { Router } from 'react-router-dom';
import { createMemoryHistory } from 'history';
import { render } from '@testing-library/react';

const renderWithRouter = (component, route = '/') => {
  const history = createMemoryHistory(({ initialEntries: [route] }));
  return ({
    ...render(<Router history={ history }>{component}</Router>), history,
  });
};
export default renderWithRouter;
```

## renderWithRouterAndRedux

```
import React from 'react';
import { render } from '@testing-library/react';
import { Router } from 'react-router-dom';
import { createMemoryHistory } from 'history';
import { Provider } from 'react-redux';
import {  legacy_createStore as createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import reducer from '../../redux/reducers';

export const renderWithRouterAndRedux = (component, initialState, route = '/') => {
  const store = createStore(reducer, initialState, applyMiddleware(thunk));
  const history = createMemoryHistory({ initialEntries: [route] });

  return {
    ...render(
      <Provider store={ store }>
        <Router history={ history }>
          {component}
        </Router>
      </Provider>,
    ),
    history,
    store,
  };
};

export default renderWithRouterAndRedux;
```

## renderWithRouterAndContext

```
import React from 'react';
import { Router } from 'react-router-dom';
import { createMemoryHistory } from 'history';
import { render } from '@testing-library/react';
import { RecipesProvider } from '../../context/RecipesContext';

const renderWithRouter = (component, route = '/') => {
  const history = createMemoryHistory({ initialEntries: [route] });
  return ({
    ...render(
      <Router history={ history }>
        <RecipesProvider>
          {component}
        </RecipesProvider>
      </Router>,
    ),
    history,
  });
};
export default renderWithRouter;
```
## beforeEach and afterEach 

```
beforeEach(() => {
    localStorage.setItem('user', JSON.stringify({ email }));
  });

  afterEach(() => {
    localStorage.clear();
  });
```

## clipboard, copy

```
https://stackoverflow.com/questions/62351935/how-to-mock-navigator-clipboard-writetext-in-jest
```
### 1 - 
```
const originalClipboard = { ...global.navigator.clipboard };
  const mockData = {
     "name": "Test Name",
     "otherKey": "otherValue"
  }

  beforeEach(() => {
    const mockClipboard = {
      writeText: jest.fn(),
    };
    global.navigator.clipboard = mockClipboard;

  });

  afterEach(() => {
    jest.resetAllMocks();
    global.navigator.clipboard = originalClipboard;
  });

  test("copies data to the clipboard", () => {
    copyData(); //my method in the source code which uses the clipboard
    expect(navigator.clipboard.writeText).toBeCalledTimes(1);
    expect(navigator.clipboard.writeText).toHaveBeenCalledWith(
      JSON.stringify(mockData)
    );
  });
```

### 2 - 
```
Object.assign(navigator, {
  clipboard: {
    writeText: () => {},
  },
});

describe("Clipboard", () => {
  describe("writeText", () => {
    jest.spyOn(navigator.clipboard, "writeText");
    beforeAll(() => {
      yourImplementationThatWouldInvokeClipboardWriteText();
    });
    it("should call clipboard.writeText", () => {
      expect(navigator.clipboard.writeText).toHaveBeenCalledWith("zxc");
    });
  });
});
```

### 3 - 
```
describe('my-test', () => {

  it("should copy to clipboard", () => {
    const { getByRole } = render(MyComponent);

    Object.assign(window.navigator, {
      clipboard: {
        writeText: jest.fn().mockImplementation(() => Promise.resolve()),
      },
    });

    const button = getByRole("button");
    fireEvent.click(button);

    expect(window.navigator.clipboard.writeText)
      .toHaveBeenCalledWith('the text that needs to be copied');
  });

});
```
