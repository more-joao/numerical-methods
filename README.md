# Numerical Methods
<img src="https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue"> <img src="https://img.shields.io/badge/Numpy-777BB4?style=for-the-badge&logo=numpy&logoColor=white"> <img src="https://img.shields.io/badge/matplotlib-brightgreen?style=for-the-badge"><br>

A repository containing implementations of numerical methods and solutions for relevant exercises.

## Root Finding Methods

### 1. Bisection Method

Given a function $f(x)$,

a. Declare interval $[a,b]$ such that $f(a)f(b) \lt 0$;

b. Declare precision $ϵ \gt 0$;

c. If $|b-a| \lt \epsilon$, $\bar{x} = x$, $\forall x \in [a,b]$;

d. If not, do: $$x_m = \frac{a+b}{2};$$

e. If $f(x_m) = 0$, then $\bar{x} = x_m$;

f. If not: if $f(a)f(x_m) \lt 0$, then $b=x_m$, else do $a=x_m$.

g. Go to c.

````python
# ------------- Python Implementation -------------

import matplotlib.pyplot as plt
import numpy as np

# declare interval
x = np.arange(0, 3, 0.1)

# declare f(x)
def f(x):
  return 3*x - np.e**x

# bisection method
def bisection(interval=list(), epsilon=float()):
  a, b = sorted(interval)
  x = a

  while True:
    if abs(b-a) <= epsilon:
      print(f"|b-a| = {abs(b-a)} <= {epsilon}")
      return x
    else:
      x = (a+b)/2
      if f(x) == 0:
        return x
      else:
        if f(a)*f(x) < 0:
          b = x
        elif f(b)*f(x) < 0:
          a = x

    print(f"I = {[a,b]} | x = {x} | f(a) = {f(a)} | f(b) = {f(b)} | f(x) = {f(x)} | |b-a| = {abs(b-a)}")
# ----------------------------------------------------
````
#### Example

Find roots of $f(x) = 3x - e^x$

Locate roots (if they exist):

`````python
import matplotlib.pyplot as plt
import numpy as np

# declare interval
x = np.arange(0, 3, 0.1)

# example functions
h = lambda x: 3*x
g = lambda x: np.e**x

# plot both functions
plt.figure(figsize=(4,3))
plt.plot(x, h(x))
plt.plot(x, g(x))
plt.grid()
plt.show()
`````
<img width="377" height="274" alt="image" src="https://github.com/user-attachments/assets/db5b0157-c748-4c14-ae3c-9988e6c0065f" />

Apply bisection method: 
````python
import numpy as np

# declare f(x)
def f(x):
  return 3*x - np.e**x

# bisection method
def bisection(interval=list(), epsilon=float()):
  a, b = sorted(interval)
  x = a

  while True:
    if abs(b-a) <= epsilon:
      print(f"|b-a| = {abs(b-a)} <= {epsilon}")
      return x
    else:
      x = (a+b)/2
      if f(x) == 0:
        return x
      else:
        if f(a)*f(x) < 0:
          b = x
        elif f(b)*f(x) < 0:
          a = x

    print(f"I = {[a,b]} | x = {x} | f(a) = {f(a)} | f(b) = {f(b)} | f(x) = {f(x)} | |b-a| = {abs(b-a)}")


# i) find root in [0.0, 1.0]
x = bisection([0.0, 1.0], 0.01)
print(f"x = {x}")

# ii) find root in [1.0, 2.0]
x = bisection([1.0, 2.0], 0.01)
print(f"x = {x}")
````

### 2. False Position Method

Given a function $f(x)$,

a. Declare interval $[a,b]$ such that $f(a)f(b) \lt 0$;

b. Declare precision $ϵ \gt 0$;

c. If $|b-a| \lt \epsilon$, $\bar{x} = x$, $\forall x \in [a,b]$;

d. If not, do: $$x_p = \frac{af(b)-b(f(a))}{f(b)-f(a)};$$

e. If $f(x_p) = 0$, then $\bar{x} = x_p$;

f. If not: if $f(a)f(x_p) \lt 0$, then $b=x_p$, else do $a=x_p$.

g. Go to c.

````python
# # ------------- Python Implementation -------------

import numpy as np

# declare interval
x = np.arange(0, 3, 0.1)

# declare f(x)
def f(x):
  return 3*x - np.e**x

# false position method
def false_position(interval=list(), epsilon=float()):
  a, b = sorted(interval)
  x = a

  while True:
    if abs(b-a) <= epsilon:
      print(f"|b-a| = {abs(b-a)} <= {epsilon}")
      return x
    else:
      x = (a*(f(b)) - b*(f(a)))/(f(b) - f(a))
      if f(x) == 0:
        return x
      else:
        if f(a)*f(x) < 0:
          b = x
        elif f(b)*f(x) < 0:
          a = x

    print(f"I = {[a,b]} | x = {x} | f(a) = {f(a)} | f(b) = {f(b)} | f(x) = {f(x)} | |b-a| = {abs(b-a)}")

# ----------------------------------------------------
````

#### Example

Find roots of $f(x) = \frac{x}{2}-tg(x)$

Locate roots (if they exist):

`````python
import matplotlib.pyplot as plt
import numpy as np

# declare interval
x = np.linspace(-2 * np.pi, 2 * np.pi, 100)

h = lambda x: x/2
g = lambda x: np.tan(x)

# plot both functions
plt.figure(figsize=(4,3))
plt.plot(x, h(x))
plt.plot(x, g(x))
plt.ylim(-5, 5)
plt.grid()
plt.show()
`````
<img width="360" height="274" alt="image" src="https://github.com/user-attachments/assets/69f60865-e67c-48b3-9b67-14894ea3895e" />


> Note: there are some implementation particularities for this example regarding the plotting of np.tg(x), which can be explored at [https://stackoverflow.com/a/54505938].

````python
import numpy as np

# declare f(x)
def f(x):
  return x/2 - np.tan(x)

# false position method
def false_position(interval=list(), epsilon=float()):
  a, b = sorted(interval)
  x = a

  while True:
    if abs(b-a) <= epsilon:
      print(f"|b-a| = {abs(b-a)} <= {epsilon}")
      return x
    else:
      x = (a*(f(b)) - b*(f(a)))/(f(b) - f(a))
      if f(x) == 0:
        return x
      else:
        if f(a)*f(x) < 0:
          b = x
        elif f(b)*f(x) < 0:
          a = x

    print(f"I = {[a,b]} | x = {x} | f(a) = {f(a)} | f(b) = {f(b)} | f(x) = {f(x)} | |b-a| = {abs(b-a)}")


# i) find root in [0.0, 1.0]
x = false_position([0.0, 1.0], 0.01)
print(f"x = {x}")

# ii) find root in [1.0, 2.0]
x = false_position([1.0, 2.0], 0.01)
print(f"x = {x}")
````

### 3. Fixed-point Method

Given a function $f(x)$ and an iterative function $ϕ(x)$ for $f(x)=0$, both such that:

*   $f'(x)$ and $ϕ'(x)$ are continuous;
*   $|ϕ'(x)| \leq M \lt 1$, $∀x \in I=[a,b]$ centered around $\xi$ (root of $f(x)$);
*   $x_0 \in I$, where $x_0$ is an initial approximation of $\bar{x}$.

a. Declare precisions $ϵ_1, ϵ_2 \gt 0$;

b. If $|f(x_0)| \lt \epsilon$, $\bar{x} = x_0$;

c. $k=1$;

d. $x_k = \phi (x_{k-1})$

e. If $|f(x_k)| \lt ϵ_1$ or $|x_k-x_{k-1}| \lt ϵ_2$, then $\bar{x}=x_k$;

f. $k=k+1$. Go back to d.

### 3.A. Newton-Raphson Method

Let $f(x)$ be a function and $\phi (x)$ be an iterative function for $f(x) = 0$, both such that:

* $f(x), f'(x)$ and $f''(x)$ are continuous in an interval $I$, with $\xi \in I$ root of $f(x)=0$;
* $\phi(x)=x - \frac{f(x)}{f'(x)}$;
* $f'(\xi) \neq 0$;
* $x_0 \in I$ is an initial approximation of $\xi$.

a. Declare precisions $ϵ_1, ϵ_2 \gt 0$;

b. If $|f(x_0)| \lt \epsilon_1$, $\bar{x}=x_0$;

c. $k = 1$;

d. Do: $$x_k = x_{k-1}-\frac{f(x_{k-1})}{f'(x_{k-1})}$$

e. If $|f(x_k)| \lt \epsilon_1$ or $|x_k - x_{k-1}| \lt \epsilon_2$, $\bar{x}=x_k$;

f. $k = k + 1$. Go back to d.

### 3.B. Secant Method

Let $f(x)$ be a function and $\phi (x)$ be an iterative function for $f(x) = 0$, both such that:

* Let $I$ be an interval, with $\xi \in I$ root of $f(x)=0$;
* $x_0, x_1 \in I$ are initial approximations of $\xi$.

a. Declare precisions $ϵ_1, ϵ_2 \gt 0$;

b. If $|f(x_0)| \lt \epsilon_1$, $\bar{x}=x_0$;

c. If $|f(x_1)| \lt \epsilon_1$ or $|x_1 - x_0| \lt \epsilon_2$ $\bar{x}=x_1$;

c. $k = 1$;

d. Do: $$x_{k+1} = x_{k}-\frac{f(x_k)}{f(k)-f(x_{k-1})}(x_k-x_{k-1})$$

e. If $|f(x_{k+1})| \lt \epsilon_1$ or $|x_{k+1} - x_k| \lt \epsilon_2$, $\bar{x}=x_{k+1}$;

f. $k = k + 1$. Go back to d.


