# Explicación de Riesgos Éticos y de Privacidad — ClipMind

> Documento requerido como parte de los entregables del proyecto.
> Fecha: 2026 · Versión 1.0

---

## 1. Propósito de la herramienta

ClipMind es una herramienta de **análisis observacional de clips de video** asistida por inteligencia artificial. Su función es apoyar a la organización, descripción y revisión de material audiovisual, generando observaciones estructuradas que sirven como **borrador preliminar** para un evaluador humano.

La aplicación **no diagnostica, no clasifica personas, no emite juicios clínicos ni toma decisiones finales** de ningún tipo.

---

## 2. Riesgos éticos identificados

### 2.1 Sobredependencia en la IA

**Riesgo:** El usuario podría tratar los resultados del modelo como verdad absoluta, sin revisarlos críticamente.

**Mitigación implementada:**
- Todos los resultados se marcan visualmente como "Borrador generado con apoyo de IA. Requiere revisión humana antes de tomar decisiones."
- Se incluye un campo explícito de revisión humana que el evaluador debe completar antes de actuar sobre el análisis.
- La interfaz nunca presenta a la IA como evaluador final.

---

### 2.2 Análisis de contenido sensible

**Riesgo:** La app podría usarse para analizar videos con contenido clínico, terapéutico, infantil o íntimo sin los controles adecuados.

**Mitigación implementada:**
- Se muestran advertencias explícitas antes de subir cualquier video.
- La app prohíbe expresamente el uso de videos de menores de edad o pacientes reales para pruebas.
- Los resultados de la IA incluyen un campo de `advertencias` donde el modelo puede señalar contenido sensible detectado.

---

### 2.3 Alucinaciones del modelo (hallucinations)

**Riesgo:** El modelo de IA puede generar información plausible pero falsa sobre el contenido del video, especialmente si los fotogramas son ambiguos o de baja calidad.

**Mitigación implementada:**
- El prompt estructurado instruye explícitamente: *"No inventes información. No diagnostiques. Evalúa únicamente lo observable."*
- Los resultados se presentan como observaciones, no como hechos confirmados.
- Se recomienda que el evaluador humano vea el clip completo antes de aceptar el análisis.

---

### 2.4 Sesgo algorítmico

**Riesgo:** Los modelos de lenguaje e imagen pueden presentar sesgos relacionados con género, etnia, apariencia física u otros factores identitarios al describir el contenido de un video.

**Mitigación implementada:**
- El prompt restringe el análisis a aspectos observables y objetivos.
- El evaluador humano es responsable de identificar y corregir cualquier descripción sesgada en el borrador.
- Se recomienda no usar los resultados de IA en contextos de evaluación de desempeño o toma de decisiones sobre personas.

---

### 2.5 Uso fuera del contexto previsto

**Riesgo:** La herramienta podría ser adaptada para vigilancia, evaluación de riesgo, clasificación de personas o usos discriminatorios.

**Mitigación implementada:**
- La aplicación se presenta explícitamente como herramienta de análisis de clips, no de evaluación de personas.
- Las reglas de uso están documentadas en la interfaz y en este documento.
- El código es revisable y no incluye funcionalidades ocultas de almacenamiento en servidores externos.

---

## 3. Riesgos de privacidad identificados

### 3.1 Exposición de datos personales en videos

**Riesgo:** Los videos subidos pueden contener rostros, voces, nombres u otra información identificable de personas que no dieron su consentimiento.

**Controles establecidos:**
- El usuario debe confirmar que tiene consentimiento para usar el material antes de subirlo.
- En el prototipo actual, los videos **no se suben a ningún servidor**: se procesan localmente en el navegador mediante la API de Canvas/Video HTML5.
- Los fotogramas enviados a la API de Claude son imágenes JPEG de 640×360px, sin audio ni metadatos EXIF.

---

### 3.2 Transmisión de fotogramas a APIs externas

**Riesgo:** Los fotogramas del clip se envían a los servidores de Anthropic para su análisis, lo que implica transferencia de datos a terceros.

**Controles establecidos:**
- Solo se envían fotogramas (imágenes estáticas), no el video completo.
- La transmisión ocurre a través de HTTPS con cifrado en tránsito.
- Anthropic tiene políticas de retención de datos para uso de API documentadas en [anthropic.com/privacy](https://anthropic.com/privacy).
- En contextos con datos sensibles, se recomienda revisar el acuerdo de procesamiento de datos de Anthropic antes de usar la app.

---

### 3.3 Almacenamiento de API Keys

**Riesgo:** La API key del usuario podría quedar expuesta si se guarda de forma insegura.

**Controles establecidos:**
- En el prototipo, la API key se guarda **solo en memoria RAM** de la sesión del navegador (no en localStorage ni cookies).
- Al cerrar el navegador, la clave se elimina automáticamente.
- Nunca se almacena en código fuente ni se sube a repositorios.

---

### 3.4 Acceso no autorizado a los análisis guardados

**Riesgo:** Los análisis guardados en localStorage podrían ser accedidos por otras personas que usen el mismo dispositivo.

**Controles establecidos:**
- localStorage es específico por dominio y no se comparte entre usuarios del sistema operativo si usan cuentas separadas.
- Para producción, se recomienda implementar autenticación con Firebase Auth y guardar los análisis en Firestore con reglas de acceso por usuario.
- Se recomienda no usar la app en dispositivos compartidos sin cifrado de disco.

---

## 4. Principios rectores del uso responsable

| Principio | Descripción |
|-----------|-------------|
| **Transparencia** | El usuario siempre sabe que está interactuando con IA y que los resultados son preliminares. |
| **Supervisión humana** | Todo resultado de IA debe ser revisado y validado por una persona antes de usarse. |
| **Minimización de datos** | Solo se procesan los datos estrictamente necesarios (fotogramas del clip). |
| **No sustitución profesional** | La IA apoya al evaluador; nunca lo reemplaza. |
| **Trazabilidad** | Cada análisis registra quién lo solicitó, cuándo, con qué modelo y prompt. |
| **Consentimiento** | Solo se analizan videos de personas que dieron su consentimiento informado. |

---

## 5. Recomendaciones para uso en contextos sensibles

Si la aplicación se usa en entornos clínicos, educativos o con menores de edad:

1. Obtener consentimiento informado por escrito de los participantes antes de grabar o analizar cualquier video.
2. Anonimizar o desenfocar rostros antes de subir el video a la herramienta.
3. No usar el análisis de IA como único criterio para tomar decisiones sobre personas.
4. Establecer un protocolo de revisión humana obligatoria antes de archivar o compartir cualquier resultado.
5. Consultar con el departamento de protección de datos de la institución antes de usar en producción.
6. Revisar la normativa aplicable (LFPDPPP en México).

---

## 6. Conclusión

ClipMind fue diseñado con privacidad y ética como restricciones de diseño, no como características adicionales. La tecnología sirve al proceso humano de evaluación y revisión; nunca lo sustituye ni lo automatiza. El evaluador humano es siempre el responsable final de cualquier decisión tomada a partir del material analizado.

---

*Documento elaborado como parte de los entregables del proyecto final*
