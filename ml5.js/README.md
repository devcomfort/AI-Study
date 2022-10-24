<h1>ml5.js</h1>

`ml5.js`는 `Tensorflow.js` 홈페이지에서 `Tensorflow.js`에 접근하기 어려운 아마추어 사용자를 위해 소개한 머신러닝 라이브러리입니다. <br>

- [`ml5.js` 한줄평](#ml5js-한줄평)
- [`ml5.js`에 대한 소개 (설치법, 사용법, 의존성 소개)](#ml5js에-대한-소개-설치법-사용법-의존성-소개)
- [`ml5.js` 참고 자료](#ml5js-참고-자료)

## `ml5.js` 한줄평

[ml5js 홈페이지](https://ml5js.org/)를 읽어본 결과, `ml5.js`는 단순히 `ml5.js` 내에 미리 작성된 모듈을 가지고 학습을 할 수 있도록 지원하는 JS 라이브러리입니다.

머신러닝을 제대로 공부하고 싶다면 어렵더라도 `TF.js (Tensorflow.js)`나 파이썬 기반의 `Keras`, `TensorFlow`, `PyTorch` 같은 라이브러리를 사용하는 것을 권합니다.

## `ml5.js`에 대한 소개 (설치법, 사용법, 의존성 소개)

`ml5.js` 홈페이지에서는 `ml5.js`를 사용하기 위해 `yarn`, `npm`과 같은 별도의 의존성 관리자를 사용하는 대신 `CDN`을 사용해 웹사이트레 스크립트를 심도록하고 있습니다.

또한 `ml5.js`는 [프로세싱 언어](# "프로세싱 언어: 컴퓨터 프로그래밍의 본질을 시각적 개념으로 프로그래머가 아닌 사람에게 교육하기 위한 목적으로 만든 그래픽용 언어")인 `p5.js`를 기반에 두고 있습니다.

때문에 `ml5.js`의 사용을 위해서는 `ml5.js`와 `p5.js` 모두를 삽입한 후, 마지막으로 별도의 학습 코드를 삽입함으로써 완성됩니다.

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.0.0/p5.min.js"></script>
<script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
```

코드 삽입을 완료했다면 `sketch.js` 코드를 추가로 작성해주세요. <br>
형식은 다음과 같습니다.

```javascript
/** sketch.js */
// Initialize the Image Classifier method with MobileNet. A callback needs to be passed.
let classifier;

// A variable to hold the image we want to classify
let img;

function preload() {
  classifier = ml5.imageClassifier("MobileNet");
  img = loadImage("images/bird.png");
}

function setup() {
  createCanvas(400, 400);
  classifier.classify(img, gotResult);
  image(img, 0, 0);
}

// A function to run when we get any errors and the results
function gotResult(error, results) {
  // Display error in the console
  if (error) {
    console.error(error);
  } else {
    // The results are in an array ordered by confidence.
    console.log(results);
    createDiv(`Label: ${results[0].label}`);
    createDiv(`Confidence: ${nf(results[0].confidence, 0, 2)}`);
  }
}
```

## `ml5.js` 참고 자료

- [위키독스 - p5 자바스크립트와 ml5 머신러닝라이브러리](https://wikidocs.net/book/5373)
