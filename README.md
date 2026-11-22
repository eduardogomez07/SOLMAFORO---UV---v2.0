# SOLMAFORO---UV---v2.0
# Solmáforo UV Inteligente con IoT

### Sistema de medición, visualización y alerta de radiación ultravioleta

**UPATecO – Universidad Provincial de la Administración, Tecnología y Oficios**  
**Carrera:** Tecnicatura Universitaria en Automatización y Robótica  
**Asignatura:** Transductores y Actuadores 
**Área:** Electrónica –Robótica– Internet de las Cosas (IoT)

---
---
## 1. Descripción del proyecto

El **Solmáforo UV Inteligente con IoT** es un dispositivo electrónico diseñado para medir y visualizar el nivel de radiación ultravioleta presente en el ambiente, proporcionando información comprensible para prevenir los riesgos asociados a la exposición solar.

El sistema utiliza un sensor de radiación ultravioleta conectado a un microcontrolador ESP32. Los valores obtenidos son procesados y representados mediante una pantalla TFT, que muestra el índice UV estimado y su correspondiente categoría de riesgo.

Además, incorpora una lámpara RGB externa que funciona como indicador visual del nivel de radiación, conectividad inalámbrica para el control de sus funciones y comunicación con una plataforma IoT para registrar y visualizar mediciones.

Cuando se detecta un nivel extremo de radiación ultravioleta, el sistema contempla el envío de una notificación mediante WhatsApp.

El proyecto integra conocimientos de transductores, sensores, electrónica digital, programación de microcontroladores, comunicaciones inalámbricas y aplicaciones IoT.

## 2. Objetivos

### Objetivo general

Desarrollar un sistema electrónico inteligente capaz de medir, procesar, visualizar y comunicar información sobre la radiación ultravioleta ambiental, contribuyendo a la prevención de los riesgos asociados a la exposición solar.

### Objetivos específicos

- Implementar un sensor de radiación UV como transductor de entrada.
- Adquirir y procesar señales analógicas mediante un microcontrolador ESP32.
- Estimar y visualizar el índice UV en una pantalla TFT.
- Clasificar los niveles de radiación mediante una escala de colores.
- Implementar una lámpara RGB como indicador visual externo.
- Incorporar comunicación Bluetooth Low Energy (BLE).
- Transmitir las mediciones a una plataforma IoT.
- Registrar la evolución temporal de las mediciones.
- Implementar un mecanismo de alerta para niveles extremos de radiación.
- Promover el desarrollo de soluciones tecnológicas aplicadas a la salud y el medio ambiente.

## 3. Arquitectura general del sistema

El funcionamiento se organiza en cinco etapas:

1. **Captación:** el sensor GUVA-S12SD detecta la radiación ultravioleta y entrega una señal analógica.
2. **Adquisición y procesamiento:** el ESP32 adquiere la señal mediante su conversor analógico-digital (ADC), realiza el procesamiento y estima el nivel UV.
3. **Visualización:** la pantalla TFT presenta el índice UV y su categoría de riesgo.
4. **Señalización:** una lámpara RGB externa representa visualmente el nivel de radiación.
5. **Comunicación:** el sistema transmite información a ThingSpeak y contempla alertas mediante WhatsApp ante niveles extremos.

### Diagrama conceptual

```text
       RADIACIÓN SOLAR UV
                │
                ▼
       ┌─────────────────┐
       │  Sensor GUVA    │
       │    S12SD        │
       └────────┬────────┘
                │ Señal analógica
                ▼
       ┌─────────────────┐
       │     ESP32       │
       │ Adquisición ADC │
       │ Procesamiento   │
       └────────┬────────┘
                │
       ┌────────┼──────────────┐
       │        │              │
       ▼        ▼              ▼
   ┌────────┐ ┌────────┐  ┌───────────┐
   │ Pantalla│ │ Lámpara│  │ Plataforma│
   │   TFT   │ │  RGB   │  │ ThingSpeak│
   └────────┘ └────────┘  └─────┬─────┘
                                │
                                ▼
                          Registro de datos

                ESP32
                  │
                  ▼
             Alerta WhatsApp
          (cuando UV ≥ 11)
```

## 4. Componentes y características técnicas

| Componente | Característica / función |
|---|---|
| Microcontrolador | ESP32 TTGO T-Display |
| Sensor UV | GUVA-S12SD |
| Pantalla | TFT ST7789 de 1,14 pulgadas |
| Resolución | 240 × 135 píxeles |
| Conversión analógica | ADC integrado en ESP32 |
| Comunicación inalámbrica | Wi-Fi 2,4 GHz y BLE |
| Indicador externo | Lámpara RGB Bluetooth |
| Plataforma IoT | ThingSpeak |
| Servicio de alertas | CallMeBot / WhatsApp |
| Alimentación | USB, 5 V |

### Componentes principales

#### Microcontrolador ESP32

Es la unidad central de procesamiento. Se encarga de adquirir las señales del sensor, realizar los cálculos, actualizar la pantalla y gestionar las comunicaciones inalámbricas.

#### Sensor GUVA-S12SD

Es el transductor encargado de captar la radiación ultravioleta y convertirla en una señal eléctrica analógica proporcional a la radiación recibida dentro de su respuesta espectral.

#### Pantalla TFT

Permite visualizar el índice UV estimado y su clasificación de riesgo en tiempo real.

#### Lámpara RGB Bluetooth

Funciona como señalización visual externa. Su color cambia de acuerdo con el nivel de radiación detectado.

#### Plataforma ThingSpeak

Permite almacenar y visualizar las mediciones transmitidas por el ESP32, facilitando el análisis de la evolución temporal de la radiación.

## 5. Escala de radiación ultravioleta

El sistema utiliza las siguientes categorías de referencia del índice UV:

| Índice UV | Categoría | Color | Recomendaciones |
|---|---|---|---|
| 0 – 2 | Bajo | 🟢 Verde | Riesgo bajo. Disfrutar del aire libre. |
| 3 – 5 | Moderado | 🟡 Amarillo | Utilizar protector solar, gorro y anteojos. |
| 6 – 7 | Alto | 🟠 Naranja | Buscar sombra y proteger la piel. |
| 8 – 10 | Muy alto | 🔴 Rojo | Reducir la exposición solar. |
| 11 o más | Extremo | 🟣 Violeta | Evitar la exposición solar directa. |

**Importante:** el índice UV es una escala de riesgo asociada a la radiación ultravioleta. No representa directamente una temperatura ni una medición de potencia eléctrica.

Las recomendaciones se basan en la escala internacional de índice UV. La exposición también depende del horario, la nubosidad, la altitud, la reflexión del entorno y las características individuales.

## 6. Conectividad e Internet de las Cosas

El proyecto incorpora conectividad para ampliar las posibilidades de monitoreo y control.

### ThingSpeak

El ESP32 transmite periódicamente los datos a ThingSpeak mediante Wi-Fi.

Los campos configurados son:

| Campo | Información |
|---|---|
| Field 1 | Índice UV estimado |
| Field 2 | Lectura ADC del sensor |
| Field 3 | Categoría de radiación |
| Field 4 | Color de la lámpara |
| Field 5 | Modo de funcionamiento |
| Field 6 | Intensidad de señal Wi-Fi (RSSI) |
| Field 7 | Estado de conexión BLE |

El intervalo de actualización configurado es de aproximadamente 20 segundos.

### Bluetooth Low Energy (BLE)

Se utiliza para establecer comunicación inalámbrica entre el ESP32 y la lámpara RGB externa.

El sistema permite enviar comandos para modificar el color de iluminación según el nivel de radiación detectado.

### Alertas por WhatsApp

Cuando el índice UV alcanza o supera el umbral extremo configurado (UV ≥ 11), el sistema contempla el envío de una notificación mediante CallMeBot.

La lógica de alerta considera el reintento de envío y la reactivación de la alarma cuando el nivel de radiación desciende por debajo del umbral durante el tiempo establecido.

## 7. Registro y análisis de radiación UV

Se realizaron registros de mediciones durante una jornada de noviembre en Salta Capital, con el objetivo de observar el comportamiento de la señal del sensor a lo largo del día.

<p align="center">
  <img src="assets/grafico-radiacion-noviembre.png" alt="Registro de radiación durante una jornada de noviembre" width="800">
</p>

### Interpretación del registro

En el gráfico se observa una variación de la señal durante el transcurso de la jornada.

Se identifica un incremento progresivo durante la mañana y un pico pronunciado alrededor del mediodía solar. Posteriormente, la señal disminuye durante la tarde, con algunas fluctuaciones intermedias.

Este comportamiento es consistente con la variación diaria de la radiación solar.

**Nota metodológica:** los valores del gráfico corresponden a la señal registrada por el sistema y deben identificarse con su unidad o escala de adquisición correspondiente. No deben interpretarse automáticamente como valores del índice UV. Para expresar el índice UV real es necesaria una calibración y validación con un instrumento de referencia.

## 8. Importancia y aplicación del proyecto

La radiación ultravioleta constituye un factor ambiental de importancia para la salud pública. La exposición excesiva puede provocar quemaduras, envejecimiento prematuro de la piel y lesiones oculares, además de incrementar el riesgo de desarrollar cáncer de piel.

El Solmáforo UV Inteligente propone una herramienta tecnológica de información y prevención que permite:

- Comunicar el nivel de radiación de manera visual e inmediata.
- Facilitar la interpretación de los niveles de riesgo.
- Promover hábitos de protección solar.
- Registrar información ambiental para su análisis.
- Incorporar sistemas de alerta y monitoreo remoto.
- Aplicar conocimientos de electrónica, sensores, programación y robótica a una problemática real.

### Posibles aplicaciones

- Instituciones educativas.
- Espacios públicos y recreativos.
- Centros deportivos.
- Establecimientos de salud.
- Municipios y organismos de prevención.
- Estaciones de monitoreo ambiental.

## 9. Calibración y consideraciones experimentales

La señal analógica del sensor debe ser procesada para obtener una estimación del índice UV.

La relación entre la lectura ADC y el índice UV depende de las características del sensor, la electrónica de acondicionamiento, la orientación del dispositivo y las condiciones de medición.

Por este motivo, los parámetros de conversión utilizados en el firmware deben considerarse experimentales hasta completar una calibración con un instrumento UV de referencia.

Para mejorar la confiabilidad de las mediciones se recomienda:

1. Comparar las lecturas con un medidor UV calibrado.
2. Realizar mediciones simultáneas.
3. Repetir el procedimiento en diferentes condiciones de radiación.
4. Obtener una curva de calibración.
5. Ajustar la conversión implementada en el firmware.
6. Verificar la estabilidad y repetibilidad del sistema.

También debe tenerse en cuenta que la orientación del sensor, las sombras, la presencia de obstáculos y la respuesta espectral del transductor influyen en los resultados.

## 10. Posibilidades de ampliación

El proyecto permite incorporar nuevas funcionalidades:

- Integración de sensores ambientales adicionales.
- Medición de temperatura y humedad.
- Almacenamiento histórico de mediciones.
- Incorporación de una estación meteorológica.
- Desarrollo de una aplicación móvil.
- Implementación de un servidor IoT propio.
- Incorporación de paneles solares y alimentación autónoma.
- Comparación con datos de estaciones meteorológicas oficiales.
- Desarrollo de algoritmos de calibración y compensación.

## 11. Conclusiones

El desarrollo del Solmáforo UV Inteligente demuestra la aplicación práctica de los conocimientos adquiridos en el área de Transductores y Sensores, integrando adquisición de señales, procesamiento digital, visualización y comunicaciones inalámbricas.

La utilización del sensor GUVA-S12SD y del microcontrolador ESP32 permite construir una solución compacta para el monitoreo de la radiación ultravioleta. La incorporación de una pantalla TFT, una lámpara RGB y una plataforma IoT amplía las posibilidades de interpretación, comunicación y registro de la información.

El proyecto constituye una propuesta tecnológica de carácter educativo y aplicado, con potencial para contribuir a la concientización sobre los riesgos de la exposición solar y para impulsar el desarrollo de sistemas inteligentes orientados a la salud y el medio ambiente.

---

## 12. Instalación y puesta en marcha

### Requisitos

- Arduino IDE.
- Placa ESP32 TTGO T-Display.
- Sensor GUVA-S12SD.
- Lámpara RGB Bluetooth compatible.
- Conexión Wi-Fi de 2,4 GHz.
- Cuenta y canal configurado en ThingSpeak.
- Servicio de alertas CallMeBot, si se desea utilizar WhatsApp.

### Procedimiento

1. Descargar o clonar este repositorio.
2. Abrir el archivo `firmware/SolmaforoUV_IoT/SolmaforoUV_IoT.ino`.
3. Configurar la placa ESP32 correspondiente en Arduino IDE.
4. Instalar y configurar la biblioteca TFT_eSPI para la pantalla TTGO T-Display.
5. Completar los parámetros de conexión en el archivo privado `secrets.h`.
6. Configurar las credenciales y campos de ThingSpeak.
7. Seleccionar el puerto correspondiente.
8. Compilar y cargar el firmware.
9. Verificar las lecturas del sensor y el funcionamiento de la pantalla.
10. Comprobar la conectividad Wi-Fi, BLE y el registro de datos.

### Seguridad de las credenciales

No publiques contraseñas de Wi-Fi, claves de escritura de ThingSpeak ni claves de servicios de mensajería en GitHub.

Utilizá un archivo local `secrets.h` excluido del repositorio y mantené una versión de ejemplo sin datos reales.

## 13. Estructura del proyecto

```text
solmaforo-uv-inteligente-iot/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── firmware/
│   └── SolmaforoUV_IoT/
│       ├── SolmaforoUV_IoT.ino
│       └── secrets.h.example
│
├── docs/
│   ├── funcionamiento.md
│   ├── conexiones.md
│   ├── calibracion.md
│   ├── niveles-uv.md
│   └── analisis-de-datos.md
│
└── assets/
    ├── solmaforo-dispositivo.jpg
    ├── grafico-radiacion-noviembre.png
    └── poster-academico.png
```

## 14. Referencias y recursos

- Organización Mundial de la Salud (OMS): información sobre radiación ultravioleta e índice UV.
- Organización Meteorológica Mundial (OMM): información y recomendaciones sobre el índice UV solar.
- Documentación oficial de Espressif Systems: ESP32.
- Documentación del proyecto ThingSpeak: https://thingspeak.com/
- Documentación de Arduino: https://docs.arduino.cc/
- Datasheet del sensor GUVA-S12SD.

---

<p align="center">
  <strong>UPATecO – Tecnicatura Universitaria en Automatización y Robótica</strong>
  <br>
  Asignatura: Transductores y Actuadores
  <br><br>
</p>
