# zalgo.js V1.0.0
## 설명

일반 텍스트에 유니코드 결합 발음 기호(diacritics)를 무작위로 추가해 크툴루 스타일의 징그러운 글자를 생성합니다. `decode`로 원래 텍스트로 복원할 수 있습니다.

## 설치

```javascript
const zalgo = require('zalgo');
```

## 사용법

### 인코딩

```javascript
const zalgo = require('zalgo');

zalgo.encode("hello");
// h̷̪e̸l̴l̵o̶
```

### 디코딩

```javascript
const zalgo = require('zalgo');

zalgo.decode("h̷̪e̸l̴l̵o̶");
// hello
```

### 강도 조절

```javascript
const zalgo = require('zalgo');

zalgo.setMaxHeight(50);  // 0 ~ 300
zalgo.encode("hello");
```

## API

### `encode(text)`

텍스트를 Zalgo 텍스트로 변환합니다.

**반환:** `String`

### `decode(text)`

Zalgo 텍스트를 일반 텍스트로 복원합니다.

**반환:** `String`

### `setMaxHeight(value)`

Zalgo 강도를 설정합니다.

| 파라미터 | 타입 | 범위 | 기본값 |
|--------|------|------|--------|
| value | Number | 0 ~ 300 | 15 |

범위를 벗어나면 `RangeError`를 던집니다.

```javascript
zalgo.setMaxHeight(300);  // OK
zalgo.setMaxHeight(301);  // RangeError: maxHeight must be between 0 and 300, got 301
```

## 라이센스

MIT

## 참고

- [zalgo.org](https://www.zalgo.org/)

## 업데이트 로그
