#Storybook 에서 global scss 를 사용해야 하는 경우

보통 vue.js 로 코딩을 하게 되면 style 의 lang을 자신에게 맞는 preprocessor로 지정하게 된다.

```<style lang="scss" scoped></style>``` 을 사용 할 때는 global 속성으로 변수 그리고 믹스인 등을 사용하는 경우가 발생하는데, 매번 style 코드에서 import 를 시키게 되면 번들 될 때 import 되는 횟수만큼 중복되는 코드가 생성된다.

이땐 필수적으로 전역 레벨에서의 scss가 필요하게 되는데 일반적인 (우리가 수정 가능 한) 방법으로는 webpack 에서 ```sass-resources-loader``` 과 같은 로더로 쉽게 접근할 수 있지만, ```vue-cli``` 나 ```storybook```에서는 webpack config 를 마음대로 수정 하다가는 무슨일이 발생될지 모르기에 ```storybook``` 기준으로 어떻게 전역레벨에서의 scss파일을 불러오는지 확인 한다.


## 1. .storybook 에 webpack.config.js 만들기
@storybook 의 패키지는 최초에 명령이 실행 될 때 패키지 내 webpack.config.js 를 불러오게 된다. 

이 기본 설정으로 이루어 진 webpack.config.js 를 상속(extend) 받아 일부 설정부분을 합치거나 내용을 추가 할 수 있게 되는데, 이럴때는 .storybook/webpack.config.js 파일을 생성해서 아래와 같은 코드를 넣어준다.

```
// load the default config generator.
const genDefaultConfig = require('@storybook/react/dist/server/config/defaults/webpack.config.js');

module.exports = (baseConfig, env) => {
  const config = genDefaultConfig(baseConfig, env);

  // Extend it as you need.

  // For example, add typescript loader:
  config.module.rules.push({
    test: /\.(ts|tsx)$/,
    include: path.resolve(__dirname, '../src'),
    loader: require.resolve('ts-loader')
  });
  config.resolve.extensions.push('.ts', '.tsx');

  return config;
};
```
[참고 - storybook 가이드 페이지](https://storybook.js.org/configurations/custom-webpack-config/#full-control-mode-default)

이러한 형식으로 webpack.config.js 에 작성을 하게되면 기본적인 설정과 더불어 설정값을 추가적으로 설정할 수 있게 된다.
그리고 scss 로더에 대해 오버라이트를 해 줘야 하는데 아래와 같은 코드로 작성하였다.

```
storybookBaseConfig.module.rules.push({
  test: /\.scss$/,
  loaders: [
    "style-loader",
    "css-loader",
    {
      'loader': "sass-loader",
      'options': {
        includePaths: [
          'src/assets/scss'
        ],
        data: '@import "src/assets/scss/global";'
      }
    }
  ],
  include: path.resolve(__dirname, '../')
});
```

webpack 설정에서 scss 파일에 대한 로더를 설정 한 부분이다.

sass-loader 를 부를 때 option 키에 includePath 를 설정하고 data키에 로더가 기본적으로 실행하는 코드를 작성 해 주면 웹팩에서 scss를 읽을 때 해당 코드를 항상 읽어주게 된다.