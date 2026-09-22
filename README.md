# Laboratorio N°1: Formateo de la Información y Ecualización del Histograma
## Comunicación Digital Avanzada — Universidad Nacional de Río Cuarto (UNRC)
### Marco Normativo: DVB-S (ETSI EN 300 421)

Este repositorio contiene la implementación integral del **Laboratorio N°1** de la materia **Comunicación Digital Avanzada**. El sistema procesa y acondiciona dos flujos de datos independientes en paralelo (fuente discreta de texto y fuente analógica de audio), implementando dispersión de energía satelital mediante aleatorizador PRBS basado en LFSR según la norma **ETSI EN 300 421**.

---

## 1. Estructura de Archivos
- `lab1_CDA.ipynb`: Cuaderno Jupyter con desarrollo teórico en LaTeX, código modular, ejecución secuencial y gráficos integrados.
- `audio_lab1.wav`: Archivo de audio de prueba muestreado a 8 kHz.
- `secuencia_audio_lab1.npy`: Flujo binario de audio acondicionado (PCM 6 bits + Ley-µ + DVB-S Scrambler) para alimentar el Modulador Digital del Laboratorio N°2.
- `secuencia_texto_lab1.npy`: Flujo binario de texto acondicionado (ASCII 8 bits + DVB-S Scrambler) para el Laboratorio N°2.
- `metadatos_lab1.json`: Parámetros de ingeniería de ambas fuentes y métricas de información calculadas.
- `panel_laboratorio_1.png`: Figura comparativa de 6 paneles en alta resolución (300 DPI).
- `requirements.txt`: Dependencias del entorno de ejecución.

---

## 2. Puesta en Marcha en Entorno Linux

```bash
# 1. Crear el entorno virtual (si no existe)
python3 -m venv venv

# 2. Activar el entorno virtual
source venv/bin/activate

# 3. Instalar dependencias del proyecto
pip install -r requirements.txt

# 4. Iniciar Jupyter Lab
jupyter lab
```

Abrir `lab1_CDA.ipynb` y ejecutar las celdas secuencialmente.

---

## 3. Métricas y Resultados Obtenidos

| Fuente / Estado | $P(0)$ | $P(1)$ | $H(X)$ [bit/bit] | Racha Máx 0 | Racha Máx 1 |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Texto (Raw)** | 0.5304 | 0.4696 | 0.9973 | 6 | 4 |
| **Texto (Scrambled DVB-S)** | 0.4764 | 0.5236 | 0.9984 | 10 | 9 |
| **Audio PCM (Raw)** | 0.5175 | 0.4825 | 0.9991 | 7 | 7 |
| **Audio (Scrambled DVB-S)** | 0.5005 | 0.4995 | 1.0000 | 18 | 17 |

- **Reversibilidad y BER:** Comprobación estricta con `assert` de $BER = 0.00000000$ para ambos canales.
- **SQNR Medido (Audio Ley-µ, $k=6$ bits):** $25.90\text{ dB}$.
