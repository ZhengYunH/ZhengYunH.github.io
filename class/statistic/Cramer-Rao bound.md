# Cramer-Rao bound(CRB)  
## Statment  
### Scalar unbiased case  
Suppose $ \theta $ is an unknown deterministic parameter which is to be estimated from measurements $ x $, distributed according to some probability density function $ f(x;\theta ) $. The variance of any unbiased estimator $ \hat{\theta} $ of $ \theta $ is then bounded by the reciprocal of the Fisher information $ I(\theta) $:
$$ {\mathrm  {var}}({\hat  {\theta }})\geq {\frac  {1}{I(\theta )}}$$  
where the Fisher information $ I(\theta )$ is defined by
$$ I(\theta )={\mathrm  {E}}\left[\left({\frac  {\partial \ell (x;\theta )}{\partial \theta }}\right)^{2}\right]=-{\mathrm  {E}}\left[{\frac  {\partial ^{2}\ell (x;\theta )}{\partial \theta ^{2}}}\right] $$  
and $ \ell (x;\theta )=\log(f(x;\theta )) $ is the natural logarithm of the likelihood function and $ \mathrm {E} $ denotes the expected value (over $ x $).  
The efficiency of an unbiased estimator $ \hat{\theta} $ measures how close this estimator's variance comes to this lower bound; estimator efficiency is defined as  
$$ e({\hat  {\theta }})={\frac  {I(\theta )^{{-1}}}{{{\rm {var}}}({\hat  {\theta }})}} $$
or the minimum possible variance for an · estimator divided by its actual variance. The Cramér–Rao lower bound thus gives
$$ {\displaystyle e({\hat {\theta }})\leq 1.} $$  

### General scalar case  
A more general form of the bound can be obtained by considering an unbiased estimator $ T(X) $ of the parameter $ \theta $. Here, unbiasedness is understood as stating that $ E [ T(X) ]=\psi (\theta ) $. In this case, the bound is given by
$$ {\mathrm  {var}}(T)\geq {\frac  {[\psi '(\theta )]^{2}}{I(\theta )}} $$
where $ \psi '(\theta ) $ is the derivative of $ \psi (\theta ) $(by $ \theta $), and $ I(\theta ) $ is the Fisher information defined above.

## Single-parameter proof  
The following is a proof of the general scalar case of the Cramér–Rao bound described above. Assume that $ T=t(X) $ is an unbiased estimator for the value $ \psi (\theta ) $ (based on the observations $ X $), and so $ {{\rm {E}}}(T)=\psi (\theta ) $. The goal is to prove that, for all $ \theta $ ,$$ {{\rm {var}}}(t(X))\geq {\frac  {[\psi ^{\prime }(\theta )]^{2}}{I(\theta )}}. $$
Let $ X $ be a random variable with probability density function $ f(x; \theta $ ). Here $ T=t(X) $ is a statistic, which is used as an estimator for $  \psi (\theta ) $. Define $ V $ as the score:$$ {\displaystyle {\rm {E}}\left(V\right)=\int f(x;\theta )\left[{\frac {1}{f(x;\theta )}}{\frac {\partial }{\partial \theta }}f(x;\theta )\right]dx={\frac {\partial }{\partial \theta }}\int f(x;\theta )dx=0} $$
where the integral and partial derivative have been interchanged (justified by the second regularity condition).  

If we consider the covariance $ {{\rm {cov}}}(V,T) $ of $ V $ and $ T $ , we have $ {{\rm {cov}}}(V,T)={{\rm {E}}}(VT) $ , because$ {{\rm {E}}}(V)=0 $ . Expanding this expression we have $${\displaystyle {\rm {cov}}(V,T)={\rm {E}}\left(T\cdot \left[{\frac {1}{f(X;\theta )}}{\frac {\partial }{\partial \theta }}f(X;\theta )\right]\right)=\int t(x)\left[{\frac {1}{f(x;\theta )}}{\frac {\partial }{\partial \theta }}f(x;\theta )\right]f(x;\theta )\,dx={\frac {\partial }{\partial \theta }}\left[\int t(x)f(x;\theta )\,dx\right]=\psi ^{\prime }(\theta )}$$
again because the integration and differentiation operations commute (second condition).
The Cauchy–Schwarz inequality shows that
$$ {\sqrt  {{{\rm {var}}}(T){{\rm {var}}}(V)}}\geq \left|{{\rm {cov}}}(V,T)\right|=\left|\psi ^{\prime }(\theta )\right| $$
therefore
$$ 
{\rm var}  (T) \geq \frac{[\psi^\prime(\theta)]^2}{{\rm var} (V)}
=
\frac{[\psi^\prime(\theta)]^2}{I(\theta)}
 $$
which proves the proposition.
