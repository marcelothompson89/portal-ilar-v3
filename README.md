# Portal de Dashboards con FastAPI y Supabase

Un portal web seguro para acceder a dashboards de análisis de datos, con autenticación mediante Supabase y conversión de dashboards Streamlit a FastAPI.

## 🚀 Características

- ✅ **Autenticación segura** con Supabase
- ✅ **Dashboard de Moléculas ILAR** con filtros interactivos
- ✅ **Diseño responsive** y moderno
- ✅ **Sistema de sesiones** para proteger contenido
- ✅ **Carga de datos desde Excel** automática
- ✅ **API REST** para datos filtrados

## 📁 Estructura del Proyecto

```
proyecto/
├── main.py                          # Servidor FastAPI principal
├── requirements.txt                 # Dependencias de Python
├── .env.example                     # Variables de entorno (ejemplo)
├── .env                            # Variables de entorno (crear)
├── README.md                       # Este archivo
├── Version final Extracto base de datos Mar 2023.xlsx  # Tu archivo de datos
├── templates/                      # Plantillas HTML
│   ├── login.html                 # Página de login
│   ├── dashboard.html             # Dashboard principal
│   └── molecules_dashboard.html   # Dashboard de moléculas
└── static/                        # Archivos estáticos (opcional)
    ├── css/
    ├── js/
    └── images/
```

## 🛠️ Instalación

### 1. Clonar o crear el proyecto

```bash
# Crear directorio del proyecto
mkdir portal-dashboards
cd portal-dashboards

# Crear estructura de carpetas
mkdir templates static
mkdir static/css static/js static/images
```

### 2. Configurar entorno virtual de Python

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno virtual
# En Windows:
venv\Scripts\activate
# En macOS/Linux:
source venv/bin/activate
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 4. Configurar Supabase

1. **Crear proyecto en Supabase:**
   - Ve a [https://supabase.com](https://supabase.com)
   - Crea una cuenta y un nuevo proyecto
   - Espera a que se complete la configuración

2. **Configurar autenticación:**
   - En tu dashboard de Supabase, ve a Authentication → Settings
   - Habilita Email authentication si no está habilitado
   - Opcionalmente configura otros providers (Google, GitHub, etc.)

3. **Crear usuarios de prueba:**
   - Ve a Authentication → Users
   - Crea algunos usuarios de prueba con email y contraseña

4. **Obtener credenciales:**
   - Ve a Settings → API
   - Copia la **URL** del proyecto
   - Copia la **anon/public key**

### 5. Configurar variables de entorno

```bash
# Copiar archivo de ejemplo
cp .env.example .env

# Editar archivo .env con tus credenciales
# Reemplaza con tus valores reales de Supabase
```

Ejemplo de archivo `.env`:
```bash
SUPABASE_URL=https://abcdefghijk.supabase.co
SUPABASE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### 6. Agregar archivo de datos

- Coloca tu archivo Excel `Version final Extracto base de datos Mar 2023.xlsx` en la raíz del proyecto
- O ajusta la ruta en `main.py` línea 44 si tienes un nombre diferente

### 7. Copiar archivos del código

Crea los siguientes archivos con el contenido proporcionado:

- `main.py` - Servidor FastAPI principal
- `templates/login.html` - Página de login
- `templates/dashboard.html` - Dashboard principal  
- `templates/molecules_dashboard.html` - Dashboard de moléculas
- `requirements.txt` - Dependencias
- `.env.example` - Ejemplo de variables de entorno

## 🚀 Ejecutar la aplicación

```bash
# Activar entorno virtual (si no está activado)
source venv/bin/activate  # o venv\Scripts\activate en Windows

# Ejecutar servidor
python main.py

# O usar uvicorn directamente
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

La aplicación estará disponible en: [http://localhost:8000](http://localhost:8000)

## 👤 Uso

1. **Acceder al portal**: Ve a `http://localhost:8000`
2. **Iniciar sesión**: Usa las credenciales de los usuarios creados en Supabase
3. **Navegar dashboards**: Una vez autenticado, accede al dashboard de moléculas
4. **Filtrar datos**: Usa los filtros para explorar los datos

## 🔧 Configuración Adicional

### Cambiar puerto del servidor

Edita el archivo `main.py` en la última línea:
```python
uvicorn.run(app, host="0.0.0.0", port=8080)  # Cambiar puerto aquí
```

### Agregar más usuarios

- Ve a tu dashboard de Supabase → Authentication → Users
- Haz clic en "Add user" y completa email/contraseña

### Personalizar datos

Si tienes un archivo Excel diferente:
1. Colócalo en la raíz del proyecto
2. Actualiza la ruta en `main.py` línea 44
3. Verifica que tenga las columnas necesarias

## 🐛 Solución de Problemas

### Error: "Archivo Excel no encontrado"
- Verifica que el archivo Excel esté en la raíz del proyecto
- Verifica el nombre exacto del archivo en `main.py`

### Error: "Credenciales de Supabase inválidas"
- Verifica que las variables `SUPABASE_URL` y `SUPABASE_KEY` estén correctas
- Asegúrate de que el proyecto de Supabase esté activo

### Error: "No se puede conectar al servidor"
- Verifica que todas las dependencias estén instaladas
- Verifica que el puerto 8000 no esté en uso por otra aplicación

### Error de autenticación
- Verifica que el usuario exista en Supabase
- Verifica que la autenticación por email esté habilitada en Supabase

## 📋 Próximos Pasos

1. **Agregar más dashboards**: Crea nuevos templates y rutas en `main.py`
2. **Mejorar diseño**: Personaliza CSS en la carpeta `static/`
3. **Agregar gráficos**: Reintegra Plotly.js para visualizaciones
4. **Base de datos**: Migra datos de Excel a PostgreSQL (Supabase)
5. **Deploy**: Despliega en Heroku, Vercel, o DigitalOcean

## 📝 Notas

- El proyecto usa datos de ejemplo si no encuentra el archivo Excel
- Las sesiones se mantienen hasta cerrar el navegador
- La aplicación es responsive y funciona en móviles
- Los filtros se aplican en tiempo real

## 🆘 Soporte

Si tienes problemas:
1. Verifica que seguiste todos los pasos de instalación
2. Revisa los logs del servidor en la consola
3. Verifica la configuración de Supabase
4. Asegúrate de que el archivo Excel tenga el formato correcto

---

**¡Listo para usar!** 🎉