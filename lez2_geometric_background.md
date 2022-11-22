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

Fondamenti Di Robotica - Lezione 2
==================================

## Geometric Understanding

### Matrici Di Rotazione ( Rotation Matrices ):
==============================================

Le matrici di rotazione sono matrici $N \times N$ che rappresentano una rotazione di un angolo $\theta$ attorno ad un asse $\vec{u}$.  

Vediamo ora le matrici di rotazione per $N=3$ più comuni, ossia quelle attorno agli assi $x,y,z$.  

$$R_x(\theta) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos(\theta) & -\sin(\theta) \\ 0 & \sin(\theta) & \cos(\theta) \end{bmatrix}$$

$$R_y(\theta) = \begin{bmatrix} \cos(\theta) & 0 & \sin(\theta) \\ 0 & 1 & 0 \\ -\sin(\theta) & 0 & \cos(\theta) \end{bmatrix}$$

$$R_z(\theta) = \begin{bmatrix} \cos(\theta) & -\sin(\theta) & 0 \\ \sin(\theta) & \cos(\theta) & 0 \\ 0 & 0 & 1 \end{bmatrix}$$


Le matrici di rotazione godono di alcune proprietà interessanti:
- sono ortogonali, cioè $R^T = R^{-1}$
- sono deteminanti unitari, cioè $det(R) = 1$
- $R^{-1}(\theta) = R(-\theta)$ in quanto l'inversa di una matrice di rotazione è la matrice di rotazione che ruota dell'angolo opposto, annullando la rotazione iniziale.  

I robot vengono modellati come una collezione di corpi rigidi connessi tra loro da giunti rappresentati da matrici di roto-traslazione.  

### Composizione di matrici di rotazione:
=========================================

Presi 3 frame di riferimento $O-x_1y_1z_1$, $O-x_2y_2z_2$ e $O-x_3y_3z_3$ consideriamo un punto nei tre sistemi di riferimento.  
Il punto rispetterà le seguenti equazioni:  

$$p^1=R^1_2p^2$$  
$$p^0=R^0_1p^1$$  
$$p^0=R^0_2p^2=R^0_1R^1_2p^2$$  

Si può infatti dimostrare che generalmente vale:  

$$R^i_j=(R^j_i)^{-1}=(R^j_i)^T$$  


### Parametrizzazioni delle rotazioni:
======================================

#### Angoli di Eulero (XYZ):

I tre angoli di Eulero rappresentano la rotazione di un punto attorno agli assi $x,y,z$ rispettivamente.  
Le rotazioni avvengono rispetto all'asse **corrente** e non rispetto all'asse fissato del sistema di riferimento iniziale.  

#### Rappresentazione Aeronautica (RPY):

Si tratta dei famosi angoli di roll, pitch e yaw.  
Sono rotazioni rispetto agli assi $x,y,z$ ma
a differenza del sistema di eulero, la rotazione avviene rispetto all'asse **fisso** del sistema di riferimento iniziale.  

#### Asse e angolo:

Questa rappresentazione si avvale del fatto che per rappresentare qualsiasi rotazione è sufficiente conoscere l'asse (vettore unitario) e l'angolo di rotazione rispetto a tale asse.  
Purtroppo con questo metodo la matrice di rotazione non sarà univoca e quindi tale rappresentazione non è invertibile.  

#### Quaternioni:

Risolviamo il problema della non univocità e non invertibilità della rappresentazione asse/angolo attraverso l'utilizzo dei quaternioni.  
Un quaternione $Q=(\eta, \epsilon)$ è definito da 4 parametri:  
- un parametro scalare $\eta=\cos{\frac{\theta}{2}}$  
- un vettore immaginario $\epsilon=\begin{bmatrix} \epsilon_x \\ \epsilon_y \\ \epsilon_z \end{bmatrix}=\sin{\frac{\theta}{2}}\cdot k$ ove k è un vettore unitario.  

I 4 parametri rispettano la seguente relazione:  
$$\eta^2+\epsilon_x^2+\epsilon_y^2+\epsilon_z^2=1$$  

### RotoTraslazioni:
====================

Diciamo di voler esprimere un punto nello spazio in un sistema di riferimento differente. In tal caso i due sistemi di riferimento potranno essere non solo ruotati tra loro ma anche traslati.  

$$p^0=o^0_1+R^0_1p^1$$

$$p^1=-R^1_0o^0_1+R^1_0p^0$$

Questa notazione diventa velocemente tediosa per cui rappresenteremo in modo più compatto le rototraslazioni creando una **rappresentazione omogenea**  $\tilde{p}$ di $p$ appendendo un $1$ al vettore.  

$$\tilde{p}=\begin{bmatrix}p\\1\end{bmatrix}$$  

Possiamo quindi creare la seguente matrice $4\cdot 4$:
$$A^0_1=\begin{bmatrix}R^0_1 & o^0_1\\0^T & 1\end{bmatrix}$$  
che viene chiamata **matrice di trasformazione omogenea.**  
$$\tilde{p}^0=A^0_1\tilde{p}^1$$  
A differenza delle matrici di rotazione, le trasformazioni omogenee non sono ortogonali per cui:  
$$A^{-1}\neq A^T$$  
Concludendo possiamo dire che:  
$$\tilde{p}^0=A^0_1A^1_2\dots A^{n-1}_{n}\tilde{p}^n$$  
