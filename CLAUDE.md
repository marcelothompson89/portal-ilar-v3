# Portal ILAR v3

Portal web de dashboards para la Asociaci&oacute;n Latinoamericana de Autocuidado Responsable (ILAR). Analiza regulaciones de suplementos alimenticios, mol&eacute;culas y otras sustancias en Am&eacute;rica Latina.

## Stack

- **Backend:** FastAPI + Uvicorn (Python)
- **Frontend:** Jinja2 templates con CSS/JS inline
- **Datos:** Pandas (CSV/Excel), sin base de datos relacional
- **Auth:** Supabase (con modo desarrollo fallback: `admin@test.com` / `password123`)
- **Excel:** openpyxl + Pillow (lectura y exportaci&oacute;n con formato)

## Ejecutar

```bash
# Activar venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Linux/Mac

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar
python main.py
# -> http://localhost:8000
```

Requiere archivo `.env` con `SUPABASE_URL` y `SUPABASE_KEY` (opcional, sin ellos usa modo desarrollo).

## Estructura del proyecto

```
portal-ilar-v3/
├── main.py                               # App principal FastAPI (~1570 l&iacute;neas)
├── regulatory_data.py                    # Datos regulatorios por pa&iacute;s (~717 l&iacute;neas)
├── requirements.txt                      # Dependencias Python
├── .env                                  # Variables de entorno (Supabase)
├── templates/
│   ├── login.html                        # P&aacute;gina de login
│   ├── dashboard.html                    # Dashboard principal (landing)
│   ├── molecules_dashboard.html          # Dashboard de mol&eacute;culas
│   └── suplementos_dashboard.html        # Dashboard de suplementos (principal)
├── static/images/
│   ├── logo-ilar.png                     # Logo ILAR
│   ├── banner-suplementos.png            # Banner suplementos
│   ├── banner-moleculas.png              # Banner mol&eacute;culas
│   └── panel-control.png                 # Imagen panel de control
├── suplementos_normalizados_completo.csv # Datos suplementos
├── referencias_suplementos_vitaminas.csv # Referencias vitaminas
├── referencias_suplementos_minerales.csv # Referencias minerales
├── moleculas_sin_duplicados_2025.xlsx    # Datos mol&eacute;culas
├── otras_substancias_ilar.xlsx           # Otras sustancias
└── docs_en_act_reg_cons_pub.xlsx         # Actualizaci&oacute;n regulatoria
```

## Rutas principales

| Ruta | Descripci&oacute;n |
|------|-------------|
| `GET /` | Login |
| `GET /dashboard` | Dashboard principal |
| `GET /dashboard/molecules` | Dashboard mol&eacute;culas |
| `GET /dashboard/suplementos` | Dashboard suplementos |

## APIs de datos

| Endpoint | Descripci&oacute;n |
|----------|-------------|
| `GET /api/suplementos-initial` | Datos iniciales suplementos |
| `GET /api/suplementos-analysis` | An&aacute;lisis filtrado con paginaci&oacute;n |
| `GET /api/suplementos-comparison` | Comparaci&oacute;n regulatoria entre pa&iacute;ses |
| `GET /api/suplementos-categories` | Categor&iacute;as regulatorias disponibles |
| `GET /api/otras-sustancias-initial` | Datos iniciales otras sustancias |
| `GET /api/otras-sustancias-analysis` | An&aacute;lisis otras sustancias |
| `GET /api/actualizacion-regulatoria-initial` | Datos actualizaci&oacute;n regulatoria |
| `GET /api/actualizacion-regulatoria-analysis` | An&aacute;lisis actualizaci&oacute;n regulatoria |
| `GET /api/molecules-data` | Datos de mol&eacute;culas |

## APIs de exportaci&oacute;n (Excel con formato)

| Endpoint | Archivo generado |
|----------|-----------------|
| `GET /api/suplementos-export-analysis` | `suplementos_analisis_YYYY-MM-DD.xlsx` |
| `GET /api/suplementos-export-comparison` | `suplementos_comparacion_YYYY-MM-DD.xlsx` |
| `GET /api/otras-sustancias-export` | `otras_sustancias_YYYY-MM-DD.xlsx` |

Las exportaciones usan la funci&oacute;n `create_branded_excel()` que genera archivos Excel con encabezado (t&iacute;tulo, subt&iacute;tulo, logos ILAR), tabla formateada con colores de marca (#2D4A65 azul, #8BA873 verde), filas alternadas y frozen panes.

## Carga de datos

Los datos se cargan al inicio en cach&eacute; global (`load_data_cache` en `@app.on_event("startup")`). Si los archivos CSV/Excel no existen, se generan datos de ejemplo autom&aacute;ticamente.

## Colores de marca

- Azul oscuro: `#2D4A65`
- Verde: `#8BA873`
- Fondo alterno: `#F8F9FA`
