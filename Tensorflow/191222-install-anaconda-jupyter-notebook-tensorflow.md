# Anaconda, Jupyter Notebook, Tensorflow 설치

#### Environment

- Mac OS 10.15.2

#### References

- [Anaconda, Jupyter Notebook, TensorFlow and Keras for Deep Learning](https://medium.com/@margaretmz/anaconda-jupyter-notebook-tensorflow-and-keras-b91f381405f8) - Margaret Maynard-Reid in Medium

---

### 1. Anacoda 홈페이지에 들어가서 Anaconda를 다운 받아 설치한다.

[링크](https://www.anaconda.com/distribution/). 설치하면, 다운받을 때 선택했던 Python 버전에으로 가상환경(virtualenv)을 활성화해준다.

### 2. Tensorflow를 설치한다.

터미널에서 아래와 같은 명령어를 사용해 설치한다.

```
$ pip install tensorflow
$ pip install tensorflow==1.5 # 1.5버전을 사용하고 싶으면 이렇게 설치
```

`pip3` 명령어를 써서 설치하면 jupyter notebook에서 인식하지 못할 수도 있다. (Anaconda와 다른 설치 경로를 가리키고 있는 듯)

### 3. 주피터 노트북을 실행한다.

설치된 Anaconda-Navigator를 사용하는 방법도 있지만, 터미널에서 아래와 같은 명령어를 치는 것도 가능하다.

```
your-directory$ jupyter notebook
```

작업할 디렉토리에서 실행하면 된다. 실행한 디렉토리의 상위 디렉토리로는 이동할 수 없다는 점 참고.