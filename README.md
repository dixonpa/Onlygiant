# OilyGiant: selección de región para nuevos pozos petroleros

Análisis para decidir en cuál de tres regiones debe la compañía **OilyGiant** perforar 200 pozos nuevos. Combina un modelo de **regresión lineal** que predice las reservas con una simulación **bootstrap** que estima el beneficio y el riesgo de pérdidas.

## 📊 Resultado

| Región | RMSE del modelo | Beneficio medio | IC 95 % | Riesgo de pérdida |
|---|---|---|---|---|
| 0 | 37.7 | 4.32 M USD | (−0.81, 9.41) M | 5.5 % ❌ |
| **1** | **0.9** | **4.78 M USD** | **(0.52, 8.98) M** | **2.0 % ✅** |
| 2 | 40.0 | 3.22 M USD | (−1.73, 8.44) M | 12.3 % ❌ |

**Recomendación: región 1.** Es la única que cumple el requisito de riesgo de pérdida menor al 2.5 % y, además, tiene el mayor beneficio esperado. Aunque sus reservas medias son menores, el modelo las predice con mucha precisión, así que los pozos elegidos son realmente buenos.

## 🎯 Condiciones del negocio

- En cada región se exploran **500 puntos** y se eligen los **200 mejores** según el modelo.
- Presupuesto: **100 M USD** para los 200 pozos.
- Ingreso: **4 500 USD** por unidad de producto (1 000 barriles). Cada pozo necesita ≈ 111.1 mil barriles para cubrir su coste.
- Se descartan las regiones con un riesgo de pérdida ≥ 2.5 %.

## 🗃️ Datos

Tres archivos en `data/raw/` (`geo_data_0.csv`, `geo_data_1.csv`, `geo_data_2.csv`), uno por región, con 100 000 puntos de exploración cada uno:

| Columna | Descripción |
|---|---|
| `id` | Identificador del pozo |
| `f0`, `f1`, `f2` | Características geológicas (anonimizadas) |
| `product` | Volumen de reservas (miles de barriles) |

## ⚙️ Metodología

1. **Revisión de datos:** nulos, duplicados (se eliminan los `id` repetidos con valores distintos), distribuciones y correlaciones.
2. **Modelo por región:** regresión lineal con división 75/25 y evaluación con RMSE.
3. **Punto de equilibrio:** reservas mínimas por pozo para no tener pérdidas.
4. **Beneficio:** se eligen los pozos con mayor reserva **predicha** y se suman sus reservas **reales**.
5. **Bootstrap (1 000 simulaciones):** beneficio medio, intervalo de confianza del 95 % y riesgo de pérdida.

## 📁 Estructura del proyecto

```
Onlygiant/
├── data/
│   └── raw/                              # Datos de exploración por región
├── notebooks/
│   └── oilygiant_well_selection.ipynb    # Análisis completo
├── requirements.txt
└── README.md
```

## 🚀 Cómo ejecutarlo

Requisitos: Python 3.11 o superior.

```bash
git clone https://github.com/dixonpa/Onlygiant.git
cd Onlygiant
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/oilygiant_well_selection.ipynb
```

## 🛠️ Tecnologías

Python · pandas · NumPy · scikit-learn · Matplotlib · seaborn · Jupyter
