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

Fondamenti Di Robotica - Lezione 4
==================================

## Direct Kinematics  

Ricordiamo un po' di definizioni fondamentali:  
- Un manipolatore consiste di una serie di corpi rigidi chiamati **link** collegati tra loro da **joints** ( giunti ).  
- I **joints** sono di due tipi:
  - **revolute**
  - **prismatic**
- I giunti prismatici si rappresentano graficamente con dei parallelepipedi, mentre i giunti revolute con dei cilindri.  

Dato un frame di riferimento $O_b-x_by_bz_b$ attaccato alla base ed un frame di riferimento $O_e-x_ey_ez_e$ attaccato all'end-effector, la posa dell'end-effector è data dalla matrice di trasformazione omogenea $T_e^b(q)$, dove $q$ è il vettore n-dimensionale di valori dei giunti.  

$$T_e^b(q) = \begin{bmatrix} R_e^b(q) & p_e^b(q) \\ 0 & 1 \end{bmatrix}= \begin{bmatrix} n_e^b(q) & s_e^b(q) & a_e^b(q) & p_e^b(q) \\ 0 & 0 & 0 & 1 \end{bmatrix}$$  

Dove $n_e,s_e,a_e$ sono i vettori unitari associati all'end-effector e sono scelti basandosi sulla sua geometria.  
Per esempio se l'end-effector è un gripper avremo che $a_e$ è scelto in base alla direzione di approccio, $s_e$ in base alla direzione di scorrimento del gripper, $n_e$ è ortogonale agli altri due in modo che il frame $(n_e,s_e,a_e)$ sia destrorso.  

Tutti gli elementi della matrice sono funzioni dei valori dei giunti, quindi $T_e^b(q)$ è una funzione di $q$.  

[ Pagina 7 / 41 ]  
