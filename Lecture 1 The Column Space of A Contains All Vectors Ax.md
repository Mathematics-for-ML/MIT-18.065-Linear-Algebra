# Lecture 1, The Column Space of A Contains All Vectors Ax

Tags: changhyeon nam

> Gilbert Strang의 18.065 강의 Lecture 1: The Column Space of A Contains All Vectors Ax를 정리한 내용이다. Matrix와 Vector의 multiplication, Matrix와 Matrix의 multiplication을 올바르게 이해하는 것을 다루고, Column space, Row space, basis vector 등을 다룬다.
>

---

## Multiplying a matrix by vector

$A = \begin{bmatrix} 2&1&3 \\ 3 & 1&4 \\ 5&7&12\end{bmatrix},\space x=\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}$

위와 같이 행렬 $A$ 와 벡터 $x$ 가 있다고 하자. $Ax$를 계산하는 방법은 크게 두가지가 있다.

1. A의 각 row와 x를 dot product하는 계산하는 방법
2. vectorwise로 product하여 계산하는 방법

행렬과 벡터를 올바르게 계산하는 방법은 2번 방법이고, 다음과 같이 표현할 수 있다.

$Ax = x_1\begin{bmatrix}2\\3\\5\end{bmatrix}+x_2\begin{bmatrix}1\\1\\7\end{bmatrix}+x_3\begin{bmatrix}3\\4\\12\end{bmatrix}$

$Ax$는 벡터 $x$을 선형변환 행렬 $A$를 통해 계산된 새로운 벡터 $x'$이라고 할 수 있다. ($Ax=x'$)

## Column space, rank

행렬 A의 column의 모든 combination은 행렬 A의 column space와 동일하다. 다시말하면 $Ax$로 표현될 수 있는 모든 공간이 A의 column space, $C(A)$라고 할 수 있다.

$B=\begin{bmatrix}1&3&8\\1&3&8\\1&3&8\end{bmatrix}$

위의 경우엔 $B$의 각 column이 모두 서로 dependent하기 때문에 $C(B)=rank(B)=1$이고, B의 column space는 line으로 표현된다.

$A = \begin{bmatrix} 2&1&3 \\ 3 & 1&4 \\ 5&7&12\end{bmatrix}$

위의 행렬 $A$의 경우 세번째 column은 첫번째와 두번째 column의 합으로 표현되기 때문에, 세번째 column은 나머지 두개에 linearly dependent하다. 그래서 $C(A)=rank(A)=2$이고, A의 column space는 plane으로 표현된다.

## Row space, rank

Row rank는 row space의 dimension을 의미한다. 즉 Row space of A는 A의 row로 표현할 수 있는 모든 combination이고, 이는 Transpose of A의 column space와 동일하다.

## Matrix Factorization of A

$A=\begin{bmatrix} 2&1&3 \\ 3 & 1&4 \\ 5&7&12\end{bmatrix}= \begin{bmatrix} 2&1 \\ 3 &1 \\ 5&7\end{bmatrix} \begin{bmatrix}1&0&1 \\ 0&1&1\end{bmatrix}$

행렬 A를 위와 같이 $A=CR$ 로 factorize해보자.

$C=\begin{bmatrix} 2&1 \\ 3 &1 \\ 5&7\end{bmatrix}, R=\begin{bmatrix}1&0&1 \\ 0&1&1\end{bmatrix}$이고, R은 reduced row echelon form이라고도 불린다.

이때 C는 basis for column space, R은 basis for row space로 이뤄진 행렬이다.

여기서, 각 col 혹은 row가 행렬의 basis이기 위해선 다음 두가지를 확인해야 한다.

1. Check independent
2. Check that combinations of basis produces all rows/columns.

위에서 확인할 수 있는것은 rank = #independent col = #independent row = #basis for col space = #basis for row space가 성립한다는 것을 알 수 있다. Column rank = Row rank 임을 증명하는 법은 여러가지 방법이 있는데, 다음 [링크](https://en.wikipedia.org/wiki/Rank_(linear_algebra)#Proofs_that_column_rank_=_row_rank)에 잘 설명 되어 있다.

만약 행렬 $A$가 정방행렬이 아닌, shape이 (m,n)인 매우 큰 행렬 일 경우에는 A의 column space를 어떻게 알수 있을까? 가장 대표적인 방법은 샘플링을 통해 A의 column space를 추정하는 것이다.

$x=randn(m,1)$

위와 같은 랜덤 함수를 통해 예를들어 100개의 벡터 $x$들을 구하고,  $Ax$를 통해 A의 column space를 추정 할 수 있다. 왜냐하면 결국 $Ax$ 또한 $A$의 column space에 있는 벡터이기 때문이다. 같은 논리로 $ABCx$의 결과 또한 A의 Column space에 있다.

## Multiplying a matrix by matrix

Matrix와 matrix의 multiplication을 올바르게 이해하려면 Row와 Col의 Dot product 방식이 아닌, sum of Col * Row의 방식으로 이해해야 한다.

1. dot product

    ![Untitled](https://i.imgur.com/pKgEji6.png)
2. Sum of Columns x rows

    ![Untitled 1](https://i.imgur.com/xYqb0RY.png)

이때 A의 shape이 (m,n)이고, B의 shape이 (n,p)라고 해보자. 각 방식의 multiplication 횟수를 계산해보면 다음과 같다. (결과 값은 동일하다.)

1. dot product → $m\cdot np$ 번의 multiplication
2. sum of Columns x rows → $n\cdot mp$번의 multiplication