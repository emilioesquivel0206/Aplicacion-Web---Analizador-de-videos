[README.md](https://github.com/user-attachments/files/27468922/README.md)
# 🎬 ClipMind — Análisis de Video con IA

> Herramienta web para subir, recortar y analizar clips de video con inteligencia artificial (Claude de Anthropic). Los resultados son **borradores preliminares revisables** que requieren validación humana.

---

## Descripción

ClipMind es una aplicación web de una sola página (HTML5 + CSS3 + JavaScript vanilla) que permite:

1. **Subir** un video desde el dispositivo local
2. **Visualizarlo** en un reproductor integrado con controles completos
3. **Seleccionar y recortar** fragmentos específicos (clips)
4. **Guardar** esos clips con nombre, descripción y metadatos
5. **Enviar** cada clip a Claude AI para obtener una evaluación estructurada
6. **Mostrar** los resultados de forma clara, revisable y exportable en JSON

---

## Aviso ético importante

Esta aplicación **no diagnostica, no toma decisiones finales y no sustituye el juicio profesional humano**. Todo análisis generado por IA es un borrador preliminar que debe ser revisado por un evaluador humano antes de utilizarse en cualquier contexto clínico, educativo o sensible.

---

## Tecnologías utilizadas

| Capa | Tecnología |
|------|-----------|
| Frontend | HTML5, CSS3, JavaScript (ES2022) |
| Video | HTML5 Video API, Canvas API |
| IA | Anthropic Claude API (claude-sonnet-4-20250514) |
| Almacenamiento | localStorage (prototipo) |
| Fuentes | Google Fonts — DM Sans + DM Mono |


---

## Requisitos

- Navegador moderno: **Chrome 90+**, Edge 90+ o Firefox 88+
- Conexión a internet (para cargar fuentes y la API de Claude)
- **API Key de Anthropic** — obtenla en [console.anthropic.com](https://console.anthropic.com)

No se requiere instalación de Node.js, npm ni ningún servidor backend. El archivo funciona directamente en el navegador.

---

## Instalación y uso

### Opción A — Uso directo (más fácil)

1. Descarga el archivo `clipanalyzer.html`
2. Ábrelo en Google Chrome o Edge 
3. Ingresa tu API key de Anthropic en la pantalla de inicio
4. ¡Listo!

### Opción B — Servir con servidor local (recomendado para desarrollo)

```bash
# Con Python (viene preinstalado en macOS y Linux)
python3 -m http.server 8080

# Con Node.js
npx serve .

# Con VS Code
# Instala la extensión "Live Server" y haz clic en "Go Live"
```

Luego abre `http://localhost:8080/clipanalyzer.html` en tu navegador.

### Opción C — Deploy en Vercel o Firebase Hosting

```bash
# Vercel (requiere cuenta gratuita en vercel.com)
npx vercel --prod

# Firebase Hosting
firebase init hosting
firebase deploy
```

---

## Configuración de variables de entorno

Para producción, crea un archivo `.env` basado en `.env.example`:

```bash
cp .env.example .env
```

Llena los valores reales en `.env`. 

---

## Flujo completo de uso

```
1. Iniciar sesión con API key
        ↓
2. Subir video (.mp4 / .mov / .webm)
        ↓
3. Abrir reproductor → seleccionar inicio y fin del clip
        ↓
4. Guardar clip con nombre y descripción
        ↓
5. Ir a "Mis Clips" → seleccionar clip → "Analizar"
        ↓
6. Claude extrae fotogramas y genera análisis estructurado (JSON)
        ↓
7. Revisar resultados → marcar revisión humana → exportar JSON
```

---

## Estructura del proyecto

```
clipmind/
├── clipanalyzer.html        # Aplicación completa (todo en un archivo)
├── README.md                # Este archivo
├── .env.example             # Variables de entorno de ejemplo
├── etica_privacidad.md      # Explicación de riesgos éticos
└── arquitectura.html        # Diagrama de arquitectura del sistema
```

---

## Atajos de teclado (Reproductor)

| Tecla | Acción |
|-------|--------|
| `Espacio` | Play / Pausa |
| `←` | Retroceder 5 segundos |
| `→` | Avanzar 5 segundos |

---

## Exportación de resultados

Cada análisis se puede exportar como JSON desde la vista de análisis. El archivo exportado incluye:

- Metadatos del clip (id, videoId, tiempos, duración)
- Resultado completo del análisis de IA
- Estado de revisión humana y notas del revisor
- Fecha de análisis y modelo utilizado
- Disclaimer de uso responsable de IA

---

## Reglas de seguridad

- No subir videos con datos sensibles de personas reales sin consentimiento
- No subir videos de menores de edad para pruebas
- No guardar API keys en el código fuente ni en repositorios públicos
- No hacer repositorios públicos con datos reales
- La IA no debe usarse para diagnóstico, decisión clínica ni evaluación definitiva

---

## Equipo

Proyecto desarrollado por Jose Emilio Esquivel García - Alumno de Universidad Tecmilenio Campus Ferrería - Matricula: Al07099820.

---

## Licencia

Proyecto académico — uso educativo únicamente.
