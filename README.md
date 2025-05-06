# **Onlygiant**

Proyecto para determinar el pozo petrolero más factible para su explotación a partir de datos geológicos y económicos.


## 📌 Descripción

**Onlygiant** es un proyecto de análisis de datos cuyo objetivo es identificar cuál de varios pozos prospectivos de petróleo ofrece la mejor combinación de reservas estimadas y viabilidad económica para su explotación. Se utilizan datos geológicos (volumen, área, espesor) y parámetros económicos (precio del barril, costo de perforación, tasa de descuento) para calcular indicadores como el Valor Presente Neto (VPN) y la Tasa Interna de Retorno (TIR).

---

## 🗃️ Datos

Los datos se encuentran en tres archivos CSV:

- `geo_data_0.csv`  
- `geo_data_1.csv`  
- `geo_data_2.csv`  

Cada uno contiene las propiedades geológicas y petrofísicas de distintos conjuntos de pozos:  
- Coordenadas y área de drenaje  
- Espesor neto de la formación  
- Porosidad y saturación de petróleo  
- Factor volumétrico de formación  

---

## ⚙️ Metodología

1. **Carga y unificación de datos** en un único DataFrame.  
2. **Análisis exploratorio** para verificar valores faltantes y rangos físicos.  
3. **Cálculo de reservas in situ** usando la fórmula:
           Volumen [STB] = Área · Espesor neto · Porosidad · Saturación · Factor
4. **Evaluación económica** de cada pozo:  
- Cálculo de flujo de caja anual estimado  
- Valor Presente Neto (VPN)  
- Tasa Interna de Retorno (TIR)  
5. **Selección del pozo óptimo** según criterios de VPN máximo y TIR mínimo aceptable.  
6. **Visualización** de resultados con gráficos de barras, curva de acumulación y ranking de pozos.

---

