[서버리스 웹 애플리케이션 구축](https://aws.amazon.com/ko/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/module-1/)

## 모듈 1. 지속적인 배포를 통한 정적 웹호스팅
[구현 지침] 항목을 따라함

### 1단계. 리전 선택
별다른 이슈 없음

### 2단계: Git 리포지토리 만들기
"e. 리포지토리가 생성되었으므로 다음 지침에 따라 다음 지침에 따라 IAM 콘솔에서 Git 자격 증명을 사용하여 IAM 사용자를 설정하십시오." 항목에서 IAM 사용자를 생성하는 것은 [Step 3: Create Git credentials for HTTPS connections to CodeCommit](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-gc.html#setting-up-gc-iam) 이 링크를 참고함. 아래는 참고해서 사용자를 생성한 과정.

- AWS 콘솔의 IAM 콘솔 접속
- 왼쪽 메뉴에서 [사용자] 선택 -> [사용자 추가] -> 버튼 클릭
  - [사용자 이름] 항목 채움
  - 액세스 유형은 [프로그래밍 방식 액세스] 항목만 체크
  - 다음 페이지 [권한 설정]에서는, 기존에 그룹이 없었기 때문에 그룹 생성
    - "AWSCodeCommitFullAccess" 권한만 할당한 normal 그룹 생성
  - 그리고 다음 버튼 계속 눌러서 생성 완료
- 생성 완료 후 뜨는 "사용자 보안 자격 증명"을 다운로드함
- 다시 왼쪽 메뉴의 [사용자] 페이지로 돌아가서, 목록에서 방금 생성한 사용자 클릭
- [보안 자격 증명] 탭 클릭
- [스크롤 내려서 AWS CodeCommit에 대한 HTTPS Git 자격 증명] 생성

이렇게 만들어진 자격 증명을 "g. 터미널 창에서 git clone과 리포지토리의 HTTPS URL을 실행합니다." 항목에서 사용하면 됨.

### 3단계 : Git 리포지토리 채우기

> a. 디렉토리를 리포지토리로 변경하고 S3에서 정적 파일을 복사하십시오:
> cd wildrydes-site/
> aws s3 cp s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website ./ --recursive

이 항목에서 컴퓨터에 AWS CLI 가 설치되어있지 않기 때문에 진행되지 않았음. AWS CLI 설치는 [macOS 사용자 인터페이스를 사용하여 AWS CLI 버전 2 설치 및 업데이트](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/install-cliv2-mac.html) 이 링크를 참고함.

설치했으나 `aws s3 cp s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website ./ --recursive` 이 부분에서 에러가 남

> fatal error: Unable to locate credentials

[aws cli 초기 설정](https://lovemewithoutall.github.io/it/aws-cli-configure/) 이 링크를 참고해 아래 명령어를 실행함

```
$ aws configure
AWS Access Key ID [None]: AKIAVXU6KE2NYOY6VDAL
AWS Secret Access Key [None]: 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
Default region name [None]: ap-northeast-2
Default output format [None]: json
```

액세스키와 시크릿엑세스키는 아까 2단계를 진행할 때 다운받았던 사용자 보안 자격 증명 에서 가져옴. 이렇게 하니 에러메시지가 바뀜

> An error occurred (AccessDenied) when calling the ListObjectsV2 operation: Access Denied

2단계에서 생성한 사용자의 권한 (정확히는 사용자의 그룹의 권한)에 AmazonS3FullAccess 를 추가했다. 추가하니 이젠 에러 없이 진행된다.

> b. Git 서비스로 파일 커밋하기
> $ git add .
> $ git push

문서의 b 항목은 위에서도 보이듯이, `git add .`과 `git push` 사이에 `git commit`이 빠졌다. (커밋하지 않으면 당연히 진행되지 않는다.)

### 4단계 : AWS Amplify 콘솔을 사용하여 웹 호스팅 활성화

"b. Amplify Console에서 배포를 위해 시작를 클릭"이라고 쓰여있으나, 'AWS Amplify 콘솔' 첫 화면에 시작이라는 버튼이 없음. 그래서 아래처럼 진행함

- 사이드 메뉴의 [모든 앱] 클릭
- [New app] 드랍다운 버튼 클릭
- [Host web app] 클릭 -> [Host your web app] 페이지로 이동
- [Host your web app] 페이지에서 [AWS CodeCommit]을 선택하고 [Continue] 버튼을 누름

이제 스크린샷에 있는 화면과 같은 화면이 나옴

### 5단계 : 사이트 수정
별다른 이슈 없음


## 모듈 2. 사용자 관리
[구현 지침] 항목을 따라함

### 1단계. Amazon Cognito 사용자 풀 생성

"a. AWS Console에서 서비스를 클릭한 다음 모바일 서비스 아래에서 Cognito를 선택합니다." 라고 되어있으나 Cognito 는 모바일 서비스 아래 있지 않고 [보안, 자격 증명 및 규정 준수] 아래 있었음.

### 2단계. 사용자 풀에 앱 추가
별다른 이슈 없음

### 3단계. 웹사이트 Config 업데이트
별다른 이슈 없음

### 4단계. 구현 테스트
별다른 이슈 없음
