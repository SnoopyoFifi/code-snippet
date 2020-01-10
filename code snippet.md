# code snippet

## array

### reduce

- `Syntax`

  `arr.reduce((prev, cur, index, arr) => {}, init);`

- `Parameters`
  - `arr` ：表示原数组
  - `prev` ：表示上一次执行回调函数的返回值(或者是初始值 `init`)
  - `cur` ：表示当前正在处理的数组元素
  - `index` ：表示当前正在处理的数组元素的索引，若 `init` 有值，则索引从0开始，否则从1
  - `init` ：表示初始值

- `Notice`

  > `reduce` 是数组的 _归并方法_ ，与 `forEach、map、filter` 等迭代方法一样都会对数组每一项进行遍历，
  > 但是 `reduce` 可同时将前面数组项遍历产生的结果与当前遍历项进行运算，这一点是其他迭代方法无法企及的

- `Examples`
  
  - 数组去重
  
    ```js
      const arr = [1, 2, 3, 4, 4, 5, 2, 20];
      const newArr = arr.reduce((prev, cur) => {
        prev.indexOf(cur) === -1 && prev.push(cur);
        return perv;
      }, []);
    ```

  - [zipObject](https://www.30secondsofcode.org/js/s/reduced-filter)
  
    ```js
      const zipObject = (props, values) =>
        props.reduce((obj, prop, index) => ((obj[prop] = values[index]), obj), {})
      zipObject(['name', 'age', 'sex'], ['snoopy',  '30', 'man']);
    ```

  - [reducedFilter](https://www.30secondsofcode.org/js/s/reduced-filter)
  
    ```js
      const reducedFilter = (data, keys, fn) =>
        data.filter(fn).map(el =>
          keys.reduce((acc, key) => {
            acc[key] = el[key];
            return acc;
          }, {})
        );
      const data = [
        {
          id: 1,
          name: 'snoopy',
          age: 30
        },
        {
          id: 2,
          name: 'fifi',
          age: 28
        }
      ]
      reducedFilter(data, ['id', 'name'], item => item.age < 30);
    ```
  
  - [函数式编程-compose与pipe](https://www.cnblogs.com/star91/p/han-shu-shi-bian-chengcompose-yupipe.html)

    ```js
      // pipe
      const pipe = (...fns) => fns.reduce((f, g) => (...args) => g(f(...args)));
      // compose
      const compose = (...fns) => fns.reduce((f, g) => (...args) => f(g(...args)));
      const add5 = x => x + 5;
      const multiply = (x, y) => x * y;
      const multiplyAndAdd5 = compose(
        add5,
        multiply
      );
      multiplyAndAdd5(5, 2);
    ```

  - [对异步操作执行pipe](https://www.30secondsofcode.org/js/s/pipe-async-functions)

    ```js
      const pipeAsync = (...fns) =>
        arg => fns.reduce((p, f) => p.then(f), Promise.resolve(arg));
      const sum = pipeAsync(
        x => x + 1,
        x => new Promise(resolve => setTimeout(() => resolve(x + 2), 3000)),
        x => x + 3,
        async x => (await x) + 4
      );
      (async () => {
        console.log(await sum(5));
      })();
    ```

