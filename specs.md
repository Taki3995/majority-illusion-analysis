# Especificaciones Técnicas: Experimento 2b (Redes Sintéticas)

## Objetivo

Replicar la "Ilusión de la Mayoría" en redes sintéticas para observar cómo la estructura afecta la percepción local.

## Parámetros de Red

- **Tipo:** Redes de escala libre (Scale-free) generadas con el Configuration Model.
- **Tamaño:** $N = 10,000$ nodos.
- **Exponentes (α):** 2.1, 2.4 y 3.1.
- **Nodos Activos:** Fracción fija $P(x=1) = 0.05$ (5%).

## Algoritmos Requeridos

1. **Attribute Swapping:** Intercambiar estados (activo/inactivo) entre nodos para variar la correlación grado-atributo ($\rho_{kx}$) según la Ec. 2 del paper.
2. **Edge Rewiring:** Ajustar la asortatividad de grado ($r_{kk}$) sin alterar la distribución de grados $p(k)$, siguiendo el procedimiento de Newman.

## Métrica de Éxito

- Calcular $P_{>1/2}$: Fracción de nodos donde más del 50% de sus vecinos son activos ($\phi = 0.5$).
- Generar gráficas de $P_{>1/2}$ vs. $\rho_{kx}$ para distintos valores de $r_{kk}$.
