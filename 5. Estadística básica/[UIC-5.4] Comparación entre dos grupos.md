# [UIC-5.4] Comparación entre dos grupos 

## Input

El archivo Excel adjunto contiene datos de un estudio de odontología. 
La columna "Paciente" contiene un ID para cada participante en el estudio. 
Hay dos grupos de pacientes, y la pertenencia a uno u otro grupo se indica en la columna "Implante".
Las columnas "CBCT_neck_0" y "CBCT_neck_1" contienen valores de la medida "CBCT Neck" en dos tiempos: el día de la operación y al cabo de cuatro meses.
Haz un test estadístico para verificar si la diferencia entre los dos grupos es significativa.

## Output (Gemini 3 Thinking)

```python
import pandas as pd
from scipy import stats
import matplotlib.pyplot as plt
import seaborn as sns

# Load the data
df = pd.read_csv('[UIC-6.1] Data.xlsx - Sheet 1.csv')

# Drop rows with missing values in the relevant columns
df_clean = df.dropna(subset=['CBCT_neck_0', 'CBCT_neck_1']).copy()

# Calculate the change (Difference)
df_clean['Difference'] = df_clean['CBCT_neck_1'] - df_clean['CBCT_neck_0']

# Group data by 'Implante'
group_v3 = df_clean[df_clean['Implante'] == 'V3']['Difference']
group_c1 = df_clean[df_clean['Implante'] == 'C1']['Difference']

# Check for normality (Shapiro-Wilk)
shapiro_v3 = stats.shapiro(group_v3)
shapiro_c1 = stats.shapiro(group_c1)

# Check for homogeneity of variances (Levene's test)
levene_test = stats.levene(group_v3, group_c1)

# Summary statistics
summary = df_clean.groupby('Implante')['Difference'].agg(['mean', 'std', 'count', 'median'])

# Perform the statistical test
# If normal and equal variances -> t-test
# If not normal -> Mann-Whitney U
if shapiro_v3.pvalue > 0.05 and shapiro_c1.pvalue > 0.05:
    test_name = "t-test independiente"
    stat, p_val = stats.ttest_ind(group_v3, group_c1, equal_var=(levene_test.pvalue > 0.05))
else:
    test_name = "Mann-Whitney U"
    stat, p_val = stats.mannwhitneyu(group_v3, group_c1, alternative='two-sided')

# Visualization
plt.figure(figsize=(8, 6))
sns.boxplot(x='Implante', y='Difference', data=df_clean)
plt.title('Comparación de la Diferencia CBCT Neck (4 meses - Inicial)')
plt.ylabel('Diferencia (mm)')
plt.savefig('comparison_plot.png')

print(f"Summary Statistics:\n{summary}")
print(f"\nShapiro-Wilk V3: p={shapiro_v3.pvalue:.4f}")
print(f"Shapiro-Wilk C1: p={shapiro_c1.pvalue:.4f}")
print(f"Levene's test: p={levene_test.pvalue:.4f}")
print(f"\nTest usado: {test_name}")
print(f"Estadístico: {stat:.4f}, p-value: {p_val:.4f}")

```

```text
Summary Statistics:
              mean       std  count  median
Implante                                   
C1       -0.544615  0.734672     13   -0.52
V3       -1.315833  0.649160     12   -1.27

Shapiro-Wilk V3: p=0.1462
Shapiro-Wilk C1: p=0.1224
Levene's test: p=0.6500

Test usado: t-test independiente
Estadístico: -2.7716, p-value: 0.0109

```

Tras analizar los datos del estudio odontológico, he realizado un test estadístico para comparar el cambio en la medida "CBCT Neck" (calculada como la diferencia entre los 4 meses y el día de la operación) entre los dos grupos de implantes (**V3** y **C1**).

Aquí tienes los resultados detallados:

### 1. Resumen Descriptivo

La variable analizada es la **diferencia (mm)** entre el tiempo final e inicial. Los valores negativos indican una reducción en la medida del cuello óseo/implante.

| Grupo de Implante | N | Media (mm) | Desviación Estándar | Mediana (mm) |
| --- | --- | --- | --- | --- |
| **C1** | 13 | $-0,54$ | $0,73$ | $-0,52$ |
| **V3** | 12 | $-1,32$ | $0,65$ | $-1,27$ |


#### 2. Verificación de Supuestos

Para elegir el test correcto, primero validamos los datos:

* **Normalidad:** Ambos grupos siguen una distribución normal (Test de Shapiro-Wilk, $p > 0,05$).
* **Homogeneidad de varianzas:** No hay diferencias significativas en la dispersión de los datos (Test de Levene, $p = 0,65$).

Dado que se cumplen estos requisitos, el test más robusto es el **T-test para muestras independientes**.

#### 3. Resultado del Test Estadístico

* **Valor p:** $0,0109$
* **Conclusión:** Existe una **diferencia estadísticamente significativa** ($p < 0,05$) entre los dos tipos de implante.

#### Interpretación de los Resultados

El grupo **V3** presenta una reducción media de la medida significativamente mayor ($-1,32$ mm) que el grupo **C1** ($-0,54$ mm). En términos clínicos, esto sugiere que el comportamiento de los tejidos o del implante en la zona del "neck" difiere según el modelo utilizado durante los primeros cuatro meses.

¿Te gustaría que realice alguna otra comparación, como analizar la estabilidad de cada grupo por separado o crear un gráfico de evolución temporal?