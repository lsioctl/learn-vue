# tictactoe

A homework rewritting my TicTacToe from React tutorial to Vue.

## Notes

This TicTacToe might look very different from others available on Internet,
as I wanted to really follow React's (excellent) tutorial and having
multiple components communicating together.

I used almost the same (two way) data flow as React:

- from parents to children: passing props
- from children to parent: callbacks (passed as props from parents)

Here it is said it an anti pattern in Vue:

https://www.bryanleetc.com/passing-functions-as-props-an-anti-pattern-in-vue-js/

I think I understand where he gets from, but in this simple case it might be OK.

Still have to test using event for data from children to parent though.

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
