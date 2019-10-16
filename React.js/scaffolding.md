# Project Scaffolding

## initialze

```
npm create-react-app <project-name>
```

## react-app-wired

eject 를 하지 않고, 설정을 override

```
yarn add -D react-app-rewired
```

## react-hot-loader with react-app-rewired

[[react-app-rewire-hot-loader Repository 참고]](https://github.com/cdharris/react-app-rewire-hot-loader)

```
yarn add react-app-rewire-hot-loader react-hot-loader

```

## add Sass

```
yarn add -D node-sass
```

## add eslint

```
yarn add -D eslint eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

## add prettier

```
yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
```

## add husky, lint-staged

```
yarn add -D husky lint-staged pretty-quick
```

## sample config file

.eslintrc.json

```JSON
{
  "extends": ["prettier", "prettier/react"],
  "rules": {
    "react/prop-types": 0,
    "no-underscore-dangle": 0
  },
  "globals": {
    "window": true,
    "document": true,
    "localStorage": true,
    "FormData": true,
    "FileReader": true,
    "Blob": true,
    "navigator": true
  },
  "parser": "babel-eslint"
}


```

.prettierrc

```JSON
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80
}
```

package.json

```JSON
{
  ...

  "lint-staged": {
    "*.{js,jsx}": [
      "pretty-quick --staged",
      "eslint src/ --fix",
      "git add"
    ]
  },
  "husky": {
    "hooks": {
      "pre-commit": "NODE_ENV=production lint-staged"
    }
  }
  ...

}
```
