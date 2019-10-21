# Report of Project4

张奕朗 16307130242



### Problem 1

##### a.

With **forward algorithm**, we have:
$$
\begin{align}
\mathbb{P}(c_2\mid D_2=0)&=\alpha\mathbb{P}(D_2=0\mid c_2)\sum_{c_1\in\{0,1\}}\mathbb{P}(c_2\mid c_1)\mathbb{P}(c_1)\\
&=\alpha\left<1-\eta,\eta\right>*(\epsilon*0.5+(1-\epsilon)*0.5)\\
&=0.5\alpha\left<1-\eta,\eta\right>\\
Normalization:\\
&0.5\alpha(1-\eta)+0.5\alpha\eta=1\\
&\Rightarrow \alpha=2\\
&\Rightarrow \mathbb{P}(C_2=1\mid D_2=0)=\eta
\end{align}
$$


##### b.

According to **forward-backward algorithm**,
$$
\begin{align}
\mathbb{P}(D_3=1\mid c_2)&=\sum_{c_3\in\{0,1\}}\mathbb{P}(c_3\mid c_2)\mathbb{P}(D_3=1\mid c_3)\mathbb{P}(\mid c_3)\\
&=\left<1-\epsilon,\epsilon\right>*\eta*1+\left<\epsilon,1-\epsilon\right>*(1-\eta)*1\\
&=\left<\epsilon+\eta-2\epsilon\eta,1-\epsilon-\eta+2\epsilon\eta\right>\\
\mathbb{P}(c_2\mid D_2=0,D_3=1)&=\alpha\mathbb{P}(c_2\mid D_2=0)\mathbb{P}(D_3=1\mid c_2)\\
&=0.5\alpha'\left<1-\eta,\eta\right>\times\left<\epsilon+\eta-2\epsilon\eta,1-\epsilon-\eta+2\epsilon\eta\right>\\
&=0.5\alpha'\left<\epsilon+\eta-3\epsilon\eta-\eta^2+2\epsilon\eta^2,\eta-\epsilon\eta-\eta^2+2\epsilon\eta^2\right>\\
Normalization:\\
&\Rightarrow\alpha'=\frac{2}{\epsilon+2\eta-4\epsilon\eta-2\eta^2+4\epsilon\eta^2}\\
&\Rightarrow \mathbb{P}(C_2=1\mid D_2=0,D_3=1)=\frac{\eta-\epsilon\eta-\eta^2+2\epsilon\eta^2}{\epsilon+2\eta-4\epsilon\eta-2\eta^2+4\epsilon\eta^2}
\end{align}
$$


##### c.

- ###### i. 

  Take $\epsilon=0.1,\eta=0.2$ into the fomula above,
  $$
  \begin{align}
  \mathbb{P}(C_2=1\mid D_2=0)&=0.2\\
  \mathbb{P}(C_2=1\mid D_2=0,D_3=1)&\approx0.4157
  \end{align}
  $$

  

- ###### ii.

  The probability of $C_2=1$ has increased after adding the second sensor reading $D_3=1$. The reason for this is that $\mathbb{P}(C_3=1\mid D_3=1)>\mathbb{P}(C_3=0\mid D_3=1)$. In other words, the evidence of $D_3=1$ indicates that $C_3$ are more likely to be 1 than 0, thus increasing the posterior probability of $C_2=1$ with the help of $P(C_2=1\mid C_3=1)$. This is how future evidences influence current probability in smoothing.

  Formally put, 
  $$
  \begin{align}
  \mathbb{P}(C_k\mid D_{2:t})&=\alpha f_{2:k}b_{k+1:t}\\
  &=\frac{1}{\mathbb{P}(D_{2:k})}\mathbb{P}(C_k\mid D_{2:k})\mathbb{P}(D_{k+1:t}\mid C_k)
  \end{align}
  $$
  Specifically for this problem,
  $$
  \mathbb{P}(C_2=1\mid D_2=0,D_3=1)=\mathbb{P}(C_2=1\mid D_2=0)\frac{\mathbb{P}(D_3=1\mid C_2=1)}{\mathbb{P}(D_3=1)}\\
  where\quad \frac{\mathbb{P}(D_3=1\mid C_2=1)}{\mathbb{P}(D_3=1)}>1
  $$
  
- ###### iii.

  Intuitively, I would set $\eta=0.5$ so that no matter what the ture position of a car is, we have the same probability to get all of the observations. Therefore, our observations would have no effect on the probability of car position.

  Formally,
  $$
  \alpha b_{k+1:t}=\frac{\mathbb{P}(D_{k+1:t}\mid C_k)}{\mathbb{P}(D_{2:k})}=1\\
  \frac{\mathbb{P}(D_3=1\mid C_2=1)}{\mathbb{P}(D_3=1)}=1
  $$
  
