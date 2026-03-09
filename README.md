# 🕵️ Mentes en la Sombra: Perfilado Criminal con IA

> **Curso:** Inteligencia Artificial: Generación de Prompts  
> **Comisión:** N° 95825  
> **Autora:** Angelica Aparicio  
> **Entrega:** Proyecto Final

---

## 📋 Resumen

*Mentes en la Sombra* es una herramienta de apoyo formativo que utiliza la API de Google Gemini y técnicas de Fast Prompting para generar automáticamente material educativo sobre análisis de perfiles criminales. A partir de un único dato de entrada —el tipo de delito a analizar— el sistema produce en tres llamadas a la API un escenario ficticio, un perfil psicológico fundamentado y un ejercicio didáctico completo con guía de respuestas.

El proyecto aborda la escasez de recursos formativos accesibles en criminología y psicología forense, democratizando la creación de material de calidad para docentes y estudiantes. Trabaja exclusivamente con escenarios ficticios, garantizando un uso ético de la IA dentro del ámbito académico.

---

## 📌 Introducción

### Nombre del proyecto
**Mentes en la Sombra: Perfilado Criminal con IA**

### Problema a abordar

La formación en análisis de perfiles criminales combina psicología, criminología y ciencia forense. Generar material educativo en este campo es complejo por varios motivos:

- Requiere conocimiento profundo de patrones de comportamiento, tipología delictiva y metodología de investigación criminal
- Los casos reales son escasos en publicación libre; muchos están sujetos a restricciones de confidencialidad
- La producción manual de escenarios ficticios realistas consume tiempo desproporcionado respecto al valor didáctico
- Pocos docentes poseen la combinación de habilidades para crear material textual y visual de calidad simultáneamente

Esta escasez limita significativamente el acceso a recursos formativos fuera de contextos académicos de alto nivel.

### Propuesta de solución

La solución integra dos tipos de modelos de IA de manera complementaria:

**Modelo texto-texto (Google Gemini):** Genera escenarios ficticios, perfiles psicológicos y ejercicios didácticos mediante un flujo de prompts encadenados que aplica técnicas de Fast Prompting.

**Modelo texto-imagen (Nightcafe):** Genera imágenes ilustrativas de los escenarios mediante prompts diseñados con vocabulario de atmósfera (noir, tensión, evidencia policial) para evitar los filtros de seguridad.

### Viabilidad del proyecto

| Criterio | Evaluación | Detalle |
|---|---|---|
| Recursos técnicos | ✅ Alto | Google Gemini API gratuita; Nightcafe gratuito. Sin hardware especial |
| Tiempo disponible | ✅ Alto | Desarrollo modular por etapas; cada prompt testeable de forma independiente |
| Complejidad | ⚠️ Media | Problema fraccionado en subtareas claras y secuenciales |
| Dependencias | ✅ Baja | Sin infraestructura externa ni licencias pagas |
| Ética | ✅ Controlada | Solo escenarios ficticios; sin datos reales de víctimas ni casos reales |

---

## 🎯 Objetivos

1. Demostrar que Fast Prompting permite generar material formativo especializado de calidad con pocas llamadas a la API
2. Implementar un flujo de prompts encadenados coherente que produzca escenario → perfil → ejercicio en una sola ejecución
3. Aplicar técnicas de Role Prompting, Chain of Thought y Few-Shot de forma deliberada y justificada
4. Optimizar el uso de la API a un mínimo de consultas sin sacrificar calidad del output
5. Generar imágenes ilustrativas con prompts diseñados para respetar los filtros de seguridad de las herramientas

---

## 🔬 Metodología

El proyecto sigue un flujo secuencial de tres etapas, donde la salida de cada etapa alimenta la siguiente:

```
[Input: tipo de delito]
        │
        ▼
┌─────────────────────┐
│  LLAMADA 1 (API)    │  Zero-Shot + Role Prompting
│  Escenario ficticio │  → genera el contexto base
└────────┬────────────┘
         │ contexto
         ▼
┌─────────────────────┐
│  LLAMADA 2 (API)    │  Few-Shot + Chain of Thought + Role Prompting
│  Perfil psicológico │  → razona sobre el escenario con evidencia
└────────┬────────────┘
         │ contexto acumulado
         ▼
┌─────────────────────┐
│  LLAMADA 3 (API)    │  Role Prompting + instrucción estructurada
│  Ejercicio didáctico│  → produce material pedagógico listo para usar
└─────────────────────┘
         │
         ▼
[Output: material formativo completo — 3 consultas a la API]
```

Este diseño evita llamadas redundantes: el contexto se pasa explícitamente entre prompts en lugar de hacer llamadas adicionales de "resumen" o "recuerdo".

---

## 🛠️ Herramientas y tecnologías

| Herramienta | Uso | Técnica de prompting |
|---|---|---|
| **Google Gemini** `gemini-1.5-flash` | Generación de texto (escenario, perfil, ejercicio) | Role Prompting, Zero-Shot, Few-Shot, Chain of Thought |
| **Nightcafe** | Generación de imágenes ilustrativas | Prompts de atmósfera noir |
| **Python 3.10+** | Lenguaje de implementación | — |
| **Jupyter Notebook** | Entorno de demostración de la POC | — |

### Justificación de técnicas

- **Role Prompting:** asignar un rol especializado (criminólogo / psicólogo forense / docente) eleva la precisión y el registro académico del output en cada etapa
- **Zero-Shot** en el escenario: la instrucción es suficientemente detallada como para no requerir ejemplos; agregar ejemplos aumentaría el costo sin mejorar el resultado
- **Few-Shot + Chain of Thought** en el perfil: el razonamiento forense requiere justificar cada inferencia con evidencia; el ejemplo de razonamiento guía el formato esperado y reduce outputs vagos
- **Prompts encadenados:** mantiene coherencia narrativa entre las tres secciones sin llamadas adicionales

---

## 💻 Implementación

El código completo está disponible en el notebook [`mentes_en_la_sombra.ipynb`](./mentes_en_la_sombra.ipynb).

### Prompts de generación de imágenes (Nightcafe)

Los siguientes prompts fueron utilizados para generar las imágenes ilustrativas. Se utiliza vocabulario de atmósfera para evitar los filtros de seguridad de la herramienta.

---

**Prompt 4 — Escena de investigación policial**
```
A dark urban alleyway at night, crime scene investigation atmosphere, 
noir style, police tape in foreground, dramatic high-contrast lighting, 
flashlight beams cutting through shadows, forensic evidence markers on 
the ground, cinematic composition, mysterious and tense mood, 
photorealistic, no people, no faces, dark blue and yellow tones
```

**Resultado:**

![Escena de investigación policial](./assets/imagen_escena.png)
*Imagen generada con Nightcafe — Escena de investigación nocturna, estilo noir*

---

**Prompt 5 — Entorno del caso**
```
Abandoned dimly lit office interior, noir detective atmosphere, 
scattered documents on a desk, single lamp casting dramatic shadows, 
dust particles in light beam, mysterious and suspenseful mood, 
cinematic style, photorealistic, no people, muted dark tones, 
high detail
```

**Resultado:**

![Entorno del caso](./assets/imagen_entorno.png)
*Imagen generada con Nightcafe — Entorno interior, atmósfera de suspenso*

---

## 📊 Resultados

La implementación logra el objetivo central del proyecto: generar material formativo completo, coherente y académicamente válido con **exactamente 3 llamadas a la API**.

**Lo que funciona bien:**
- El encadenamiento de contexto mantiene consistencia entre el escenario, el perfil y el ejercicio: los tres hablan del mismo caso
- El Chain of Thought en el perfil psicológico produce razonamientos justificados (evidencia → conclusión) en lugar de listados genéricos
- El Role Prompting diferenciado por etapa genera registros apropiados: narrativo en el escenario, analítico en el perfil, pedagógico en el ejercicio
- El sistema funciona con cualquier tipo de delito: robo, estafa, secuestro, etc.

**Limitaciones:**
- La generación de imágenes es manual (Nightcafe no tiene API gratuita), lo que rompe el flujo automático
- El sistema no exporta el material generado a archivo; requiere copiar el output manualmente
- La calidad del output depende de qué tan específico sea el tipo de delito ingresado

**Comparativa con la Pre-entrega 1:**

| Aspecto | Pre-entrega 1 | Proyecto Final |
|---|---|---|
| Rol del modelo | Genérico | Especializado por etapa |
| Razonamiento | Respuesta directa | Chain of Thought con evidencia → conclusión |
| Guía de output | Solo descripción | Few-Shot con ejemplo de razonamiento |
| Prompts de imagen | Lenguaje explícito | Vocabulario noir/atmósfera |
| Llamadas a la API | Sin optimizar | 3 llamadas exactas |

---

## ✅ Conclusiones

El proyecto demuestra que es posible construir una herramienta formativa funcional y optimizada aplicando técnicas de Fast Prompting de forma deliberada. Los objetivos propuestos se lograron:

- ✅ Se implementó un flujo de 3 prompts encadenados que genera material completo y coherente
- ✅ Las técnicas de Role Prompting, CoT y Few-Shot mejoraron notablemente la calidad respecto a prompts simples
- ✅ El sistema se optimizó a 3 consultas a la API, haciéndolo viable en términos de costo
- ✅ Los prompts de imagen con vocabulario de atmósfera resuelven el problema de los filtros de seguridad
- ⚠️ La integración de imagen sigue siendo el punto débil del flujo por la falta de APIs gratuitas

La principal lección del proyecto es que **el diseño del prompt es más determinante que el modelo elegido**: el mismo modelo con un prompt bien estructurado produce resultados académicamente válidos, mientras que con un prompt vago produce contenido genérico e inutilizable para fines formativos.

---

## 📚 Referencias

- Google AI Studio — Documentación de Gemini API: https://aistudio.google.com
- OpenAI Prompt Engineering Guide: https://platform.openai.com/docs/guides/prompt-engineering
- Nightcafe Creator: https://creator.nightcafe.studio
- Turvey, B. (2011). *Criminal Profiling: An Introduction to Behavioral Evidence Analysis*. Academic Press.
- Douglas, J., Burgess, A., Burgess, A. G., & Ressler, R. (2013). *Crime Classification Manual*. Wiley.

---

*Proyecto desarrollado para el curso de Inteligencia Artificial: Generación de Prompts — Comisión 95825*
