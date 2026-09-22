# Curso de IA en Digestivo · SEPD · 2ª edición (2026-2027)

Web estática con una ficha por sesión del curso. Sin dependencias: HTML + CSS + JS vanilla.

## Estructura

```
sitio/sepd-curso/
├── index.html              Portada: programa (8 módulos), equipo docente, cómo funciona
├── modulo-1.html           Ficha del Módulo 1 · Fundamentos de IA
├── plantilla-modulo.html   Plantilla para los módulos 2-8 (textos entre [corchetes])
├── README.md
└── assets/
    ├── sepd.css            Estilos compartidos (paleta SEPD: morado #5503B1 · naranja #FFA52B)
    ├── sepd.png            Logo SEPD
    ├── curso-logo.png      Logo "IA Generativa Digestiva"
    ├── equipo/             Retratos del equipo docente
    └── m1/                 Recursos del Módulo 1
        ├── portada.jpg, mapa.jpg, slide-*.jpg     Diapositivas clave (renderizadas del PDF)
        ├── presentacion-sesion-1.pdf              Presentación completa (35 MB)
        ├── PracticaIA_SEPD_Modulo1_alumnos.zip    Material de la práctica SIN la hoja de claves
        └── muestra-kvasir.jpg                     Mosaico de imágenes Kvasir-SEG
```

## Añadir un módulo nuevo

1. Copia `plantilla-modulo.html` como `modulo-N.html` y rellena los `[corchetes]`.
2. Crea `assets/mN/` con la portada, las diapositivas clave y los materiales descargables.
   Para renderizar diapositivas de un PDF sin capa de texto:
   ```bash
   python3 -c "import fitz; d=fitz.open('sesion.pdf'); p=d[PAGINA-1]; p.get_pixmap(matrix=fitz.Matrix(1280/p.rect.width,1280/p.rect.width)).save('assets/mN/slide-nombre.png')"
   ```
3. En `index.html`, convierte la tarjeta del módulo en enlace: cambia `<div class="module module--soon">` por
   `<a class="module" href="modulo-N.html">` y la etiqueta `Próximamente` por `Ficha disponible`.
4. Actualiza el bloque `pager` (anterior / siguiente) de la ficha previa.

Secciones de cada ficha (ids fijos para que funcione el índice lateral): `resumen`, `ideas`, `recorrido`,
`diapositivas` (opcional), `herramientas`, `practica`, `reglas` (opcional), `preguntas`, `glosario`,
`autoevaluacion`, `referencias` (opcional), `siguiente`.

## Previsualizar en local

```bash
python3 -m http.server 8791 --directory sitio/sepd-curso
```

y abre <http://localhost:8791>. También se puede abrir `index.html` directamente en el navegador.

## Notas

- Las etiquetas de herramientas usan `pill--ok` (gratis), `pill--warn` (freemium), `pill--bad` (pago / no disponible),
  `pill--purple` (módulo en que se trabaja), `pill--orange` (práctica), `pill--grey` (otros).
- Las respuestas correctas del cuestionario van en `data-answer` de cada `.q`; los textos de feedback en `data-ok` / `data-ko`.
- El zip de la práctica publicado excluye `CLAVES_solo_profesor.csv`. El original está en `~/Desktop/SEPD Sesión I/`.
