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


-------------------
## Modelling Robots


### Robots:
=================

Un **robot** è un sistema composto da un insieme di componenti che interagiscono tra loro:
- **link:** sono 'le ossa' del robot
- **joint:** sono le 'giunture' tra i link
- **base:** è il punto di ancoraggio del robot
- **end-effector:** è l'elemento finale del robot, che interagisce con l'ambiente  

### I Giunti ( Joints ):
=======================

I **joint** possono essere di due tipi:
- **revolute:** il link può ruotare attorno ad un asse
- **prismatic:** il link può muoversi lungo un asse

Inoltre i vari **link** sono connessi tra loro da joint, che possono essere disposti sia in **serie** che in **parallelo.**  

**Dexterity / Destrezza:** è la capacità di un robot di eseguire un certo tipo di movimento.  
**Stiffness / Durezza:** è la capacità di un robot di resistere ad un certo tipo di forza.  

### I Gradi di Libertà ( Degrees of Freedom ):
=============================================

Un robot può avere più DoF (Degree of Freedom), che sono le possibili dimensioni di movimento che può avere.
A seconda della loro disposizione (serie o parallelo) si possono avere varie configurazioni note, ponendo N = 3DoF:
- **Cartesiano:** N giunti prismatici perpendicolari tra loro (N = 2 o 3) ottima durezza, destrezza ridotta dalla sola presenza di giunti prismatici
- **Cilindrico:** N-1 giunti prismatici perpendicolari tra loro e 1 giunto revoluto (N = 2 o 3) ottima durezza, spazio di lavoro cilindrico
- **Sferico:** N-2 giunti prismatici perpendicolari tra loro e 2 giunti revoluto (N = 3) utilizzando principalmente nelle lavorazioni a controllo numerico
- **SCARA:** 2 giunti revoluto e 1 giunto prismatico (N = 3) alta durezza a carichi verticali, precisione al posizionalmento scende all'aumentare della distanza dal primo giunto
- **Antropomorfo:** 3 giunti revoluto (N = 3) simili alle braccia umane, destrezza massima, la precisione dipende dalla posizione nello spazio di lavoro, di gran lunga il manipolatore più diffuso a livello industriale.

### I Polsi ( Wrist ):
=====================

I polsi sono le giunture che collegano il braccio del robot con la mano (end-effector).  
La configurazione che massimizza la destrezza in questo caso è un polso sferico (3DoF revolute).  


### I Robot Mobili ( Mobile Robots ):
====================================

Possono essere di due tipi:
- **Wheeled Robots:** un corpo rigido ed un sistema di ruote che permette al robot di muoversi rispetto al terreno
- **Legged Robots:** multipli corpi rigidi connessi al corpo centrale attraverso giunti revoluto e tal volte anche prismatici

### I Robot 'Wheeled':
=====================

I **Wheeled Robots** possono essere di tre tipi:
- **Fixed Wheel:** la ruota è fissa e permette sono di andare in linea retta
- **Steerable Wheel:** la ruota può ruotare attorno ad un asse, permettendo di muoversi in qualsiasi direzione
- **Caster Wheel:** la ruota può ruotare attorno ad un asse, come la steerable wheel, ma il suo asse verticale ha un offset rispetto al centro della ruota, ciò le permette di auto-allinearsi alla direzione di movimento del robot

### La Cinematica Dei Robot ( Robot Kinematics ):
================================================

La **cinematica** è la parte della robotica che studia la geometria dei robot e la loro dinamica.
Si divide in tre branche:
- **Forward Kinematics:** studia la relazione tra la posizione e l'orientamento dei giunti e la posizione e l'orientamento dell'end-effector [ $\mathbf{X} = f(\mathbf{q})$ ]
- **Inverse Kinematics:** studia la relazione tra la posizione e l'orientamento dell'end-effector e la posizione e l'orientamento dei giunti [ $\mathbf{q} = f(\mathbf{X})$ ]
- **Diffential Kinematics:** studia la relazione tra la velocità e l'accelerazione dei giunti e la velocità e l'accelerazione dell'end-effector [ $\mathbf{V_X} = f(\mathbf{q}, \mathbf{\dot{q}})$ ]

