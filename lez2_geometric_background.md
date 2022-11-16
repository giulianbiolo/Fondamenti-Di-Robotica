<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [['$','$'], ['\\(','\\)']],
      processEscapes: true},
      jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"],
      extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"],
      TeX: {
      extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
      equationNumbers: {
      autoNumber: "AMS"
      }
    }
  });
</script>

Fondamenti Di Robotica - Lezione 1
==================================

## Geometric Understanding

### Matrici Di Rotazione ( Rotation Matrices ):
==============================================

Le matrici di rotazione sono matrici $N \times N$ che rappresentano una rotazione di un angolo $\theta$ attorno ad un asse $\vec{u}$.  

Vediamo ora le matrici di rotazione per $N=3$ più comuni, ossia quelle attorno agli assi $x,y,z$.  

#### Matrice di rotazione attorno all'asse $x$:

$$R_x(\theta) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos(\theta) & -\sin(\theta) \\ 0 & \sin(\theta) & \cos(\theta) \end{bmatrix}$$

#### Matrice di rotazione attorno all'asse $y$:

$$R_y(\theta) = \begin{bmatrix} \cos(\theta) & 0 & \sin(\theta) \\ 0 & 1 & 0 \\ -\sin(\theta) & 0 & \cos(\theta) \end{bmatrix}$$

#### Matrice di rotazione attorno all'asse $z$:

$$R_z(\theta) = \begin{bmatrix} \cos(\theta) & -\sin(\theta) & 0 \\ \sin(\theta) & \cos(\theta) & 0 \\ 0 & 0 & 1 \end{bmatrix}$$


Le matrici di rotazione godono di alcune proprietà interessanti:
- sono ortogonali, cioè $R^T = R^{-1}$
- sono deteminanti unitari, cioè $det(R) = 1$
- $R^{-1}(\theta) = R(-\theta)$ in quanto l'inversa di una matrice di rotazione è la matrice di rotazione che ruota dell'angolo opposto, annullando la rotazione iniziale.  

I robot vengono modellati come una collezione di corpi rigidi connessi tra loro da giunti rappresentati da matrici di roto-traslazione.  

