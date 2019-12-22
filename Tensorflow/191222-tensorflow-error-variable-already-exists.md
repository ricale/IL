# Tensorflow 에러 - Variable already exists

#### Environment

- Python 3.7.4
- Tensorflow 1.15

#### References

- [Error in notebook: "ValueError: Variable conv1/weights already exists, disallowed. Did you mean to set reuse=True in VarScope"](https://github.com/kratzert/finetune_alexnet_with_tensorflow/issues/8) - kratzert/finetune_alexnet_with_tensorflow in GitHub
- [tf.reset_default_graph](https://www.tensorflow.org/versions/r1.15/api_docs/python/tf/reset_default_graph) - Tensorflow API Documentation

---

Jupyter Notebook을 사용해서 Tensorflow 예제 코드를 돌려보다 보면 자주 직면하는 에러.

```
ValueError: Variable conv1/weights already exists, disallowed
```

같은 이름의 variable을 다시 만들지 말라는 에러인데, 그렇다고 variable 사용시 `reuse=True` 같은 옵션을 넣어주기에는 번거롭고 찝찝하다.

해결 방법은 해당 코드블록 최상단에 아래와 같은 코드를 넣어주는 것.

```
tf.reset_default_graph()
```

그러면 Tensorflow에서 그래프 스택을 초기화해주고, 같은 이름의 variable을 다시 사용할 수 있다.