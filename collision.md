#  Collision 충돌판정
[1. 사각형끼리의 충돌 판정](#1-사각형끼리의-충돌-판정)  
[2. 원형끼리, 원형과 사각형 충돌 판정](#2-원형끼리-원형과-사각형-충돌-판정)  
[3. 가늘고 긴 물체와 원과의 충돌 판정](#3-가늘고-긴-물체와-원과의-충돌-판정)  
[4. 부채꼴 물체와의 충돌 판정](#4-부채꼴-물체와의-충돌-판정)  
[5. 3D 충돌 판정 이야기](#5-3d-충돌-판정-이야기)

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
1. [상황1] 사각형 1의 오른쪽 끝이 사각형 2의 왼쪽보다 **왼쪽**에 있는 경우
2. [상황2] 사각형 1의 왼쪽 끝이 사각형 2의 오른쪽보다 **오른쪽**에 있는 경우
3. [상황1]이거나 혹은  [상황2]인 경우 충돌하지 않는다.
4. 즉 [상황1] || [상황2]

**사각형끼리 충돌하는 상황**

1. not ([상황1] || [상황2])
2. not[상황1] && not[상황2]  드모르간의 법칙 적용
3. [상황A] = not[상황1] : 사각형 1의 오른쪽 끝이 사각형 2의 왼쪽보다 **오른쪽**에 있는 경우
4. [상황B] = not[상황2] : 사각형 1의 왼쪽 끝이 사각형 2의 오른쪽보다 **왼쪽**에 있는 경우
5. 즉 not[상황1] && not[상황2] == [상황A] && [상황B]
6. [상황A] : pRect1.right > pRect2.left
7. [상황B] : pRect1.left  < pRect2.right

---
<br>

## 2. 원형끼리, 원형과 사각형 충돌 판정

### **[원형끼리 충돌]**
#### 구조체
```
var circleA = {x: 0, y: 0, r: 0};
var circleB = {x: 0, y: 0, r: 0};
```

#### 함수 collisionCircle
```
function collisionCircle(pCircle1, pCircle2) {
	var nResult = false, dx, dy, ar, fDistSqr;

    dx = pCircle1.x - pCircle2.x;				// ⊿ｘ
	dy = pCircle1.y - pCircle2.y;				// ⊿ｙ
	fDistSqr = dx * dx + dy * dy;				// 거리의 제곱 
	ar = pCircle1.r + pCircle2.r;
	if (fDistSqr < ar * ar) {					// 제곱으로 비교 
		nResult = true;
	}
    
	return nResult;
}
```

#### 함수 call
```
collisionCircle(circleA, circleB);
```

#### 설명
두 원형의 중점간의 거리가 두 원형의 반지름을 더한 값 보다 작으면 충돌

---
### **[원형과 사각형 충돌]**
#### 구조체
```
var circle_A = {x: 0, y: 0, r: 0};
var rect_B = {left: 0, top: 0, right: 0, bottom: 0};
```

#### 함수 collisionCircleRect
```
function collisionCircleRect(pRect, pCircle) {
	var nResult = false, ar, fDistSqr;

	// 큰 장방형 체크 
	if ((pCircle.x > pRect.fLeft - pCircle.r) && (pCircle.x < pRect.fRight  + pCircle.r) && (pCircle.y > pRect.fTop - pCircle.r) && (pCircle.y < pRect.fBottom + pCircle.r)) {
		nResult = true;
        ar = pCircle.r;
		// 왼쪽 끝 체크 
		if (pCircle.x < pRect.fLeft) {
			// 좌측상단 모서리 체크 
            if (pCircle.y < pRect.fTop) {
				if (distanceSqr(pRect.fLeft, pRect.fTop, pCircle.x, pCircle.y) >= ar * ar) {
					nResult = false;
				}
			} else {
				// 좌측하단 모서리 체크 
				if (pCircle.y > pRect.fBottom) {
					if ((distanceSqr(pRect.fLeft, pRect.fBottom, pCircle.x, pCircle.y) >= ar * ar)) {
						nResult = false;
					}
				}
			}
		} else {
			// 오른쪽 끝 체크 
			if (pCircle.x > pRect.fRight) {
				// 우측 상단 모서리 체크 
				if (pCircle.y < pRect.fTop) {
					if (distanceSqr(pRect.fRight, pRect.fTop, pCircle.x, pCircle.y) >= ar * ar) {
						nResult = false;
					}
				} else {
					// 좌측 하단 모서리 체크 
					if (pCircle.y > pRect.fBottom) {
						if (distanceSqr(pRect.fRight, pRect.fBottom, pCircle.x, pCircle.y) >= ar * ar) {
							nResult = false;
						}
					}
				}
			}
		}
	}
    
	return nResult;
}
```

#### 함수 call
```
collisionCircleRect(rect_B, circle_A)
```

---

## 3. 가늘고 긴 물체와 원과의 충돌 판정

---

## 4. 부채꼴 물체와의 충돌 판정

---

## 5. 3D 충돌 판정 이야기