# [UIC-6.4] Comparación entre más de dos grupos (2)

## Input

En el fichero Excel adjunto se han recogido los resultados de un estudio de comparación de 4 grupos.

En la primera columna (id) hay un identificador de los participantes en el estudio.

En la segunda columna (values) están los resultados de las mediciones realizadas sobre cada uno de los participantes.

En la tercera columna (group) está el grupo al que pertenece cada participante.

Aplica un test estadístico para ver si las diferencias entre los grupos son significativas.

## Output (Gemini 3 Thinking)

```python
import pandas as pd
import scipy.stats as stats
import statsmodels.api as sm
from statsmodels.formula.api import ols
import seaborn as sns
import matplotlib.pyplot as plt

# Load the data
df = pd.read_csv('[UIC-6.5] Data.xlsx - Sheet1.csv')

# Check groups
groups = df['group'].unique()
print(f"Groups: {groups}")

# Descriptive statistics
stats_desc = df.groupby('group')['values'].describe()
print(stats_desc)

# Check for normality (Shapiro-Wilk)
normality_results = {}
for group in groups:
    subset = df[df['group'] == group]['values']
    shapiro_test = stats.shapiro(subset)
    normality_results[group] = {'W': shapiro_test.statistic, 'p-value': shapiro_test.pvalue}

# Check for homogeneity of variance (Levene's test)
levene_test = stats.levene(*[df[df['group'] == group]['values'] for group in groups])

print("\nNormality results:", normality_results)
print("Levene's test result:", levene_test)

# Perform ANOVA or Kruskal-Wallis
# Based on the results of the tests above, I will choose.
# Let's assume ANOVA for a moment to see if it works, or check the p-values first.

```

```text
Groups: ['Control' 'AP' 'Alcohol' 'Alcohol+AP']
            count       mean       std        min        25%        50%        75%        max
group                                                                                        
AP            8.0  30.272142  9.272950  10.829298  27.010424  32.722512  35.415456  39.953104
Alcohol       8.0  29.192916  8.197116  14.481480  25.021507  28.648208  35.332463  40.507913
Alcohol+AP    8.0  17.625788  2.942610  12.878162  15.915416  17.429447  19.300196  21.826159
Control       8.0  77.001181  2.238066  73.453555  75.780728  77.737686  78.422008  79.567909

Normality results: {'Control': {'W': 0.8994386998593198, 'p-value': 0.2856133776563966}, 'AP': {'W': 0.8828499386668027, 'p-value': 0.2004773599451397}, 'Alcohol': {'W': 0.9635646314227387, 'p-value': 0.8432897601803054}, 'Alcohol+AP': {'W': 0.9660640515613994, 'p-value': 0.8654608260009207}}
Levene's test result: LeveneResult(statistic=2.6402432852563216, pvalue=0.06892348989464883)

```

```python
# One-way ANOVA
anova_model = ols('values ~ group', data=df).fit()
anova_table = sm.stats.anova_lm(anova_model, typ=2)
print("ANOVA results:\n", anova_table)

# If significant, post-hoc Tukey
from statsmodels.stats.multicomp import pairwise_tukeyhsd

tukey = pairwise_tukeyhsd(endog=df['values'], groups=df['group'], alpha=0.05)
print("\nTukey HSD results:\n", tukey)

# Plotting the results
plt.figure(figsize=(10, 6))
sns.boxplot(x='group', y='values', data=df, palette="Set2")
sns.stripplot(x='group', y='values', data=df, color=".3", alpha=0.5)
plt.title('Resultados por Grupo')
plt.xlabel('Grupo')
plt.ylabel('Mediciones (values)')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.savefig('boxplot_results.png')
plt.show()

```

```text
ANOVA results:
                 sum_sq    df           F        PR(>F)
group     16579.128022   3.0  132.488721  1.200102e-16
Residual   1167.937370  28.0         NaN           NaN

Tukey HSD results:
      Multiple Comparison of Means - Tukey HSD, FWER=0.05     
=============================================================
  group1     group2   meandiff p-adj   lower    upper  reject
-------------------------------------------------------------
        AP    Alcohol  -1.0792 0.9869  -9.8961  7.7376  False
        AP Alcohol+AP -12.6464 0.0028 -21.4632 -3.8295   True
        AP    Control   46.729    0.0  37.9122 55.5459   True
   Alcohol Alcohol+AP -11.5671 0.0066  -20.384 -2.7503   True
   Alcohol    Control  47.8083    0.0  38.9914 56.6251   True
Alcohol+AP    Control  59.3754    0.0  50.5586 68.1922   True
-------------------------------------------------------------
has vm saved

```

Tras analizar los datos del fichero, he realizado un estudio estadístico completo para determinar si existen diferencias significativas entre los cuatro grupos (**Control, AP, Alcohol y Alcohol+AP**).

#### 1. Verificación de Supuestos

Antes de aplicar el test, se comprobaron las condiciones necesarias:

* **Normalidad:** Mediante el test de Shapiro-Wilk, se confirmó que los datos de cada grupo siguen una distribución normal ($p > 0.05$).
* **Homocedasticidad:** El test de Levene mostró que las varianzas son suficientemente homogéneas entre los grupos ($p = 0.0689$).

#### 2. Test Estadístico: ANOVA de un factor

Dado que se cumplen los supuestos, se aplicó un **ANOVA de un factor**. Los resultados indican que **existen diferencias altamente significativas** entre los grupos:

* **F-statistic:** $132.49$
* **p-valor:** $1.20 \times 10^{-16}$ (prácticamente cero)

Al ser el p-valor mucho menor que 0.05, rechazamos la hipótesis nula de que todos los grupos son iguales.

#### 3. Comparaciones Múltiples (Post-hoc Tukey)

Para identificar qué grupos específicos son diferentes entre sí, se realizó un test de **Tukey HSD**:

| Comparación | Diferencia de Medias | p-adj | ¿Es significativo? |
| --- | --- | --- | --- |
| **Control vs. Todos los demás** | ~47 a 59 unidades | < 0.001 | **Sí** |
| **AP vs. Alcohol** | -1.08 | 0.9869 | **No** |
| **Alcohol+AP vs. AP** | -12.65 | 0.0028 | **Sí** |
| **Alcohol+AP vs. Alcohol** | -11.57 | 0.0066 | **Sí** |

#### Visualización de los Resultados

![](https://raw.githubusercontent.com/lab30041954/Aplicaciones_IA/blob/main/6.%20Tests%20estadísticos/%5BUIC-6.4%5D%20Figure.png)

#### Conclusiones

1. El grupo **Control** presenta valores significativamente más altos que cualquier otro grupo.
2. No hay una diferencia estadística real entre aplicar solo **AP** o solo **Alcohol**.
3. La combinación **Alcohol+AP** produce los valores más bajos del estudio, siendo significativamente distinta de todos los demás grupos, lo que sugiere un efecto aditivo o sinérgico entre ambos factores.

¿Te gustaría que realice algún análisis adicional, como un gráfico de barras con el error estándar o profundizar en algún grupo específico?