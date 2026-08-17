# Libro de Análisis Matemático — Plantilla Modular LaTeX

## Descripción

Libro académico de análisis matemático, organizado en módulos separados para facilitar el mantenimiento y la colaboración. Los capítulos están numerados en el nombre de archivo (`01-...`, `02-...`), los temas fundamentales viven en cuatro apéndices (teoría de conjuntos, números reales, números complejos y álgebra lineal) y se genera un índice de palabras con `imakeidx`.

## Estructura del proyecto

```
analisis-matematico/
├── main.tex                        % Archivo maestro
├── bibliografia.bib                % Base de datos bibliografica
├── README.md                       % Este archivo
├── preambulo/
│   ├── estilos.tex                 % Geometria, tipografia, colores, encabezados
│   ├── macros.tex                  % Entornos matematicos (teoremas, definiciones...)
│   └── referencias.tex             % cleveref, hyperref, biblatex
└── contenido/
    ├── portada.tex                 % Portada interior
    ├── dedicatoria.tex             % Pagina de dedicatoria
    ├── prologo.tex                 % Prefacio / prologo
    ├── capitulos/
    │   ├── capitulo-01.tex         % Espacios métricos (fusión de métricas + topología métrica)
    │   ├── capitulo-02.tex
    │   ├── ...
    │   └── capitulo-22.tex
    └── apendices/
        ├── apendice-teoria-conjuntos.tex
        ├── apendice-numeros-reales.tex
        ├── apendice-numeros-complejos.tex
        └── apendice-algebra-lineal.tex
```

## Requisitos

- Compilador: **XeLaTeX**
- Paquete **imakeidx** (gestión del índice de palabras)
- Fuente: Latin Modern (incluida en TeX Live / MiKTeX)

## Cómo compilar por consola

Abre una terminal en la carpeta raíz del proyecto y ejecuta los comandos en orden. `imakeidx` invoca `makeindex` automáticamente al terminar cada pasada; `biber` genera la bibliografía.

### Windows (PowerShell / CMD)

```powershell
xelatex -interaction=nonstopmode main
biber main
xelatex -interaction=nonstopmode main
xelatex -interaction=nonstopmode main
```

### Linux / macOS

```bash
xelatex -interaction=nonstopmode main
biber main
xelatex -interaction=nonstopmode main
xelatex -interaction=nonstopmode main
```

### Resumen del flujo

1. `xelatex main` — Compila el documento y genera el `.bcf` y el `.idx`.
2. `biber main` — Procesa la bibliografía (`bibliografia.bib`).
3. `xelatex main` — Resuelve referencias cruzadas e índice de palabras.
4. `xelatex main` — Ajusta la numeración y el índice general finales.

## Consejos prácticos

- Si agregas un nuevo capítulo, crea el archivo `.tex` en `contenido/capitulos/` con el nombre `capitulo-NN.tex` (NN = número) y añádelo con `\input{contenido/capitulos/capitulo-NN}` en `main.tex`.
- Para añadir términos al índice de palabras usa `\index{término}` en la definición o al inicio del capítulo.
- Las referencias internas usan `\cref{etiqueta}` (teoremas, ecuaciones, secciones).
- Las ecuaciones se etiquetan con `\label{eq:nombre}` y se citan con `\cref{eq:nombre}`.
- TikZ está cargado y listo para diagramas conmutativos y figuras.

## Personalización rápida

| Elemento | Archivo | Comando clave |
|----------|---------|---------------|
| Título / autor | `main.tex` | `\title{}`, `\author{}` |
| Márgenes / formato página | `preambulo/estilos.tex` | `geometry` |
| Estilo de teoremas | `preambulo/macros.tex` | `\newtheoremstyle` |
| Nuevos comandos matemáticos | `preambulo/macros.tex` | `\newcommand` |
| Índice de palabras | `main.tex` | `imakeidx`, `\printindex` |

## Licencia

Uso académico libre. Modifícalo según las necesidades de tu proyecto.