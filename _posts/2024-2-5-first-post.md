---
layout: post
title: First post
permalink: /first-post/
---

First post to test which technology my website lacks:


A; Công thức toán

1; Ký hiệu

- $p$ elements $\textbf{x}_j$ = $(x_{1j},...,x_{nj})^T$
- $d(\textbf{x}_j,\textbf{x}_{j'})$: dissimilarity between j and j’
- $\textbf{D}$ (pxp symmetric matrix): matrix of dissimilarity
- $\textbf{K}$: number of clusters
- $\textbf{M} = (M_1,...,M_k)$: set of K collection. K collections have the sum of elements equal to $p$ (or: $|M_1|+...+|M_k|=p$)
- Each element $\textbf{x}_j:$
    - $d(\textbf{x}_j,M_k)=$? (=kc tu 1 diem toi medoid cua cluster do)
    - Label: $l_1(\textbf{x}_j,\textbf{M}^*)$ là medoid ứng với vecto $\textbf{x}_j$ đó
    - Minimum: $min_{k=1,...,K}d(\textbf{x}_j,M_k) = d_1(\textbf{x}_j,\textbf{M})$ là khoảng cách min của $x_j$ tới $\textbf{M}$ collection.
    - Minimizer: $min^{-1}_{k=1,...,K}d(\textbf{x}_j,M_k)=l_1(\textbf{x}_j,\textbf{M})$
- $\textbf{M}^*$: tập các medoids
- $l(\textbf{X},\textbf{M}^*) = (l_1(\textbf{x}_1,\textbf{M}^*),...,l_1(\textbf{x}_p,\textbf{M}^*))$: tập các label (thông tin về các medoid của các điểm)
- $a_j= avg\ d(\textbf{x}_j,\textbf{x}j')\ (j' \in {i: l_1(\textbf{x}_i,M) = l_1(\textbf{x}_j,M)})$
- $b_{jk} = avg\ d(\textbf{x}_j,\textbf{x}_{j'}) \ (j' \in {i:l_1(\textbf{x}_i,M)=k})$
- $b_j=min_kb_{jk}$
- $\~b_j=$ is the dissimilarity of the element $x_j$ and the second-closest medoid $M_k$ = $d_2(\textbf{x}_j,\textbf{M})$
- Silhouette của vector $\textbf{x}_j$: $S_j(\textbf{M})=\frac{b_j-a_j}{max(a_j,b_j)} \in [-1,1]$ (the silhouette
measures how well matched an element is to the other elements in its own cluster versus how well matched it would be if it were moved to another cluster)
- The cluster labels produced by a given algorithm applied to D are **an estimate** of the true cluster labels, which we call the clustering parameter
- 

```jsx
diC => mot mang co kich co k - 1 tam thoi de luu 
diC[l] = UCTdist[ik+j]/Nj[j]; 
// min b ung voi cac b cua cac phan tu

ldiC => co kich co k - 1; 
luu ten cac cluster tam thoi khac voi 
cluster hien tai
```

2; Các version

- K-means clustering:
- PAM:
    - Input: $\textbf{D}$
    - Chọn các medoid $\textbf{M}^*$ bằng cách ⇒ min $\textbf{M}^* = min^{-1}_M \sum_j d_1(\textbf{x}_j,M)$.
    - maximizes over all potential medoids M the function: $f(\textbf{M})=-\sum_jd_1(x_j,\textbf{M})$
- PAMSIL
    - maximizes over all potential medoids M the function (= maximize silhouette) : $f(\textbf{M})=\sum_j S_j(\textbf{M})=\frac{b_j-a_j}{max(a_j,b_j)}$. How:
        - Step 1: Let m = 0 and choose M^m. Define $\textbf{M}_{-i}=(M_1,...M_{i-1},M_{i+1},...,M_K)$
        - Step 2: For every swap $(\textbf{M}^m_{-i},h)$ of one of the K current medoids i with a non-medoid element h,
        calculate $f(\textbf{M}^m_{-i},h)$. Let $i^*$and $h^*$ be the swap that gives the maximal value of $f(.)$. Then, let $\textbf{M}^{m+1}=(\textbf{M}^m_{-i^*},h^*)$
            
            (= swapping each medoid with every non-medoid and accept the swap which cooresponds with the greatest positive improvement in the criteria function f(.)
            
            ⇒ each element is considered as a potential medoid while holding the other K 71 medoids fixed and the best of these ‘‘coordinate changes’’ is accepted
            
            ⇒ vector of medoids is updated at each iteration with the single swap of one medoid with a non-medoid that maximizes the improvement of f(.))
            
        - Step 3: Set m = m + 1 and repeat 2 and 3 until convergence. Denote the solution by $\textbf{M}^*$
- PAMMEDSIL
    - maximizes over all potential medoids M the function (= maximize medoid-based silhouette): $f(\textbf{M})=\sum_j \~S_j(\textbf{M})=\frac{\~b_j-a_j}{max(a_j,\~b_j)}$

3; Implementation for comparison

- So sánh $\textbf{B}=100$ lần ⇒ thực hiện việc tính toán 100 lần để so sánh (100 bộ dataset)
- $p=60,n = 500, k =3$ (500 gene, 3 loại cancer, 60 bệnh nhân)
- Cancer 1: gene 1-25 có $\mu_j=\log3$, gene 25-50 có $\mu_j=-\log3$
- Cancer 2: gene 51-75 có $\mu_j=\log3$, gene 76-100 có $\mu_j=-\log3$
- Cancer 3: gene 101-125 có $\mu_j=\log3$, gene 126-150 có $\mu_j=-\log3$ (350 gene còn lại của 3 loại cancer auto hiểu là $\mu_j=\log0$

⇒ nani??

- $p=500,n=60,k=7$ ⇒ cluster xem gene nào overexpressed, underexpressed,…. ⇒ mục tiêu đi tìm 2 cluster 25 gene gây ra ung thư của mỗi loại cancer (…In other words, the cause of each of the three types of cancer is related to 50 genes of which 25 are suppressed (tumor-suppressor genes) and 25 are over-expressed (the onco-genes)…). Cluster 350 gene còn lại thì là mean $\mu_j=0$

4; Kết quả implement

- Tìm ra đúng: six clusters of 25 genes and one large cluster of 350 non-differentially expressed genes.
    - The true cluster labels correspond with a true average silhouette of 0.27
- PAM did not tend to split or combine the six small clusters, but often split the mean zero genes into two clusters, combining about half of them with one of the six
small clusters.

B; Mining code

1; Hàm phụ trợ

- indexing (17) (// 0. Relevant functions)
    - int indexing(int N, int i, int j){
    - // indexing(): Convert 2d index to 1d index to extract elements from dist objects
- swap_to_clustering(4) (phần 5: The PAMSil algorithm)
    - IntegerVector swap_to_clustering(NumericVector dist, IntegerVector medoids, IntegerVector C1st, IntegerVector C2nd, NumericVector d1st, NumericVector d2nd, int N, int k, int s_i, int s_j){
    - //swap_to_clustering() efficiently compute a clustering given a swap in O(N) time
- expand_dist(3) (phần 4:The original Fast Optimum Silhouette Algorithm)
    - NumericVector expand_dist(NumericVector dist, int N){
    - //expand_dist() expands the dist object by one row
- nearest_and_2nd_nearest(10) (phần 5: The PAMSil algorithm)
    - void nearest_and_2nd_nearest(NumericVector dist, IntegerVector medoids, IntegerVector C1st, IntegerVector &C2nd, NumericVector &d1st, NumericVector &d2nd, int N, int k){
    - //nearest_and_2nd_nearest() computes the nearest and second nearest distances from each point to other medoids.

2; Hàm chính

- ASWCpp(3) (// 0. Relevant functions)
    - double ASWCpp(IntegerVector C, NumericVector dist, int N, int k)
    - Compute the Average Silhouette Width
- subDistCpp(1) (// 0. Relevant functions)
    - NumericVector subDistCpp(NumericVector dist, IntegerVector idx, bool diag, bool upper, int N, int n)
    - subDistCpp(): Extract a sub-distance matrix from a "dist" object
- SWCpp(6) (// 0. Relevant functions)
    - List SWCpp(IntegerVector C, NumericVector dist, int N, int k){
    - SWCpp(): Compute the Silhouette Widths
- effOSilCpp(1) (// 1. The Efficient Optimum Silhouette algorithm)
    - List effOSilCpp(NumericVector dist, IntegerVector iC, int N, int k){
    - effOSilCpp(): the Efficient Optimum Silhouette Clustering Algorithm
- OSilCpp(1) (phần 2: The original Optimum Silhouette algorithm)
    - List OSilCpp(NumericVector dist, IntegerVector iC, int N, int k){
    - //OSilCpp(): The original Optimum Silhouette Clustering Algorithm
- PAMSilCpp  (phần 5: The PAMSil algorithm)
    - List PAMSilCpp(NumericVector dist, IntegerVector C, IntegerVector medoids, int N, int k){
    - // [[Rcpp::export(.PAMSilCpp)]]

3; Hàm phụ

- miniSW(2) (phần 2: The original Optimum Silhouette algorithm ⇒ phần 2.2: // The Scalable Optimum Silhouette algorithm)
    - double miniSW(NumericVector diC, int m, int k){
    - //miniSW() computes the SW only for the newest unassigned point
- UCT(1) (// 1. The Efficient Optimum Silhouette algorithm)
    - NumericVector UCT(IntegerVector C, NumericVector dist, int N, int k){
    - // UCT(): Compute Unit-Cluster Total distance matrices

4; Hàm chuyển đổi

- UCT2ASW(3) (// 1. The Efficient Optimum Silhouette algorithm)
    - double UCT2ASW(IntegerVector C, NumericVector UCTdist, int N, int k, IntegerVector Nj, NumericVector ai, NumericVector bi, NumericVector si, NumericVector hi,IntegerVector lbi, IntegerVector lsi, IntegerVector lhi){
    - //UCT2ASW: Compute the ASW from a UCT distance matrix
- ASWOSil(4) (phần 2: The original Optimum Silhouette algorithm)
    - double ASWOSil(IntegerVector  C, NumericVector dist, int N, int k, IntegerVector Nj){
    - //ASWOSil(): Compute the ASW (used inside OSil)

5; Hàm update

- UpdateASW(3) (// 1. The Efficient Optimum Silhouette algorithm)
    - double UpdateASW(NumericVector UCTdist, IntegerVector C, NumericVector dist, int N, int i, int j, int k, IntegerVector Nj, NumericVector ai, NumericVector bi, NumericVector si, NumericVector hi,IntegerVector lbi, IntegerVector lsi, IntegerVector lhi){
    - //UpdateASW(): Efficiently compute the ASW in each swap
- UpdateUCT(4) (// 1. The Efficient Optimum Silhouette algorithm)
    - void UpdateUCT(NumericVector UCTdist, NumericVector dist, int N, int k, int i, int j, int li){
    - //UpdateUCT(): Update the UCT after finding the best swap
- UpdateABSH(3) (// 1. The Efficient Optimum Silhouette algorithm)
    - void UpdateABSH(IntegerVector C, NumericVector UCTdist, int N, int k, IntegerVector Nj, NumericVector ai, NumericVector bi, NumericVector si, NumericVector hi,IntegerVector lbi, IntegerVector lsi, IntegerVector lhi){
    - //UpdateABSH(): Update a,b,s,h terms after finding the best swap (k>=3)

6; Hàm tính toán

- BSCalc(2) (// 1. The Efficient Optimum Silhouette algorithm)
    - void BSCalc(NumericVector diC, IntegerVector ldiC, int NdiC, double &b, double &s, int &lb, int &ls){
    - //BSCalc(): Compute the two largest numbers in an array and their indexes given in ldiC (k=3).+
- BSHCalc(3) (// 1. The Efficient Optimum Silhouette algorithm)
    - void BSHCalc(NumericVector diC, IntegerVector ldiC, int NdiC, double &b, double &s, double &h, int &lb, int &ls, int &lh){
    - //BSHCalc(): Compute the three largest numbers in an array and their indexes given in ldiC (k>=3).

7; Hàm update sau steps

- scalOSil_PC_step (phần 2: The original Optimum Silhouette algorithm ⇒ phần 2.2: // The Scalable Optimum Silhouette algorithm)
    - List scalOSil_PC_Step(NumericVector dist, IntegerVector iC, int N, int k){
    - //scalOSil_PC_Step() performs the PC step of scalOSil
- scalOSil_C_step (phần 2: The original Optimum Silhouette algorithm ⇒ phần 2.2: // The Scalable Optimum Silhouette algorithm)
    - IntegerVector scalOSil_C_Step(NumericVector dist, int k, List PC_result, IntegerVector idxPC, IntegerVector idxC, int n1, int n2, int N){
    - //scalOSil_C_Step() performs the C step of scalOSil
- FOSil_PC_Step() (phần 4:The original Fast Optimum Silhouette Algorithm)
    - List FOSil_PC_Step(NumericVector dist, IntegerVector iC, int N, int k){
    - //FOSil_PC_Step() performs the PC step of FOSil
- FOsil_C_Step() (phần 4:The original Fast Optimum Silhouette Algorithm)
    - IntegerVector FOSil_C_Step(NumericVector dist, NumericVector distPC, int k, List PC_result, IntegerVector idxPC, IntegerVector idxC, int n1, int n2, int N){
    - //FOSil_C_Step() performs the C step of FOSil

C; Bắt đầu đọc

0, Revelant functions

- indexing: (i ≥ j luôn luôn z vì được swap)
    
    return ((2*N-1-j)*j >> 1) - 1 +(i-j) = (2*N-1-j)*j*1/2 + (i - 1 - j) 
    
    Ví dụ N=60,i=5,j=7 ⇒ return 286? ⇒ phần tử thứ 286 trong ma trận 60 * 60??
    
    N=3,i=1,j=2⇒
    

1. The Efficient Optimum Silhouette algorithm

- UCT
- UCT2ASW
- UpdateASW
- UpdateUCT
- UpdateABSH
- BSCalc
    - void BSCalc(NumericVector diC, IntegerVector ldiC, int NdiC, double &b, double &s, int &lb, int &ls){
    - //BSCalc(): Compute the two largest numbers in an array and their indexes given in ldiC (k=3).+

2, Can phan biet SW với ASW

- SW: là của 1 thằng trong p thằng
- ASW: là trung bình của p thằng