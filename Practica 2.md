1. Un sistema operativo mantiene 5 instancias de un recurso almacenadas en una cola.
Además, existen P procesos que necesitan usar una instancia del recurso. Para eso, deben
sacar la instancia de la cola antes de usarla. Una vez usada, la instancia debe ser encolada
nuevamente.
```ada
sem mutex= 1;
sem accesoCola= 1;
queue recurso[5]

Process Proceso [id: 0..p-1]}
recurso r;
P(mutex)
  P(accesoCola);
     r= recurso.poop();
  v(accesoCola);

// Uso del recurso

  P(accesoCola);
    recurso.push(r);
  V(accesoCola);
V(mutex);
}
```
2. Existen N personas que deben ser chequeadas por un detector de metales antes de poder
ingresar al avión.
a. Analice el problema y defina qué procesos, recursos y semáforos serán
necesarios/convenientes, además de las posibles sincronizaciones requeridas para
resolver el problema.
```ada
sem mutex= 1;
process Detector[id:0..N-1]{
 P(mutex);
  //Usar detector
V(mutex);
}
```
b. Implemente una solución que modele el acceso de las personas a un detector (es decir,
si el detector está libre la persona lo puede utilizar; en caso contrario, debe esperar).
```ada
sem mutex= 1;
queue espera[N] =([N]0)
boolean libre= true;
process Detector[id:0..N-1){

P(mutex)
 if(libre){
   libre= false;
   V(mutex)
{
 else{
  espera.push(id);
  V(mutex)
  P(accesoDeector);
}

//Usar detector

P(mutex)
if(empty(espera){
  libre= true;
}else{
 V(accesoDetector);
}
V(mutex); 
}
```

c. Modifique su solución para el caso que haya tres detectores.
```ada
sem mutex= 3;
process Detector[id:0..N-1]{
 P(mutex);
  //Usar detector
V(mutex);
}
```
3. Un sistema de control cuenta con 4 procesos que realizan chequeos en forma
colaborativa. Para ello, reciben el historial de fallos del día anterior (por simplicidad, de
tamaño N). De cada fallo, se conoce su número de identificación (ID) y su nivel de
gravedad (0=bajo, 1=intermedio, 2=alto, 3=crítico). Para cada item realice una solución
adecuada a lo pedido:
a. Se debe imprimir en pantalla los ID de todos los errores críticos (no importa el
orden).
```ada
sem mutex= 1;
queue fallos[N];
int cant= 0;
process Controlador[id:0..3]{
Fallo f;
int nivel;
P(mutex);
  while (cant < N) {
    f= fallos.pop();
    cant ++;
    V(mutex);
    nivel =f.getNivel();
    if(nivel == 3= {
      print(f.getID);
    }
  P(mutex)
}
V(mutex)
}
```
b. Se debe calcular la cantidad de fallos por nivel de gravedad, debiendo quedar los
resultados en un vector global.

c. Ídem b) pero cada proceso debe ocuparse de contar los fallos de un nivel de gravedad
determinado.



