# 신경망 모델을 통한 미디파일 장르 분류

이 프로젝트는 고려대학교 세종캠퍼스 전자 및 정보공학과 '한철' 교수님의 '인공신경망과 딥러닝' 수업의 학기말 프로젝트임을 밝힙니다.

프로젝트의 목적은 Midi 파일을 가져와서 음악의 장르를 파악할 수 있는 신경망 모델을 만드는 것입니다.

이 프로젝트를 통해 음악의 악기로 연주할 수 있는 파일을 가져오게 되면 이를 장르를 먼저 파악할 수 있고, 좀 더 나아가서는 장르보다는 사람의 감정에 따라 분류를 할 수도 있는 모델을 만들 수 있을 것입니다.

또한 코딩 전문가가 아닌 대학생 수준에서의 코딩이기에 다른 문서를 참조하거나 코딩의 수준이 낮고, 오픈소스용 코딩으로 만들지 않았기에 참고용으로만 사용해 주시면 감사하겠습니다.

# 모듈

파이썬에서 미디파일을 사용하기 위한 [music21](http://web.mit.edu/music21/)

신경망모델을 만들기 위한 [keras](https://keras.io/) , [tensorflow](https://github.com/tensorflow/tensorflow)

중간 데이터셋을 저장하기 위한 [pickle](https://wayhome25.github.io/cs/2017/04/04/cs-04/) / 출처 : 초보몽키의 개발공부로그

데이터의 shape를 맞춰 주기 위한 [numpy](https://github.com/numpy/numpy)

데이터의 padding과 normalize를 위한 [sklearn](https://github.com/scikit-learn/scikit-learn)

# 데이터 셋

https://freemidi.org/

www.piano-midi.de

http://www.tadpoletunes.com/songs/songs.htm

http://midkar.com/jazz/jazz_13.html

http://midkar.com/country

https://freemidi.org/genre-country

http://www.midiworld.com/search/4/?q=country

http://www.midihifi.fr/playlist-jazz

위 링크에서 가장 동떨어진 장르로 클래식,재즈,컨츄리,댄스,락 으로 대략 100곡 정도를 모아서 사용.

train_set과 validation_set의 8:2 비율로 학습을 할 예정.

모든 미디파일이 비슷한 형태를 띄는 것도 아니고 어떤 미디파일은 다른 악기/트랙/음정등을 사용하기에 악기와 음정의 차원을 가진 데이터로 선처리를 함.

![설명용악보](/image/i_1.png)

각각의 음들을 악보에 표현하면 위 그림처럼 되서 우리는 그중에서 파란색 화살표와 빨간색 화살표를 사용할 예정.

파란색 화살표는 음사이의 시간차 빨간색 화살표는 음사이의 음정의 차로 생각하면 될 것.

즉 2개의 데이터가 하나의 쌍을 이룬다 생각.

![설명용그림1](/image/음차시차.png)

이와 같이 2개의 데이터가 1개의 곡에서 여러쌍을 찾게됨.

여기서 이 2개의 데이터를 노트라고 표현하고, 노트들은 1개의 곡에서도 악기의 종류에 따라 또 여러개 쌓이게 될 것.

악기 종류에 따라 노트가 여러개 쌓이게 되지만 0번 박자부터 500번 박자까지를 slicing해서 1/4박자마다 찾아내도록 하기위해서 2000개의 노트를 준비.

또한 1곡에 모든 악기가 들어 있지 않기에 미디파일에 사용되는 악기의 총수 142개의 차원을 넣어 노트가 없는 부분은 Zero padding을 해줌.

![설명용그림2](/image/선치리.png)

즉, 위 그림과 같이 (전체 곡 500 / 악기 총수 142 / 노트 총수 2000(변경) / 데이터 수 2) 인 인풋 데이터를 완성할 수 있다.

Y데이터는 One Hot 코드로 5개의 장르를 선택하도록 만듬. (ex [0 0 0 0 1])
# 모델

현재 CNN에 3개의 layer를 달고 3,3 커널사이즈로 만든 모델로 사용하고있음.

결과적으로 실패하였기에 일단 1개의 모델만 달아둔 상태.

# 레퍼런스

https://maclab-kaist.github.io/DeepArt/    (미디파일 선처리법/딥러닝을 이용한 예술 튜토리얼)

https://github.com/jskDr/keraspp (케라스 모델 설정법/코딩셰프의 3분 딥러닝, 케라스맛)

https://tykimos.github.io/2017/06/10/Model_Save_Load/    (케라스 학습모델 저장법)
