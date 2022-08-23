## strange structure that I got confused and decided to save

```
  useEffect(() => {
    let newNewPlanets = newPlanets;
    let newOptions = options;
    filterByNumericValues.forEach((f) => {
      newNewPlanets = newNewPlanets.filter((planet) => {
        if (f.comparison === 'maior que') {
          return (Number(planet[f.column]) > Number(f.value));
        }
        if (f.comparison === 'menor que') {
          return (Number(planet[f.column]) < Number(f.value));
        }
        return (Number(planet[f.column]) === Number(f.value));
      });
    });
    filterByNumericValues.forEach((f) => {
      newOptions = newOptions.filter((option) => f.column !== option);
    });
    setFinalPlanets(newNewPlanets);
    setOptions(newOptions);
  }, [filterByNumericValues, newPlanets]);
```
