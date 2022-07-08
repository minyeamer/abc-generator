# Reference Notes

---

## 00. Idea

### Scraping
- abcnotation.com에는 70만개의 파일이 있지만,   
  대부분이 가사와 같은 노이즈 정보가 섞인 데이터고 너무 많은 데이터는 학습 시간의 증가를 발생
- 때문에, 누군가가 일정한 규칙을 가지고 정리한 파일들만을 수집해서 데이터로 활용
- 결과, 약 5천개의 파일을 가지고 활용할 예정

### Vectorizing
- 참고 논문에서는 tune body를 구성하는 문자만을 사용해 학습을 진행했지만,   
  박자(M), 노트 길이(L), 키(K)에 대한 정보를 토큰과 함께 제공하면 더욱 그럴싸한 결과가 나올 것이라 판단
- Body의 경우 특정한 의미를 가지고 있는 기호의 쌍을 하나의 문자로 표현할지, 각각을 벡터로 변환할지 고민 중

---

## 01. The ABC Music Standard 2.1
- abcnotation.com의 공식 문서를 통해 abc format에 대한 자세한 정보를 얻을 수 있음
- 모델링에 있어서 필요한 1)information fields, 2)tune body 에 대한 정보만 수집

### Information Fields
- abc notation은 곡에 대한 상세한 정보가 담긴 information fields를 포함
- information fields는 A부터 Z까지의 알파벳에 해당하는 필드명을 보유
|Field name|Tune header|Type|Examples and notes|
|:-|:-|:-|:-|
|X:reference number|first|instruction|X:1, X:2|
|T:tune title|second|string|T:Paddy O'Rafferty|
|M:meter|yes|instruction|M:3/4, M:4/4|
|L:unit note length|yes|instruction|L:1/4, L:1/8|
|Q:tempo|yes|instruction|Q:"allegro" 1/4=120|
|K:key|last|instruction|K:G, K:Dm, K:AMix|

### Tune Body
- **Pitch**: A-G, a-g 알파벳으로 구성되며, 옥타브를 올리거나 내리기 위해 ' 또는 , 기호를 추가
- **Accidentals**: 임시표를 적용하기 위해 ^, =, _ 기호를 문자 앞에 추가하며, 기호가 반복되는 경우도 있음
- **Note lengths**: 음표 길이를 조절하기 위해 A3, A/2, A3/2 형식으로 표시, L 필드와 중첩해서 적용됨
- **Broken rhythm**: 점음표를 표시하기 위해 >, < 기호를 문자 사이에 추가
- **Rests**: z 문자로 쉼표 표시, 여러 마디 쉼표를 표시할 때는 Z 문자 사용
- **Beams**: 연음을 표시하기 위해 ` 기호를 문자 사이에 추가
- **Reapeat/bar symbols**: |, |], ||, [|, |:, :|, :: 기호가 존재
- **Ties and slurs**: 붙임줄과 이음줄을 표시하기 위해 () 기호로 문자를 묶음
- **Grace notes**: 꾸밈음을 표시하기 위해 {} 기호로 문자를 묶음
- **Decorations**: ., ~, H, L, M, O, P, S, T, u, v 기호가 존재
- **Symbol lines**: 다수의 기호를 표시하기 위해 !...! 또는 "..."로 감싸진 표현
- **Chords and unisons**: 동시에 연주하는 음을 표시하기 위해 [] 기호로 문자를 묶음

### References
- https://abcnotation.com/wiki/abc:standard:v2.1

---

## 02. Music21 라이브러리를 활용한 미디 데이터 분석

### References
- https://inspiringpeople.github.io/data%20analysis/midi-music-data-extraction-using-music21/

---

## 03. Music Generation Using Deep-Learning

### Music Generation
- Music generation started by randomly selecting sounds and combining them.
- Another idea was to make use of musical grammar to generate music.

### Elements of Music
- **Note**: the sound produced by a single key
- **Chords**: the sound produced by 2 or more keys simultaneously, most chords contain at least 3 key sounds.
- **Octave**: a repeated pattern, each octave contains 7 white and 5 black keys.

### References
- https://www.wenyanet.com/opensource/ko/61fd2622827eba0d0d7899d2.html
- https://github.com/soumya997/Music-Generation-Using-Deep-Learning
- https://www.analyticsvidhya.com/blog/2020/01/how-to-perform-automatic-music-generation/

---

## Additional References
- [Music Generation using Three-layered LSTM](https://arxiv.org/abs/2105.09046)
- [Music.Generation.with.DeepLearning](https://github.com/laventura/Music.Generation.with.DeepLearning)
- [Music21 가이드](https://ddggblog.tistory.com/228)
- [딥러닝을 이용한 BGM 음원 작곡 서비스 설계 및 구현](https://www.koreascience.or.kr/article/CFKO201924664108480.pdf)
- [딥러닝을 이용한 음악 생성](https://www.wenyanet.com/opensource/ko/61fd2622827eba0d0d7899d2.html)
- [딥러닝을 이용한 음악 생성 Github](https://github.com/soumya997/Music-Generation-Using-Deep-Learning)
- [딥러닝을 이용한 음악 생성 Demo](https://www.abcjs.net/abcjs-editor.html)
- [music21.abcFormat](https://web.mit.edu/music21/doc/moduleReference/moduleAbcFormat.html)
- [Music21 라이브러리를 활용한 미디 데이터 분석](https://inspiringpeople.github.io/data%20analysis/midi-music-data-extraction-using-music21/)
- [abc notation of tunes](https://www.kaggle.com/datasets/raj5287/abc-notation-of-tunes/code)
- [Interacting with GPT-2 to Generate Controlled and Believable Musical Sequences in ABC Notation](https://aclanthology.org/2020.nlp4musa-1.10.pdf)
