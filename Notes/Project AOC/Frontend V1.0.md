## Import and Export
In React, `export` means making a component, function, or variable available to other files in project.
### Default Export
```javascript
// Default export
export default Appheader;
```
When importing a default export, we **do not need curly braces**, and we can name it anything:
```javascript
import Header from './AppHeader'; // Header is now AppHeader
```
### Named Export
```javascript
// Named export
export const AppHeader = () => {
  return <header>Welcome!</header>;
};

export const Footer = () => {
  return <footer>Goodbye!</footer>;
};
```
When importing named exports, we must use **curly braces** and the exact names:
```javascript
import { AppHeader, Footer } from './components';
```
## Arrow Function
**JavaScript Grammar**: The `= () =>` syntax is valid JavaScript and is a modern replacement for traditional function expressions like:
```javascript
const AppHeader = function() {
    return <header>Welcome!</header>;
};
```

```javascript
const AppHeader = () => {
  return <header>Welcome!</header>;
};
```
If needed, we can pass parameters in the `= () =>` parentheses.
## 