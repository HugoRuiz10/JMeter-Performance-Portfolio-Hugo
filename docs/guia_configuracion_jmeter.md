# Guía de instalación y configuración de Apache JMeter

> Rellena los campos entre {{ }} con tus datos.

## 1) Prerrequisitos
- Java 8+ instalado (recomendado Java 11 o 17).
- 2–4 GB de RAM disponibles.
- Acceso de red al entorno bajo prueba (si aplica).

## 2) Instalar JMeter (Windows/Mac/Linux)
1. Descarga JMeter: https://jmeter.apache.org/download_jmeter.cgi
2. Descomprime el .zip en una carpeta (ej: C:\tools\jmeter o /opt/jmeter).
3. Ejecuta:
   - Windows: `bin/jmeter.bat`
   - Mac/Linux: `bin/jmeter`

## 3) Plugins útiles (opcionales)
- Custom Thread Groups
- JSON Plugins
Instalación con JMeter Plugins Manager:
1. Descarga `JMeterPlugins-Manager.jar` y colócalo en `JMETER_HOME/lib/ext/`.
2. Abre JMeter → `Options > Plugins Manager` → instala los que necesites.

## 4) Estructura recomendada del proyecto
```
test-plans/
  login.jmx
  authorization.jmx
  get_consultar_valores.jmx
  post_insertar_valores.jmx
  put_update_valores.jmx
  patch_actualizar_tarifa.jmx
  plan_general.jmx
data/
  users.csv
results/
docs/
assets/
```

## 5) Variables base
En **User Defined Variables** o en **HTTP Request Defaults** define:
- `BASE_URL` = `https://api.demo-server.com`
- `CONTENT_TYPE` = `application/json`

En consola puedes sobreescribirlas con: `-JBASE_URL=https://api.tu-entorno.com`

## 6) Buenas prácticas de configuración
- Usa `HTTP Request Defaults` para centralizar host/puerto/protocolo.
- Usa `CSV Data Set Config` para usuarios/IDs de prueba.
- Añade `Assertions` (Código 200, JSON Path, etc.).
- Añade `View Results Tree` solo en desarrollo (no en ejecución de carga).
