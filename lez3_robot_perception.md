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

Fondamenti Di Robotica - Lezione 3
==================================

## Robot Perception  

La percezione è un'attività cognitiva che rende il sistema cosciente di se stesso e del suo ambiente.  

La percezione è un processo che coinvolge la rilevazione, l'interpretazione e l'assimilazione di informazioni provenienti dall'ambiente esterno.  
Per fare ciò si fa uso di vari sensori, che possono essere di diverso tipo:  
- sensori di contatto: permettono di rilevare la presenza di un oggetto e la sua forma  
- videocamera: permettono di studiare l'ambiente circostante attraverso l'analisi di immagini  
- sensori di posizione: permettono di rilevare la posizione di un oggetto rispetto al robot  
- ToF: permettono di rilevare la distanza tra il robot e un oggetto  

[ Potrei fare un riassunto di tutto quel che parla nel pdf ma sono 70 pagine di fuffa ]

-----------------------

## Sensing Devices:

**Encoders:** Dispositivi elettro-meccanici che convertono posizione lineare o angolare in segnali analogici o digitali.  
Alcuni utilizzi sono per esempio nelle ruote di un robot o nei motori di un braccio robotico per rilevare la posizione e la velocità.  

**Heading sensors:** Dispositivi che misurano la direzione di un oggetto, come per esempio magnetometri, IMU, giroscopi, accelerometri, ecc...  

**Position sensors:** Dispositivi che misurano la posizione del robot nello spazio di riferimento, come per esempio GPS (meter range accuracy), dGPS (centimeter range accuracy), ecc...  

**Range Sensors:** Dispositivi che misurano la distanza tra il robot e un oggetto, come per esempio sonar, laser, ToF, ecc...  

[ Potrei riassumere tutto il pdf ma sono 70 pagine di fuffa in cui spiega per filo e per segno la meccanica di funzionamento dei vari sensori con tanto di formule matematiche ]  
