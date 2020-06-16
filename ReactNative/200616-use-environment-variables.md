
# [React Native] 환경 변수 사용하기

#### Environment

- React Native 0.62

#### References

- [lugg](https://github.com/luggit) / [react-native-config][react-native-config]
- [How to manage staging and production environments in React Native][how-to-env]

---

node 환경에서 `process.env` 를 통해 제공해주는 환경 변수를, React Native 에서는 기본적으로 제공해주지 않는다. 환경 변수를 쓰기 위해서는 별도의 babel 플러그인([babel-plugin-transform-inline-environment-variables](https://stackoverflow.com/questions/33117227/setting-environment-variable-in-react-native))을 사용하거나, 환경 변수를 제공해주는 라이브러리([react-native-dotenv][react-native-dotenv], [react-native-config] 등)를 사용해야 한다.

위 플러그인은 사용 시 번거로움이 있고, [react-native-dotenv][react-native-dotenv]는 development/production 이외의 환경을 공식적으로 제공하지 않기 때문에 제약이 있다. 그래서 사용하기 편리하면서 임의로 환경을 구성할 수 있는 [react-native-config][react-native-config] 를 사용하기로 했다.

[공식 문서][react-native-config]에 들어가면 설치 및 사용 방법이 잘 설명되어 있지만, 딱 하나 제대로 되지 않는 것이 Xcode 에서 archive 기능을 사용할 때다.

### Xcode archive

Xcode 에서 빌드 혹은 아카이브를 실행하면 환경 파일이 자동적으로 `PROJECT_ROOT/.env` 파일로 적용된다. 공식 문서에서는 [Xcode에 스키마를 추가해서 해당 스키마의 빌드/아카이브의 **pre-actions** 옵션에 아래 스크립트를 삽입하라](https://github.com/luggit/react-native-config#ios-1)고 나와있다.

    cp ${PROJECT_DIR}/../.env.dev .env

하지만 알 수 없는 원인 때문에 작동되지 않았다.

[구글링을 해 본 결과][how-to-env] 아래 스크립트를 **pre-actions** 에 넣으면 정상적으로 환경이 적용되는 것을 알아냈다.

    echo ".env.dev" > /tmp/envfile

단 위처럼 하기만 하면 콘솔에서는 무슨 수를 써도 `.env.dev` 가 환경 파일로 적용된다. 그래서 **post-actions** 에 아래 스크립트도 같이 추가해주었다.

    rm /tmp/envfile

이제는 잘 된다.

[react-native-config]: https://github.com/luggit/react-native-config
[react-native-dotenv]: https://github.com/zetachang/react-native-dotenv
[how-to-env]: https://dev.to/calintamas/how-to-manage-staging-and-production-environments-in-a-react-native-app-4naa