[English](README.md) | **Español**

# OilyGiant - Elección de región para nuevos pozos de petróleo

Proyecto para decidir en cuál de tres regiones conviene abrir 200 pozos nuevos de petróleo. Usé regresión lineal para predecir las reservas y bootstrapping para calcular la ganancia y el riesgo de pérdida.

## Resultado

| Región | RMSE | Ganancia promedio | Intervalo 95% | Riesgo de pérdida |
|---|---|---|---|---|
| 0 | 37.7 | 4.32 M USD | -0.81 a 9.41 M | 5.5% |
| **1** | **0.9** | **4.78 M USD** | **0.52 a 8.98 M** | **2.0%** |
| 2 | 40.0 | 3.22 M USD | -1.73 a 8.44 M | 12.3% |

**Recomiendo la región 1**, porque es la única con riesgo de pérdida menor al 2.5% y tiene la ganancia promedio más alta. Aunque tiene menos reservas en promedio, el modelo la predice casi sin error, así que los pozos que elige son realmente buenos.

![Distribución de la ganancia](results/figures/profit_distribution.png)

## Condiciones

- En cada región se exploran 500 puntos y se eligen los 200 mejores.
- Presupuesto: 100 millones de USD para los 200 pozos.
- Cada 1000 barriles dejan 4500 USD, así que un pozo necesita al menos 111.1 mil barriles para no perder dinero.
- Solo se descartan las regiones con riesgo de pérdida mayor o igual a 2.5%.

## Datos

Tres archivos en `data/raw/` (`geo_data_0.csv`, `geo_data_1.csv`, `geo_data_2.csv`), uno por región, con 100 000 puntos cada uno:

- `id`: identificador del pozo
- `f0`, `f1`, `f2`: características geológicas
- `product`: reservas en miles de barriles

## Qué hice

1. Revisé los datos y eliminé los `id` que estaban repetidos con valores distintos.
2. Entrené una regresión lineal por región (75% entrenamiento, 25% validación) y la evalué con RMSE.
3. Calculé la ganancia eligiendo los 200 pozos con mayor reserva predicha.
4. Hice 1000 simulaciones con bootstrapping para calcular la ganancia promedio, el intervalo de confianza y el riesgo de pérdida.

**Algo que corregí:** en la primera versión la función de ganancia tomaba un solo pozo en lugar de los 200 mejores, por eso todas las regiones daban pérdida. Al corregirlo, la conclusión cambió.

## Estructura

```
Onlygiant/
├── data/raw/                              # datos por región
├── notebooks/
│   └── oilygiant_well_selection.ipynb     # análisis completo
├── results/figures/                       # gráficos
└── requirements.txt
```

## Cómo ejecutarlo

```bash
git clone https://github.com/dixonpa/Onlygiant.git
cd Onlygiant
python -m venv .venv
.venv\Scripts\activate        # en Windows
source .venv/bin/activate     # en Mac/Linux
pip install -r requirements.txt
jupyter notebook notebooks/oilygiant_well_selection.ipynb
```

## Herramientas

Python, pandas, NumPy, scikit-learn, matplotlib, seaborn.

## Autor

Paulo Alvarez · [LinkedIn](https://www.linkedin.com/in/paulocealva) · [Portafolio](https://dixonpa.github.io/) · palvarez17@gmail.com
