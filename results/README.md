# Resultados y reportes

## Cómo generar el Dashboard HTML
```bash
jmeter -n -t ../test-plans/plan_general.jmx -l plan_general.jtl -e -o plan_general_dashboard -JBASE_URL=https://api.demo-server.com
```

## Convertir a PDF
1. Abre `plan_general_dashboard/index.html` en tu navegador.
2. `Imprimir > Guardar como PDF`.
3. Nombra el archivo como `report_plan_general_YYYYMMDD.pdf`.

## Convenciones de nombres
- `plan_general_YYYYMMDD.jtl`
- `plan_general_dashboard/`
- `report_plan_general_YYYYMMDD.pdf`
