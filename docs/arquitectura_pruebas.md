# Arquitectura de pruebas y diseño del plan

## 1) Componentes principales
- **Thread Group**: define concurrencia y tiempos.
- **HTTP Request Defaults**: BASE_URL/puerto/protocolo por defecto.
- **CSV Data Set Config**: datos de prueba (usuarios/IDs).
- **Login + JSON Extractor**: obtiene `auth_token` para el resto.
- **HTTP Header Manager**: `Authorization: Bearer ${auth_token}`.
- **Assertions**: verifica código 200/JSON esperado.
- **Timers**: `Constant Timer` o `Uniform Random Timer` para think-time.
- **Listeners**: usar los mínimos en carga; preferir el Dashboard HTML.

## 2) Flujo recomendado
1. **Login** → extraer `auth_token`.
2. **Servicios protegidos** (GET/POST/PUT/PATCH) con header de autorización.
3. **Validaciones** (assertions) por servicio.
4. **TearDown** si aplica (limpieza de datos de prueba).

## 3) Modularización (Include Controller)
- Un `.jmx` por servicio.
- `plan_general.jmx` que incluye a todos mediante **Include Controller**.
- Ventajas: reutilización de login, mantenimiento simple, ejecuciones parciales.

## 4) Métricas clave a reportar
- **Tiempos de respuesta**: promedio, p90, p95, p99.
- **Throughput** (req/s).
- **Error Rate** (%).
- **Concurrencia efectiva**.
- **Resource footprint** (si monitoreas host con PerfMon).

## 5) Ejemplo de SLA
- `p95 < 2.0 s` para endpoints críticos.
- `Error Rate < 1%` en pruebas de carga.
