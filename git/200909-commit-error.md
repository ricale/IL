# [git] git commit 시 에러로 커밋이 되지 않음

#### Environment

- react-native 2.24.3

#### References

- [Git Commit Problem: "error: There was a problem with the editor 'vi'"](https://github.com/VundleVim/Vundle.vim/issues/167#issuecomment-11760207) - VundleVim/[Vundle.vim](https://github.com/VundleVim/Vundle.vim)

---

### 이슈

git 커밋 시 아래와 같은 에러가 나면서 커밋이 되지 않는 경우가 있다.

> hint: Waiting for your editor to close the file... error: There was a problem with the editor 'vi'.

개인적으로 주로 경험하는 케이스는 아래와 같다.

1. `git commit` 명령어 입력
2. vim 이 실행됨
3. 로그를 다 작성하고 `:wq` 명령어로 저장 및 종료를 시도하나 명령어 입력 실수로 `:Wq`가 입력되고 저장 및 종료가 되지 않음
4. 재시도로 `:wq` 명령어를 입력함.
5. vim 이 종료되면서 위와 같은 메시지가 출력됨. 커밋은 되지 않음

자주 실수하는 케이스이고, 저장되지 않으면 커밋 메시지를 다시 써야 하므로 굉장히 거슬리고 귀찮다.

### 결론

`git config --global core.editor /usr/bin/vim` 명령어를 입력하니 해결되었다.
