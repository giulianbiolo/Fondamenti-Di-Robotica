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

Nei casi più semplici possiamo calcolare $T_e^b(q)$ in modo analitico, attraverso alcune considerazioni geometriche. Per esempio nel caso di un manipolatore planare a due link:   

<img style="filter: invert(80%); width: 300px; position:relative; left: 50%; transform: translateX(-50%);" src="lez4_2d_simple_manipulator.svg" />  

Possiamo calcolare $T_e^b(q)$:  
$$ T_e^b(q) = \begin{bmatrix} n_e^b & s_e^b & a_e^b & p_e^b \\ 0 & 0 & 0 & 1 \end{bmatrix} = \begin{bmatrix} 0 & s_{12} & c_{12} & a_1c_1+a_2c_{12} \\ 0 & -c_{12} & s_{12} & a_1s_1+a_2+c_{12} \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} $$  

Ove $s_i=\sin(\theta_i)$, $c_i=\cos(\theta_i)$, $s_{12}=\sin(\theta_1+\theta_2)$, $c_{12}=\cos(\theta_1+\theta_2)$.  

In casi più complessi la derivazione può essere molto più difficile, per cui dobbiamo trovare una soluzione generale al problema.  

Prendendo in considerazione un manipolatore generico di $n+1$ link e $n$ giunti. Attacchiamo ad ogni giunto un frame di riferimento dove la posa del frame $i+1$ sarà determinata da una semplice trasformazione dal frame $i$.  
L'idea è che possiamo ricostruire la trasformazione $T_e^b(q)$ in modo ricorsivo.  

$$T_n^0(q)=A_1^0(q_1)A_2^1(q_2)...A_n^{n-1}(q_n)$$  

Ove $A_i^{i-1}(q_i)$ è una trasformazione omogenea funzione di $q_i$ che porta dal frame $i-1$ al frame $i$.  
Per completare il calcolo dobbiamo considerare anche la trasformazione dalla base al primo link e dall'ultimo link all'end-effector che tipicamente sono costanti:  

$$T_e^b(q)=T_0^bT_n^0(q)T_e^n$$  


## Denavit-Hartenberg Convention  

La convenzione Denavit-Hartenberg è una convenzione per rappresentare i manipolatori in modo da poter calcolare la trasformazione $T_e^b(q)$ in modo semplice ed automatico.  

[ Pagina 10 / 41 ]  
