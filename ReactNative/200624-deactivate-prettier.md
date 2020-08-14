
# [React Native] prettier 비활성화

#### Environment

- react-native 0.62
- typescript 3.8.3
- eslint-config-prettier 6.11.0

#### References

- [How to manage staging and production environments in React Native](https://github.com/facebook/react-native/issues/26903) - Stack Overflow

---

[prettier](https://prettier.io/) 는 코드를 일관성 있고 가독성 있게 유지시켜주는 툴이다. 일반적으로 [eslint](https://eslint.org/) 와 비슷한 형식으로, 혹은 eslint 와 같이 엮어서 많이 사용된다. React Native 환경에서 사용되는 기본 eslint 설정인 [react-native-community/eslint-config](https://www.npmjs.com/package/@react-native-community/eslint-config) 에 prettier 가 기본으로 포함된다.

나는 prettier 의 [printWidth](https://prettier.io/docs/en/options.html#print-width) 옵션을 좋아하지 않는다. 배열이나 오브젝트, 함수 작성 시 줄바꿈을 많이 하는 나와 맞지 않는다. 문서를 살펴 봐도 타협할 수 있는 방법이 보이지 않았으므로 prettier 를 끄고자 했다.

하지만 react-native-community/eslint-config 의 디펜던시에 prettier 가 포함되어 있기 때문에 프로젝트에서 prettier 를 지워도, `.prettierrc.js` 파일을 지워도 eslint 실행 시 prettier 가 적용되는 것을 막을 수 없다.

물론 해결 방법은 있다.

[eslint-config-prettier](https://github.com/prettier/eslint-config-prettier#readme) 를 설치해서 아래처럼 .eslintrc.js 옵션을 작성해주면 된다.

```javascript
module.exports = {
  // ...
  extends: [
    '@react-native-community/eslint-config',
    'eslint-config-prettier', // 추가해주어야 할 문장
    // ...
  ],
  rules: {
    'prettier/prettier': 0, // 추가해주어야 할 문장
    // ...
  },
  // ...
};
```

단 위처럼 prettier를 꺼버리면 `comma-dangle`, `quotes` 등 prettier 를 통해 적용되고 있던 일부 lint 옵션들이 꺼질 수 있다. 그러면 `rules` 필드에 원하는 룰을 추가해주면 된다.

```javascript
module.exports = {
  // ...
  rules: {
    'prettier/prettier': 0,
    'comma-dangle': ['error', 'always-multiline'], // 이런 식으로 원하는 룰을 추가해주자.
    'quotes': ['error', 'single'],
    'semi': ['error', 'always']
  },
  // ...
};
```