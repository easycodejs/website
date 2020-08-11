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
4. 즉 `[상황1] || [상황2]`

**사각형끼리 충돌하는 상황**

1. `not ([상황1] || [상황2])`
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
function distanceSqr(x1, y1, x2, y2) {	            // 거리의 제곱 계산 
    var dx, dy;							            // 위치의 차이 

	dx = x2 - x1;									// ⊿ｘ
	dy = y2 - y1;									// ⊿ｙ

	return dx * dx + dy * dy;
}

function collisionCircleRect(pRect, pCircle) {
	var nResult = false, ar, fDistSqr;

	// 큰 장방형 체크 
	if ((pCircle.x > pRect.left - pCircle.r) && (pCircle.x < pRect.right  + pCircle.r) && (pCircle.y > pRect.top - pCircle.r) && (pCircle.y < pRect.bottom + pCircle.r)) {
		nResult = true;
        ar = pCircle.r;
		// 네 귀퉁이 체크
		// 왼쪽 끝 체크 
		if (pCircle.x < pRect.left) {
			// [귀퉁이 체크 1] 좌측상단 모서리 체크 
            if (pCircle.y < pRect.top) {
				if (distanceSqr(pRect.left, pRect.top, pCircle.x, pCircle.y) >= ar * ar) {
					nResult = false;
				}
			} else {
				// [귀퉁이 체크 2] 좌측하단 모서리 체크 
				if (pCircle.y > pRect.bottom) {
					if ((distanceSqr(pRect.left, pRect.bottom, pCircle.x, pCircle.y) >= ar * ar)) {
						nResult = false;
					}
				}
			}
		} else {
			// 오른쪽 끝 체크 
			if (pCircle.x > pRect.right) {
				// [귀퉁이 체크 3] 우측 상단 모서리 체크 
				if (pCircle.y < pRect.top) {
					if (distanceSqr(pRect.right, pRect.top, pCircle.x, pCircle.y) >= ar * ar) {
						nResult = false;
					}
				} else {
					// [귀퉁이 체크 4] 좌측 하단 모서리 체크 
					if (pCircle.y > pRect.bottom) {
						if (distanceSqr(pRect.right, pRect.bottom, pCircle.x, pCircle.y) >= ar * ar) {
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

#### 설명
1. function distanceSqr(x1, y1, x2, y2)  
네 귀퉁이 체크 시 사각형의 정점이 원 내부에 포함되는지 판단하기 위한 거리 측정용  
사각형의 정점과 원의 중점과의 거리의 제곱 값을 계산하여 리턴  
(x1, y1) : 원에서 제일 가까운 사각형의 정점  
(x2, y2) : 원의 중점
2. 판정할 사각형보다 상하좌우 각각 원의 반지름 r 만큼 확장한 사각형 안에 원의 중심 좌표가 포함되면 충돌 가능성이 있다.
3. 2의 조건을 만족해도 원의 중심 좌표가 원래 사각형의 밖, 확장된 사각형의 각 모퉁이에 있고 또한 원이 사각형의 가장 가까운 정점을 내부에 포함하지 않을 때는 충돌하지 않는다.  
[큰 장방형 체크] : 확장된 사각형 안에 원의 중점이 있고 (2의 조건을 만족 즉 nResult = true;), 
	- [귀퉁이 체크 1] : 사각형의 *좌측상단* 모서리에서 원이 사각형의 *좌측상단* 정점을 내부에 포함하지 않으면 (nResult = false;)
	- [귀퉁이 체크 2] : 사각형의 *좌측하단* 모서리에서 원이 사각형의 *좌측하단* 정점을 내부에 포함하지 않으면 (nResult = false;)
	- [귀퉁이 체크 3] : 사각형의 *우측상단* 모서리에서 원이 사각형의 *우측상단* 정점을 내부에 포함하지 않으면 (nResult = false;)
	- [귀퉁이 체크 4] : 사각형의 *우측하단* 모서리에서 원이 사각형의 *우측하단* 정점을 내부에 포함하지 않으면 (nResult = false;)

---

## 3. 가늘고 긴 물체와 원과의 충돌 판정

### 구조체
```
var circleA = {x: 0, y: 0, r: 0};
```
- (x, y) : 원의 중점 좌표
- r : 원의 반지름
```
var rectCircleB = {x: 0, y: 0, vx: 0, vy: 0, r: 0, newVX: 0};
```
- rectCircleB를 선분으로 보고 양 끝에 반원을 형성한다고 보면 
- (x, y) : 선분 rectCircleB 벡터 (vx, vy)의 출발 좌표
- r : 선분의 굵기의 반, 선분 끝 원의 반지름
- newVX : 회전된 선분 rectCircleB의 새 벡터의 vx 값

### 함수 collisionCircle_RectCircle

```
function collisionCircle_RectCircle(pCircle, pRectCircle) {
	var nResult = false, dx, dy, t, mx, my, ar, fDistSqr, fRate;
    
	fRate = pRectCircle.newVX / pRectCircle.vx;

	dx = pCircle.x - pRectCircle.x;				// ⊿ｘ
	dy = pCircle.y - pRectCircle.y;				// ⊿ｙ

	t = (pRectCircle.vx * dx + pRectCircle.vy * dy) / (pRectCircle.vx * pRectCircle.vx + pRectCircle.vy * pRectCircle.vy);
	if (t < 0) { t = 0; }					    // t의 하한
	if (t > fRate) { t = fRate;	}				// t의 상한 (1이 정상이나 도형그리기에 오차를 보정한 값)
	mx = pRectCircle.vx * t + pRectCircle.x;	// 최소 위치가 되는 좌표
	my = pRectCircle.vy * t + pRectCircle.y;
	fDistSqr = (mx - pCircle.x) * (mx - pCircle.x) + (my - pCircle.y) * (my - pCircle.y);	// 거리의 제곱 
	ar = pCircle.r + pRectCircle.r;
	if (fDistSqr < ar * ar) {					// 제곱인 채로 비교 
		nResult = true;
	}
    
	return nResult;
}
```

### 함수 call
```
```

### 설명
- fRate : 원본 vx의 길이를 t = 1 이라고 할때 선분 rectCircleB가 회전된 후 얻어지는 newVX 의 비율로 t의 상한값으로 사용됨
- dx : 원의 중점의 x 값과 선분 rectCircleB 벡터의 출발점의 x 값의 차이
- dy : 원의 중점의 y 값과 선분 rectCircleB 벡터의 출발점의 y 값의 차이

---

## 4. 부채꼴 물체와의 충돌 판정

---

## 5. 3D 충돌 판정 이야기


$$c^2 = \sqrt{a^2 + b^2}$$
$$x_{1,2} = {-b\pm\sqrt{b^2 - 4ac} \over 2a}.$$

