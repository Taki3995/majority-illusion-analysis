# Especificaciones Técnicas: Replicación de "Majority Illusion" (Sintético)

## 1. Generación de Redes

- **Modelo:** Configuration Model para redes Scale-Free.
- **Distribución de Grado:** p(k) ~ k^-alpha.
- **Parámetros:** N = 10,000 nodos; alpha en {2.1, 2.4, 3.1}.
- **Limpieza:** Eliminar self-loops y aristas paralelas tras la generación.

## 2. Configuración de Atributos (Nodos Activos)

- **Fracción Activa:** P(x=1) = 0.05 (5% de la red).
- **Estado Inicial:** Asignar x=1 de forma aleatoria a 500 nodos.
- **Correlación Grado-Atributo (rho_kx):** Se define según la Ec. 2 del paper:
  rho*kx = [P(x=1) / (sigma_x * sigma_k)] \* [<k>*{x=1} - <k>]
  _Donde <k>\_{x=1} es el grado promedio de los nodos activos._

## 3. Algoritmos de Manipulación

### A. Attribute Swapping (Variar rho_kx)

Para aumentar la correlación rho_kx:

1. Elegir un nodo v1 con x=1 y un nodo v0 con x=0.
2. Intercambiar sus estados si k_v0 > k_v1.
3. Repetir hasta alcanzar el valor deseado de rho_kx.

### B. Edge Rewiring (Variar Asortatividad r_kk)

Para cambiar la asortatividad sin alterar la distribución de grados p(k):

1. Elegir dos aristas al azar, (u, v) y (w, z).
2. Intercambiar los extremos para formar (u, w) y (v, z) si el cambio acerca el coeficiente de Pearson (r_kk) al objetivo.

## 4. Medición de la Ilusión

- **Cálculo de P\_>1/2:** Fracción de nodos donde más de la mitad de sus vecinos son activos (x=1).
- **Gráfica Requerida:** Eje X: Correlación k-x (rho*kx); Eje Y: Fracción de mayoría (P*>1/2).
- **Comparación:** Mostrar curvas para diferentes valores de asortatividad (r_kk) por cada alpha.
