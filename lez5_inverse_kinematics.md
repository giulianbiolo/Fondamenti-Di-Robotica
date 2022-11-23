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

Fondamenti Di Robotica - Lezione 5
==================================


**Salto, per rimanere succinto, la parte sulla calibrazione dei parametri DH del robot, per saperne di più leggere la prima sezione del pdf [Inverse Kinematics](https://didatticaonline.unitn.it/dol/pluginfile.php/1677918/mod_resource/content/1/lect7.pdf#page=7).**  


---------------------
## Inverse Kinematics  

Dato un manipolatore la cui cinematica diretta è rappresentabile come:  

$$x_e=k(q)$$  

Il problema della cinematica inversa riguarda trovare la configurazione di parametri di giunti $q$ come funzione della posizione dell'end-effector $x_e$.  

$$q=k^{-1}(x_e)$$  

Il problema è **non-lineare** per cui:  
- Non sempre risolvibile in forma chiusa  
- Potremmo avere più soluzioni  
- Potremmo avere infinite soluzioni ( nel caso di manipolatori ridondanti )  
- Potremmo non avere soluzioni ( nel caso di punti fuori dallo spazio di lavoro )  

Una soluzione a forma chiusa è spesso difficile da trovare e richiede un'intuizione algebrica e geometrica.  


---------------------
## Three link example  

<img style="filter: invert(80%); width: 300px; position:relative; left: 50%; transform: translateX(-50%); -webkit-transform: translateX(-50%); -ms-transform: translateX(-50%);" src="lez5_three_link.svg" />  

Proviamo a risolvere l'equazione di cinematica inversa per questo manipolare per dimostrare che avrà infinite soluzioni.  
Una prima equazione da utilizzare è sicuramente:  
$$ \phi = \phi_1 + \phi_2 + \phi_3 $$  
Dopodichè poniamo $p_W$ l'origine del secondo frame, avremo che:  
$$p_{W_x}=p_x-a_3c_{\phi}=a_1c_1+a_2c_{12}$$  
$$p_{W_y}=p_y-a_3s_{\phi}=a_1s_1+a_2s_{12}$$  
Quindi sommando e ponendo al quadrato le due equazioni otteniamo:  
$$p_{W_x}^2+p_{W_y}^2=a_1^2+a_2^2+2a_1a_2(c_1c_{12}+s_1s_{12})$$  
Ove $c_1c_{12}+s_1s_{12}=\cos(\theta_1-(\theta_1+\theta_2))=c_2$ da cui:  
$$c_2=\frac{p_{W_x}^2+p_{W_x}^2-a_1^2-a_2^2}{2a_1a_2}$$  
Da cui sapendo che $\sin(x)=\pm\sqrt{1-\cos^2(x)}$ possiamo trovare entrambi $\theta_1$ e $\theta_2$ a partire da questa equazione, sapendo che saranno:
$$\theta_1=atan2(s_1,c_1)$$  
$$\theta_2=atan2(s_2,c_2)$$  
Mentre ci troveremo di fronte al problema che:  
$$\theta_3=\phi-\theta_1-\theta_2$$  
Per cui se non fissiamo $\phi$ avremo infinite soluzioni.  


------------------
## Spherical wrist  

<img style="filter: invert(80%); width: 300px; position:relative; left: 50%; transform: translateX(-50%); -webkit-transform: translateX(-50%); -ms-transform: translateX(-50%);" src="lez5_spherical_wrist.svg" />  

In questo caso scegliamo $p_W$ all'intersezione dei 3 giunti del polso, sappiamo che per una posizione del polso data da $p_e$ e dalla matrice di rotazione $R_e$ avremo che:  
$$p_W=p_e-d_6a_e$$  
Per un manipolatore a 3DoF non ridondante possiamo seguire una semplice procedura per ottenere la cinematica inversa.  
L'idea è **dividere la soluzione del braccio da quella dell'end-effector**, trattando l'end-effector come la rotazione che darà l'angolo di approccio, mentre il restante braccio sarà la configurazione di giunti che portano a quel punto, e quindi un semplice 3DoF antropomorfo.  

Quindi la roadmap è:  
- Trovare la posizione del polso $p_W(q_1,q_2,q_3)$  
- Risolvere la cinematica inversa per $(q_1,q_2,q_3)$  
- Usare i valori per trovare $R_3^0(q_1,q_2,q_3)$  
- Trovare $R_3^6(\theta_4, \theta_5, \theta_6)=R_3^{0T}R_e$  
- Risolvere la cinematica inversa per $(\theta_4, \theta_5, \theta_6)$  

**Per vedere l'intera soluzione dettagliata di calcoli riferirsi al pdf moodle [Inverse Kinematics](https://didatticaonline.unitn.it/dol/pluginfile.php/1677918/mod_resource/content/1/lect7.pdf#page=26).**  
