# 差分法(difference method)

## 差分式の導出
差分式は関数のテイラー展開(Taylor expansion)より求められる．2階の差分までなら幾何学的にもとめられるが，テイラー展開を用いた方が高次の項や3階以上の微分に対応できる．$x=a$まわりのテイラー展開は次式で表される．
$$
\begin{align}
f(x) &= \sum_{n=0}^{\infty} \frac{f^{(n)}(a)}{n!} (x-a)^n \notag \\
&= f(x) + f^{\prime}(a)(x-a) + \frac{f^{\prime\prime}(a)}{2!}(x-a)^2 + \frac{f^{\prime\prime\prime}(a)}{3!}(x-a)^3 + \cdots \notag \\
&= f(x) + f^{\prime}(a)(x-a) + \frac{f^{\prime\prime}(a)}{2}(x-a)^2 + \frac{f^{\prime\prime\prime}(a)}{6}(x-a)^3 + \cdots \notag
\end{align}
$$
ここで，$u(x - \Delta x), u(x + \Delta x )$のテイラー展開を求めておく．$u$を多変数関数として，3次までの項を考えれば，
$$
\begin{equation}
u(x - \Delta x) = u(x) -\Delta x \frac{\partial u}{\partial x} + \frac{(\Delta x)^2}{2} \frac{\partial ^2 u}{\partial x^2}  + \mathcal{O}((\Delta x)^3) \notag
\end{equation}
$$
$$
\begin{equation}
u(x + \Delta x) = u(x) +\Delta x \frac{\partial u}{\partial x} + \frac{(\Delta x)^2}{2} \frac{\partial ^2 u}{\partial x^2} + \mathcal{O}((\Delta x)^3) \notag
\end{equation}
$$

### 中心差分(centered difference)
中心差分は$u(x-\Delta x)$と$u(x+\Delta x)$のテイラー展開より，1階微分は
$$
\frac{\partial u}{\partial x} \approx \frac{u(x + \Delta x) - u(x - \Delta x)}{2 \Delta x} + \mathcal{O}(\Delta x)^2
$$
2階微分は
$$
\frac{\partial ^2 u}{\partial x^2} \approx \frac{u(x + \Delta x) - 2u(x) + u(x - \Delta x)}{(\Delta x)^2} + \mathcal{O}(\Delta x)
$$

### 前進差分(forward difference)
前進差分は$u(x + \Delta x)$のテイラー展開より，1階微分は
$$
\frac{\partial u}{\partial x} \approx \frac{u(x + \Delta x) - u(x)}{\Delta x} + \mathcal{O}(\Delta x)
$$
2階微分は$u(x + \Delta x)$と$u(x + 2 \Delta x)$のテイラー展開より
$$
\frac{\partial ^2 u}{\partial x^2} \approx \frac{u(x - 2\Delta x) + u(x)}{(\Delta x)^2} + \mathcal{O}(\Delta x)
$$

### 後退差分(backward difference)
後退差分は$u(x - \Delta x)$のテイラー展開より，1階微分は
$$
\frac{\partial u}{\partial x} \approx \frac{u(x) - u(x - \Delta x)}{\Delta x} + \mathcal{O}(\Delta x)
$$
2階微分は$u(x - 2 \Delta x)$と$u(x - \Delta x)$のテイラー展開より
$$
\frac{\partial ^2 u}{\partial x^2} \approx \frac{u(x -2 \Delta x) - 2u(x - \Delta x) + u(x)}{(\Delta x^2)} + \mathcal{O}(\Delta x)
$$

## 精度（誤差）について
精度のオーダーは数値計算の計算コストや物理的な信頼度に影響を与える．誤差を$1/10$に抑えたい場合，差分式の精度が$\mathcal{O} (\Delta x)$であるとき，メッシュサイズを10倍にする必要があるが，$\mathcal{O} (\Delta x)^2$であるとき，メッシュサイズを$\sqrt{10} = 3.16$倍にすればよい．また，数値拡散や数値分散が含まれる現象の場合，低精度の前進差分や後退差分を選ぶと，現象を正確に計算することができない．