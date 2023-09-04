# 브루트 포스(brute force)
- 완전 탐색 알고리즘 : 가능한 모든 경우의 수를 탐색하면서 요구조건에 충족되는 결과를 찾음 -> 연산 횟수는 많으나 못푸는 문제는 없다..
- 순차 탐색, 깊이 우선 탐색, 너비 우선 탐색
- 주어진 문제를 선형 구조로 구조화하는 능력이 필요
- a_linear.py 참고
*일단 브루트포스로 연습을 계속하면서 구현하고, 감을 잡고, 나중에 다양한 방법을 통해서 개선하자!*

<br>

# 분할정복
- 분할 : 문제의 사례를 둘 이상의 충분히 작은 사례롤 분할
- 정복 : 작은 사례를 각각 정복
- 통합 : 필요하면, 작은 사례의 해답을 통합해 원래 사례의 해답을 도출
- b_binary.py 참고

<br>

---

<br>

# bubble sort
- 인접한 배열의 두 수를 선택해, 그 두 수가 정렬되어 있지 않다면 두 수를 정렬하는 방식
    ![bubble_sort](https://res.cloudinary.com/practicaldev/image/fetch/s--AXL0Lmqr--/c_imagga_scale,f_auto,fl_progressive,h_900,q_auto,w_1600/https://miro.medium.com/max/388/1%2A7QsZkfrRGhAu5yxxeDdzsA.png)

# selection sort
- 순차적으로 가장 작은 값을 탐색하여 배열의 0번 인덱스 부터 마지막 인덱스까지 채워넣는 정렬
