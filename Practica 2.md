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




