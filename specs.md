# Especificaciones Técnicas: Replicación de "Majority Illusion"

## PARTE 1: Experimento Sintético (2b)

### 1. Generación de Redes

Se deben generar dos topologías de red distintas para la evaluación:

**A. Redes Heterogéneas (Scale-Free):**

- **Modelo:** Configuration Model.
- **Distribución de Grado:** $p(k) \sim k^{-\alpha}$.
- **Parámetros:** 10,000 nodos; $\alpha \in \{2.1, 2.4, 3.1\}$.
- **Fracción Activa:** $P(x=1) = 0.05$ (5% de la red).

**B. Redes Homogéneas (Erdős-Rényi):**

- **Modelo:** Erdős-Rényi (grafo aleatorio).
- **Parámetros:** 10,000 nodos; grado promedio $\langle k\rangle \in \{2.5, 5.2\}$.
- **Fracción Activa:** Evaluar para $P(x=1) \in \{0.05, 0.10, 0.20\}$.

**Limpieza (Ambos):** Eliminar self-loops y aristas paralelas tras la generación y registrar la degradación del grado promedio post-limpieza.

### 2. Configuración de Atributos (Nodos Activos)

- **Estado Inicial:** Asignar $x=1$ de forma aleatoria a la fracción de nodos requerida.
- **Correlación Grado-Atributo ($\rho_{kx}$):** Se define según la Ec. 2 del paper:
  $\rho_{kx} = \frac{P(x=1)}{\sigma_x \sigma_k} [\langle k\rangle_{x=1} - \langle k\rangle]$
  _(Donde $\langle k\rangle_{x=1}$ es el grado promedio de los nodos activos)._

### 3. Algoritmos de Manipulación

#### A. Attribute Swapping (Variar $\rho_{kx}$)

Para aumentar la correlación $\rho_{kx}$:

1. Elegir un nodo $v_1$ con $x=1$ y un nodo $v_0$ con $x=0$.
2. Intercambiar sus estados si $k_{v_0} > k_{v_1}$.
3. Repetir hasta alcanzar el valor deseado de $\rho_{kx}$. **Obligatorio: Utilizar actualización $O(1)$ para los cálculos en el bucle.**

#### B. Edge Rewiring (Variar Asortatividad $r_{kk}$)

Para cambiar la asortatividad sin alterar la distribución de grados $p(k)$:

1. Elegir dos aristas al azar, $(u, v)$ y $(w, z)$.
2. Intercambiar los extremos para formar $(u, w)$ y $(v, z)$ si el cambio acerca el coeficiente de Pearson ($r_{kk}$) al objetivo. **Obligatorio: Utilizar actualización $O(1)$ para los cálculos en el bucle.**

### 4. Medición de la Ilusión

- **Cálculo de $P_{>1/2}$:** Fracción de nodos donde más de la mitad de sus vecinos son activos ($x=1$).
- **Gráficas Requeridas:** Replicar métricas de las Figuras 2 y 3 del paper original. Eje X: Correlación k-x ($\rho_{kx}$); Eje Y: Fracción de mayoría ($P_{>1/2}$). Separar gráficos por modelo de red.

---

## PARTE 2: Experimento Redes Reales (2c)

### 1. Datos

- **Red 1 (Asortativa):** `data/ca-AstroPh.txt` (Ignorar líneas con '#').
- **Red 2 (Desasortativa):** `data/git_edges.json` y `data/git_target.csv`.
- **Limpieza:** Extraer la mayor componente conectada y asegurar que sean grafos simples no dirigidos.

### 2. Configuración de Atributos

- Evaluar con **dos** fracciones de nodos activos por red para eficiencia de cómputo: $P(x=1) = 0.05$ (5%) y $P(x=1) = 0.20$ (20%).
- Utilizar la misma métrica de correlación $\rho_{kx}$ (Ec. 2).

### 3. Manipulación (REGLA ESTRICTA)

- **NO HACER EDGE REWIRING.** La topología y asortatividad de las redes reales es inmutable.
- Aplicar **únicamente** el algoritmo _Attribute Swapping_ (optimizado $O(1)$) para variar la correlación grado-atributo.

### 4. Medición

- **Gráfica requerida:** Subplots de 1x2 (uno por red). Eje X: $\rho_{kx}$ (de 0.0 a 0.8), Eje Y: $P_{>1/2}$. Mostrar dos curvas (una para 5% y otra para 20%) en cada subgráfico para replicar la estructura central de la Figura 4 del paper.
