## Software used  : Python
## IDE : Google Colab

# Completed By
Name : Atul Kumar Dwivedi

Roll Number :11111111

Branch : Electronics and Communication Engineering

Semester : 4

Lab: Signals and Systems (BEC 451)

Date of Completion 30/03/2024

## Sympy
Sympy is a computer algebra module for Python. It allowspython to do algebric calculations. It is used for solving simultaniuousequations, finding factors of a polynomials, differentiation, integration etc. 
We need to import the SymPy module to get symbolic math capabilities using "import sympy" command and We also need to start the pretty-printer to get nicely typeset math using "sympy.init_printing()" command. 



## Laplace Transform
The Laplace transform is given by \
${L[{f(t)}] = \int_0^\infty f(t) e^{-st} d}s $


```python
import sympy
sympy.init_printing()

import matplotlib.pyplot as plt
# Let's define some symbols to work with
t, s = sympy.symbols('t, s')
a = sympy.symbols('a', real=True, positive=True)
#direct evaluation
f = sympy.exp(-a*t)
f
#We can evaluate the integral directly using integrate:
sympy.integrate(f*sympy.exp(-s*t), (t, 0, sympy.oo))

```




$\displaystyle \begin{cases} \frac{1}{s \left(\frac{a}{s} + 1\right)} & \text{for}\: \left|{\arg{\left(s \right)}}\right| \leq \frac{\pi}{2} \\\int\limits_{0}^{\infty} e^{- a t} e^{- s t}\, dt & \text{otherwise} \end{cases}$




```python
import sympy
sympy.init_printing()

import matplotlib.pyplot as plt
# Let's define some symbols to work with
t, s = sympy.symbols('t, s')
a = sympy.symbols('a', real=True, positive=True)
#direct evaluation
f = sympy.exp(-a*t)
f
# using Library function, Sympy provides a function called laplace_transform which does this more efficiently. 
#By default it will return conditions of convergence as well (recall this is an improper integral, with an infinite bound, so it will not always converge).

sympy.laplace_transform(f, t, s)


```




$\displaystyle \left( \frac{1}{a + s}, \  - a, \  \text{True}\right)$



#standard transform table


```python
import sympy
sympy.init_printing()

import matplotlib.pyplot as plt
# Let's define some symbols to work with
omega = sympy.Symbol('omega', real=True)
exp = sympy.exp
sin = sympy.sin
cos = sympy.cos
def L(f):
    return sympy.laplace_transform(f, t, s, noconds=True)
def invL(F):
    return sympy.inverse_laplace_transform(F, s, t)
functions = [1,
         t,
         exp(-a*t),
         t*exp(-a*t),
         t**2*exp(-a*t),
         sin(omega*t),
         cos(omega*t),
         1 - exp(-a*t),
         exp(-a*t)*sin(omega*t),
         exp(-a*t)*cos(omega*t),
         ]


Fs = [L(f) for f in functions]
Fs
```




$\displaystyle \left[ \frac{1}{s}, \  \frac{1}{s^{2}}, \  \frac{1}{a + s}, \  \frac{1}{\left(a + s\right)^{2}}, \  \frac{2}{\left(a + s\right)^{3}}, \  \frac{\omega}{\omega^{2} + s^{2}}, \  \frac{s}{\omega^{2} + s^{2}}, \  \frac{a}{s \left(a + s\right)}, \  \frac{\omega}{\omega^{2} + \left(a + s\right)^{2}}, \  \frac{a + s}{\omega^{2} + \left(a + s\right)^{2}}\right]$



We can make a pretty good representation of the table with a little help from pandas


```python
from pandas import DataFrame
def makelatex(args):
    return ["$${}$$".format(sympy.latex(a)) for a in args]

DataFrame(list(zip(makelatex(functions), makelatex(Fs))))
```





  <div id="df-b75b39b2-1e13-416f-a9d7-fb06a573102e">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$$1$$</td>
      <td>$$\frac{1}{s}$$</td>
    </tr>
    <tr>
      <th>1</th>
      <td>$$t$$</td>
      <td>$$\frac{1}{s^{2}}$$</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$$e^{- a t}$$</td>
      <td>$$\frac{1}{a + s}$$</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$$t e^{- a t}$$</td>
      <td>$$\frac{1}{\left(a + s\right)^{2}}$$</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$$t^{2} e^{- a t}$$</td>
      <td>$$\frac{2}{\left(a + s\right)^{3}}$$</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$$\sin{\left(\omega t \right)}$$</td>
      <td>$$\frac{\omega}{\omega^{2} + s^{2}}$$</td>
    </tr>
    <tr>
      <th>6</th>
      <td>$$\cos{\left(\omega t \right)}$$</td>
      <td>$$\frac{s}{\omega^{2} + s^{2}}$$</td>
    </tr>
    <tr>
      <th>7</th>
      <td>$$1 - e^{- a t}$$</td>
      <td>$$\frac{a}{s \left(a + s\right)}$$</td>
    </tr>
    <tr>
      <th>8</th>
      <td>$$e^{- a t} \sin{\left(\omega t \right)}$$</td>
      <td>$$\frac{\omega}{\omega^{2} + \left(a + s\right...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>$$e^{- a t} \cos{\left(\omega t \right)}$$</td>
      <td>$$\frac{a + s}{\omega^{2} + \left(a + s\right)...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b75b39b2-1e13-416f-a9d7-fb06a573102e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b75b39b2-1e13-416f-a9d7-fb06a573102e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b75b39b2-1e13-416f-a9d7-fb06a573102e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




# Reference 
https://github.com/alchemyst/Dynamics-and-Control/blob/master/1_Dynamics/3_Linear_systems/Laplace%20transforms.ipynb


```python

```
