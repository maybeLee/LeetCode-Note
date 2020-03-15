## 279 Perfect Squares

### *Description*

```
Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:

Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
Example 2:

Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```



### *My Solution*

这种题目想到就是用递归或者动态规划来实现会比较好。

递归的方法，从1到最大的square数一个一个试，把减去的再递归，或者用stack会更好一点

或者能想到一种数学方法......

递归结果如下：

```java
class Solution {
    public int numSquares(int n){
        if(n==0){
            return 0;
        }
        int i = 1;
        int minCount = 1000;
        while(i*i <= n){
            int count = 1 + numSquares(n-i*i);
            minCount = Math.min(count, minCount);
            i++;
        }
        return minCount;
    }
}
```



#### *Result*

理所当然的TLE.....



### *My Solution II*

用动态规划的方法，对于求n 的数，我转而列出n之前所有数的最少square数量和，然后对第n个数，就是比较n-1, n-4, n-9等等的匹配规则

```java
class Solution {
    public int numSquares(int n){
        //Solution II Dynamic Programming
        int[] dp = new int[n];
        dp[0] = 1;
        for(int i = 1; i < n; i++){
            int j = 1;
            dp[i] = 1000;
            while(j*j<=i+1){
                if(j*j == i+1){
                    dp[i] = 1;
                    break;
                }
                dp[i] = Math.min(dp[i], 1 + dp[i-j*j]);
                j++;
            }
        }
        return dp[n-1];
    }
}
```



#### *Result*

Runtime: 33 ms, faster than 56.41% of Java online submissions for Perfect Squares.

Memory Usage: 38.7 MB, less than 13.89% of Java online submissions for Perfect Squares.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312673498/) | 33 ms   | 38.7 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312673484/) | 34 ms   | 38.6 MB | java     |
| 2 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/312673210/) | 34 ms   | 38.7 MB | java     |

内存确实比较搞，毕竟多用了一个n长度的数组。



### *Crazy Solution: Mathematics (Lagrange's four-square theorem)*

这个方法真的神了，运用的是拉格朗日的一个定理：Lagrange's four-square theorem (中文名不太清楚)

这个定理的意思是：给一个整数，就一定能够用四个平方数的和来表示

> The theorem appears in the *[Arithmetica](http://en.wikipedia.org/wiki/Arithmetica)* of [Diophantus](http://en.wikipedia.org/wiki/Diophantus), translated into Latin by [Bachet](http://en.wikipedia.org/wiki/Claude_Gaspard_Bachet_de_Méziriac) in 1621. It states that every [positive](http://en.wikipedia.org/wiki/Negative_and_positive_numbers) [integer](http://en.wikipedia.org/wiki/Integer) can be expressed as the sum of four squares of integers. For example,
>
> $3 = 1^2 + 1^2 + 1^2 + 0^2$
>
> $31 = 5^2 + 2^2 + 1^2 + 1^2$
>
> $310 = 17^2 + 4^2 + 2^2 + 1^2$

在这个基础上[Adrien-Marie Legendre](http://en.wikipedia.org/wiki/Adrien-Marie_Legendre)提出了一个新的定理，但是他的这个定理没有证完，所以只能说是一个猜想？如下：

如果一个数不能够用$4^k(8m+7)$的形式表示，那么这个数可以用三个数的平方和表示

> [Adrien-Marie Legendre](http://en.wikipedia.org/wiki/Adrien-Marie_Legendre) improved on the theorem in 1798 by stating that a positive integer can be expressed as the sum of three squares [if and only if](http://en.wikipedia.org/wiki/If_and_only_if) it is not of the form $4^k(8m + 7)$. His proof was incomplete, leaving a gap which was later filled by [Carl Friedrich Gauss](http://en.wikipedia.org/wiki/Carl_Friedrich_Gauss).



根据Legendre的猜想，我们可以对这个数首先判断它是不是$4^k(8m+7)$的形式：

a. 如果是的话，可以直接把$4^k$丢掉，因为决定平方和数量的是括号里面的内容，如果是m=0（7）的话，是四个数的平方和，如果$m\neq0$的话，首先不可能只有三个平方数的和，其次根据拉格朗日的定理，最多也只需要四个平方数来组成目标数据，因此，我们可以assert：如果一个数满足$4^k(8m+7)$的形式，那么其最少由四个非零的平方和数相加得到。

b. 如果并不满足上述形式，那么就说明这个数最少可以由三个平方和的数组成，不妨进行分类讨论，可能出现的结果是，该数由：1）1个数的平方和组成；2）2个数的平方和组成；3）三个数的平方和组成。可以通过在目标数内进行平方数搜寻来实现划分，遍历所有平方小于目标数n的数，假设为$a^2$，那么可以找到$b^2=int(\sqrt{n-a^2})$，且满足$a^2+b^2\leq n$。如果$a^2+b^2=n$那么表示n可以由两个数的平方和组成，如果a和b中有一个是0，就表明n可以仅仅由一个数的平方和组成。相反，如果所有的a遍历完了之后，都不能找到一对a,b满足$a^2+b^2=n$那么表明，这个数对少也必须由三个数的平方和组成



下面是代码：

```java
class Solution {
    public int numSquares(int n){       
        // Solution III Mathematics
        while (n % 4 == 0) n /= 4;
        if (n % 8 == 7) return 4;
        for (int a = 0; a * a <= n; a++) {
            int b = (int) Math.sqrt(n - a * a);
            if (a * a + b * b == n) return a == 0 ? 1 : 2;
        }
        
        return 3;
    }
}
```



#### *Result*

Runtime: 1 ms, faster than 99.93% of Java online submissions for Perfect Squares.

Memory Usage: 36.3 MB, less than 13.89% of Java online submissions for Perfect Squares.

| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312681000/) | 1 ms    | 36.3 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312680969/) | 1 ms    | 36.9 MB | java     |
| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/312680915/) | 1 ms    | 36.9 MB | java     |

runtime真的神了........

内存感觉是LeetCode系统的问题......