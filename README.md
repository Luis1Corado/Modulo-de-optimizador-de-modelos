# Modulo-de-optimizador-de-modelos

pip install OptimizadorModelos

Optimizador básico de modelo Wilson , Nrtl  y Uniquac, para sistemas termodinámicos no convexos. 

**Ejemplo de como utilizar el paquete:**

// Importamos el modulo sistema del paquete   
hola  
```python
from OptimizadorModelos import Sistema 
import numpy as np 
```

// Declaramos las variables que necesitara el programa

```python
t = np.array([100, 98.59, 95.09, 91.05, 88.96, 88.26, 87.96, 87.79, 87.66, 87.83, 89.34, 92.3, 97.18])
x = np.array([0, 0.003, 0.0123, 0.0322, 0.0697, 0.139, 0.231, 0.311, 0.412, 0.545, 0.73, 0.878, 1])
y = np.array([0, 0.0544, 0.179, 0.304, 0.365, 0.384, 0.397, 0.406, 0.428, 0.465, 0.567, 0.721, 1])
CoefA = np.array([17.5439, 3166.38, 193])
CoefB = np.array([18.3036, 3816.44, 227.02])
V1 = 218.5
V2 = 56
P = 101.3
q = np.array([2.5129, 1.4])
r = np.array([2.7799, 0.92])
q_prima = np.array([0.89, 1])

``` 

//Creamos el sistema, si no se cuenta con los datos de UNIQUAC se puede crear el sistema de igual forma omitiendo los kwargs** q , qprima y r  
```python
Propanol_Agua = Sistema.sistema(t, x, y, CoefA, CoefB, V1, V2, P, q = q, qprima = q_prima, r = r, Nombre= 'Propanol_Agua')
```
// Resolvemos el sistema  usando la funcion resolver("Limites inferiores","Limites superiores", "cantidad de parametros", "población","iteraciones", size= cantidad de datos que se quieran calcular, modelo= 1, 2,3,4 o Nulo)  
```python
Propanol_Agua.resolver([-1000.0, -1000.0], [2500.0, 2500.0], 2, 30, 150, size = 50, modelo= 3)
```

modelos
- 1 : Modelo de Wilson
- 2 : Modelo NRTL
- 2 : Modelo UNIQUAC
- 4 o nulo : Calcula los parametros para los tres modelos.

Si se quieren los ver los datos tabulados
`Propanol_Agua.resultados`  
Devolvera un Dataframe con los datos del modelo con el que se trabajo 

## UNIDADES CON LA QUE TRABAJA EL PROGRAMA

* t --- Celcius 
* x,y --- fraciones molares
* CoefA y CoefB -- Coeficientes del modelo de Antoine(mmHg y Kelvin). 
Si necesita transformar sus unidades utilice este link https://www.envmodels.com/freetools.php?menu=antoine&lang=en
* Volumen molar -- cc/mol
* p -- kPa

