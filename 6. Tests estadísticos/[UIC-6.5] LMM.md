# [UIC-6.5] LMM

## Input

El archivo Excel adjunto contiene datos de un estudio de odontología.

La columna "Paciente" contiene un ID para cada participante en el estudio.

Hay dos grupos de pacientes, y la pertenencia a uno u otro grupo se indica en la columna "Implante".

Las columnas "CBCT_neck_0" y "CBCT_neck_1" contienen valores de la medida "CBCT Neck" en dos tiempos: el día de la operación y al cabo de cuatro meses.

Haz un análisis estadístico basado en un modelo lineal de efectos mixtos que contenga un término "Implante", un término "Tiempo" y un término de interacción.

## Output (Gemini 3 Thinking)

```python
import pandas as pd
import statsmodels.api as sm
import statsmodels.formula.api as smf

# Load the data
file_path = '[UIC-6.1] Data.xlsx - Sheet 1.csv'
df = pd.read_csv(file_path)

# Reshape data from wide to long format
# We have CBCT_neck_0 and CBCT_neck_1.
df_long = pd.melt(df, id_vars=['Paciente', 'Implante'], 
                  value_vars=['CBCT_neck_0', 'CBCT_neck_1'],
                  var_name='Tiempo', value_name='CBCT_neck')

# Clean 'Tiempo' column to be numeric or categorical
df_long['Tiempo'] = df_long['Tiempo'].map({'CBCT_neck_0': 0, 'CBCT_neck_1': 1})

# Drop rows with missing values for the analysis
df_clean = df_long.dropna(subset=['CBCT_neck'])

# Fit the mixed-effects model
# Formula: CBCT_neck ~ Implante * Tiempo
# Random Effect: Random intercept for each Paciente
model = smf.mixedlm("CBCT_neck ~ C(Implante) * C(Tiempo)", df_clean, groups=df_clean["Paciente"])
result = model.fit()

# Get the summary
summary = result.summary()
print(summary)

# Calculate means for interpretation
means = df_clean.groupby(['Implante', 'Tiempo'])['CBCT_neck'].mean().reset_index()
print("\nMedias por grupo y tiempo:")
print(means)

```

```text
                   Mixed Linear Model Regression Results
===========================================================================
Model:                    MixedLM       Dependent Variable:       CBCT_neck
No. Observations:         59            Method:                   REML     
No. Groups:               34            Scale:                    0.2435   
Min. group size:          1             Log-Likelihood:           -76.0379 
Max. group size:          2             Converged:                Yes      
Mean group size:          1.7                                              
---------------------------------------------------------------------------
                                 Coef.  Std.Err.   z    P>|z| [0.025 0.975]
---------------------------------------------------------------------------
Intercept                         3.006    0.253 11.902 0.000  2.511  3.500
C(Implante)[T.V3]                 0.584    0.368  1.586 0.113 -0.138  1.305
C(Tiempo)[T.1]                   -0.570    0.191 -2.984 0.003 -0.944 -0.196
C(Implante)[T.V3]:C(Tiempo)[T.1] -0.789    0.275 -2.864 0.004 -1.329 -0.249
Group Var                         0.904    0.837                           
===========================================================================

Medias por grupo y tiempo:
  Implante  Tiempo  CBCT_neck
0       C1       0   3.005556
1       C1       1   2.343077
2       V3       0   3.589375
3       V3       1   2.072500

```

He realizado el análisis estadístico utilizando un **modelo lineal de efectos mixtos (LMM)**. Este tipo de modelo es el estándar de oro para estudios odontológicos con medidas repetidas, ya que permite manejar datos de un mismo paciente en diferentes tiempos y es robusto ante la pérdida de algunos datos puntuales (valores faltantes).

Para el análisis, los datos se han reestructurado a formato "largo" y se ha definido el **Paciente** como el efecto aleatorio (para controlar la variabilidad individual).

### Resultados del Modelo de Efectos Mixtos

A continuación se detallan los coeficientes del modelo para la variable dependiente `CBCT_neck`:

| Término | Coeficiente (Est.) | Error Est. | valor *p* | Significación |
| --- | --- | --- | --- | --- |
| **Intercepto** (Referencia: C1 en T0) | 3.006 | 0.253 | < 0.001 | *** |
| **Implante [V3]** (Diferencia inicial) | 0.584 | 0.368 | 0.113 | No sig. |
| **Tiempo [T1]** (Cambio en grupo C1) | -0.570 | 0.191 | **0.003** | ** |
| **Interacción (V3 x T1)** | -0.789 | 0.275 | **0.004** | ** |

### Interpretación de los Hallazgos

1. **Efecto del Tiempo (Significativo):** Existe una disminución general de los valores de `CBCT_neck` tras cuatro meses. En el grupo de control (**C1**), la reducción media es de **0.57 unidades** ($p = 0.003$).
2. **Efecto del Implante (No significativo al inicio):** Al día de la operación (T0), no se encontraron diferencias estadísticamente significativas entre los implantes V3 y C1 ($p = 0.113$), aunque el grupo V3 empezó con valores ligeramente superiores.
3. **Efecto de Interacción (Muy Significativo):** Este es el resultado más importante. El valor de $p = 0.004$ indica que **el tipo de implante influye significativamente en la evolución de la medida a lo largo del tiempo**.

> **Conclusión técnica:** El grupo con el implante **V3** experimentó una reducción mucho más pronunciada que el grupo C1. Mientras que C1 bajó 0.57, el grupo V3 bajó un total de **1.359 unidades** (0.57 del tiempo + 0.789 de la interacción) entre el día 0 y el cuarto mes.

### Medias Estimadas

* **Implante C1:** De 3.01 (T0) a 2.44 (T1).
* **Implante V3:** De 3.59 (T0) a 2.23 (T1).

¿Te gustaría que genere un gráfico de interacción para visualizar cómo divergen las pendientes de ambos grupos de implantes?