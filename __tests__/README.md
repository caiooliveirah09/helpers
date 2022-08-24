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
