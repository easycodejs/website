#  Collision 충돌판정
[1. 사각형끼리의 충돌 판정](#1.-사각형끼리의-충돌-판정)<br>
[2. 원형끼리, 원형과 사각형 충돌 판정](#2.-원형끼리,-원형과-사각형-충돌-판정)<br>
[3. 가늘고 긴 물체와 원과의 충돌 판정](#3.-가늘고-긴-물체와-원과의-충돌-판정)<br>
[4. 부채꼴 물체와의 충돌 판정](#4.-부채꼴-물체와의-충돌-판정)<br>
[5. 3D 충돌 판정 이야기](#5.-3D-충돌-판정-이야기)

---

## 1. 사각형끼리의 충돌 판정

### 사각형 구조체 사용
```
var rect_A = {left: 0, top: 0, right: 0, bottom: 0};
var rect_B = {left: 0, top: 0, right: 0, bottom: 0};
```

### 함수 collisionRect

```
function collisionRect(pRect1, pRect2) {
	var nResult = false;

	if ((pRect1.right > pRect2.left) && (pRect1.left  < pRect2.right)) {
		if ((pRect1.bottom > pRect2.top) && (pRect1.top < pRect2.bottom)) {
			nResult = true;
		}
	}

	return nResult;
}
```

### 함수 call
```
collisionRect(rect_A, rect_B);
```

### 설명

**사각형끼리 충돌하지 않는 상황**

1. 사각형 1의 오른쪽 끝이 사각형 2의 왼쪽보다 왼쪽에 있는 경우
2. 사각형 1의 왼쪽 끝이 사각형 2의 오른쪽보다 오른쪽에 있는 경우



---

## 2. 원형끼리, 원형과 사각형 충돌 판정

---

## 3. 가늘고 긴 물체와 원과의 충돌 판정

---

## 4. 부채꼴 물체와의 충돌 판정

---

## 5. 3D 충돌 판정 이야기