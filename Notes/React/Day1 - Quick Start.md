### 1. Functions as Components or Data Handlers
A function in React can serve two purposes: as a **component** or for **handling data**.  
- When the function represents a component, it is called with `<FunctionName />`.
- When the function handles data or responses, it is passed down using `{functionName}`.
### 2. When to use `{ }`?
- `<FunctionName />` is used to **call** a function, specifically a **component**.
- `{value/functionName}` is used to **pass down** values or functions, such as data or response handlers (`onClick = {handleClick}`).
### 3. Why use `<>< />` or `<div></div>`?
React components are designed to return a single root element. By enforcing a **single root** element, React avoids ambiguity about how to merge multiple elements into the **DOM tree**.
### 4. `export default` & `return`
- `export default` is the **entry point** of the **whole application**.
- `return` is the **exit point** of **this function**, return a component.
### 5. `count ++` & `count + 1` in `setCount()`
In `const [count, setCount] = useState()`, **cannot** replace `setCount(count + 1)` with `setCount(count++)`, because:
- `count` is a constant (`const`) and can **only** be changed using the `setCount` function.
- `count++` **directly** modifies the value of `count`, which is not allowed.
### 6. `products.map(product => )`
- **`map()`**: **Iterates** through `products`.
- **`=>`**: Implicitly **returns** the element for each `product`.