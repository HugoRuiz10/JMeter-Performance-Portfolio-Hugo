# Manual de ejecución de pruebas (paso a paso)

## A) Ejecutar desde la interfaz (GUI)
1. Abre JMeter (`bin/jmeter`).
2. `File > Open` y selecciona el plan (`plan_general.jmx` o el servicio individual).
3. En el **Thread Group** ajusta:
   - `Number of Threads (users)`
   - `Ramp-up period (s)`
   - `Duration` (si aplica)
4. Configura variables en `User Defined Variables` (ej.: `BASE_URL`, `USERNAME`, `PASSWORD`).
5. Ejecuta con el botón **Start** (▶) y revisa **Listeners** (en pruebas cortas).

## B) Ejecutar en modo no GUI (recomendado para carga)
Genera resultados `.jtl` y el dashboard HTML:

```bash
jmeter -n -t test-plans/plan_general.jmx -l results/plan_general.jtl -e -o results/plan_general_dashboard -JBASE_URL=https://api.demo-server.com
```

- `-n` no GUI
- `-t` plan de prueba
- `-l` archivo de resultados JTL
- `-e -o` genera reporte HTML en la carpeta indicada
- `-JVAR=valor` sobreescribe variables del test

## C) Exportar a PDF
1. Abre `results/plan_general_dashboard/index.html` en el navegador.
2. `Imprimir > Guardar como PDF` (elige “Ajustar a página”).

## D) Ejecución de un servicio individual (ej.: GET)
```bash
jmeter -n -t test-plans/get_consultar_valores.jmx -l results/get_consultar_valores.jtl -e -o results/get_consultar_valores_dashboard -JBASE_URL=https://api.demo-server.com
```

## E) Limpieza de listeners
Antes de correr carga pesada, desactiva o elimina:
- `View Results Tree`
- `View Results in Table`
- Deja **Summary Report** o solo genera el Dashboard (con `-e -o`).

## F) Tokens: extracción y uso (paso a paso)
1. **Login (HTTP Request)** → envía usuario/clave (JSON).
2. Añade **JSON Extractor** como *Post-Processor* al login:
   - Variable Name: `auth_token`
   - JSONPath: `$..access_token` (ajusta al campo real de tu respuesta)
   - Default Value: `NO_TOKEN`
3. En los demás requests agrega **HTTP Header Manager** con:
   - `Authorization` = `Bearer ${auth_token}`
4. Opcional: **If Controller** para validar `auth_token != NO_TOKEN`.
