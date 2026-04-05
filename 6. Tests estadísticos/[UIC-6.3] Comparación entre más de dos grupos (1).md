# [UIC-6.3] Comparación entre más de dos grupos (1)

## Input

Los resultados siguientes se han obtenido en un estudio de comparación de 4 grupos de 8 individuos. Están en la forma mean ± sd.

- Control: 76.8 ± 3.8

- AP: 38.6 ± 14.9

- Alcohol: 27.5 ± 8.7

- Alcohol+AP: 19.3 ± 5.4

Aplica un análisis one-way ANOVA seguido de un test de Student-Newman-Keuls.

## Output (Gemini 3 Thinking)

Para realizar este análisis, primero calcularemos el ANOVA de una vía para determinar si existen diferencias globales significativas y, posteriormente, aplicaremos el test de **Student–Newman–Keuls (SNK)** para identificar qué grupos específicos difieren entre sí.

### 1. Preparación de los Datos

Tenemos 4 grupos ($k=4$) con 8 individuos cada uno ($n=8$), lo que da un total de $N=32$ observaciones.

| Grupo | Media ($\bar{x}$) | Desviación Típica ($sd$) | $n$ |
| --- | --- | --- | --- |
| **Control** | 76.8 | 3.8 | 8 |
| **AP** | 38.6 | 14.9 | 8 |
| **Alcohol** | 27.5 | 8.7 | 8 |
| **Alcohol+AP** | 19.3 | 5.4 | 8 |

### 2. Análisis de Varianza (ANOVA) de una vía

#### A. Cálculo de las Sumas de Cuadrados (SS)

* **Suma de Cuadrados Dentro de los grupos ($SS_{within}$):**

$$SS_{within} = \sum (n_i - 1) \cdot s_i^2 = 7 \cdot (3.8^2 + 14.9^2 + 8.7^2 + 5.4^2) = 7 \cdot (14.44 + 222.01 + 75.69 + 29.16) = 2389.1$$

* **Media Global ($\bar{x}_{grand}$):** $(76.8 + 38.6 + 27.5 + 19.3) / 4 = 40.55$
* **Suma de Cuadrados Entre grupos ($SS_{between}$):**

$$SS_{between} = n \cdot \sum (\bar{x}_i - \bar{x}_{grand})^2 = 8 \cdot [(36.25)^2 + (-1.95)^2 + (-13.05)^2 + (-21.25)^2] = 15517.84$$

#### B. Tabla ANOVA

| Fuente de Variación | SS | df | MS (Varianza) | F |
| --- | --- | --- | --- | --- |
| **Entre grupos** | 15517.84 | 3 | 5172.61 | **60.62** |
| **Dentro (Error)** | 2389.10 | 28 | 85.33 |  |
| **Total** | 17906.94 | 31 |  |  |

> **Conclusión del ANOVA:** El valor crítico de $F(3, 28)$ para $\alpha = 0.05$ es aproximadamente **2.95**. Como $60.62 > 2.95$, rechazamos la hipótesis nula: **existen diferencias altamente significativas entre los grupos ($p < 0.001$).**

### 3. Test Post-hoc de Student-Newman-Keuls (SNK)

El test SNK es un procedimiento de rangos múltiples. Primero, ordenamos las medias de menor a mayor:

1. **Alcohol+AP:** 19.3
2. **Alcohol:** 27.5
3. **AP:** 38.6
4. **Control:** 76.8

**Error Estándar (SE):**

$$SE = \sqrt{\frac{MS_{within}}{n}} = \sqrt{\frac{85.33}{8}} = \sqrt{10.666} \approx 3.266$$

Calculamos los valores críticos $W_p = q \cdot SE$ usando la tabla de rangos studentizados ($df=28, \alpha=0.05$):

* Para un rango de $p=2$: $q \approx 2.90 \rightarrow W_2 = 2.90 \cdot 3.266 = \mathbf{9.47}$
* Para un rango de $p=3$: $q \approx 3.50 \rightarrow W_3 = 3.50 \cdot 3.266 = \mathbf{11.43}$
* Para un rango de $p=4$: $q \approx 3.86 \rightarrow W_4 = 3.86 \cdot 3.266 = \mathbf{12.61}$

#### Comparaciones:

* **Control vs Alcohol+AP (p=4):** $76.8 - 19.3 = 57.5 > 12.61$ (**Significativo**)
* **Control vs Alcohol (p=3):** $76.8 - 27.5 = 49.3 > 11.43$ (**Significativo**)
* **Control vs AP (p=2):** $76.8 - 38.6 = 38.2 > 9.47$ (**Significativo**)
* **AP vs Alcohol+AP (p=3):** $38.6 - 19.3 = 19.3 > 11.43$ (**Significativo**)
* **AP vs Alcohol (p=2):** $38.6 - 27.5 = 11.1 > 9.47$ (**Significativo**)
* **Alcohol vs Alcohol+AP (p=2):** $27.5 - 19.3 = 8.2 < 9.47$ (**No Significativo**)

### Resumen de Resultados

El análisis muestra que el grupo **Control** tiene valores significativamente más altos que todos los demás. El tratamiento con **AP** reduce los valores, pero sigue siendo significativamente distinto de los grupos que contienen **Alcohol**. Finalmente, no se encontró una diferencia estadística suficiente para separar el efecto de **Alcohol** solo del efecto combinado de **Alcohol+AP**.

¿Te gustaría que graficara estos resultados para visualizar mejor las diferencias entre los grupos?