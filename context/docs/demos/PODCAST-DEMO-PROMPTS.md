# Prompts para Demo del Podcast

> Guía de prompts listos para usar durante la demo del podcast de NexusFlow.

---

## 3.1 - Discovery Orchestrator

### Opcion A: Demo rapido (~15 min)
```
/discovery-orchestrator feature="Onboarding Simplificado" depth=quick
```

### Opcion B: Demo completo (~45 min)
```
/discovery-orchestrator feature="CRM Integration Wizard" depth=standard include-competitive=true
```

**Que mostrara:**
- Coordinacion automatica de 4 agentes especializados
- Recopilacion de contexto estrategico
- Analisis de datos cuantitativos
- Investigacion de usuarios
- Analisis competitivo
- Sintesis en un DISCOVERY_SUMMARY.md

---

## 3.3 - Dashboard de Data

### Prompt para crear dashboard desde cero:
```
Crea un dashboard HTML interactivo usando la data sintetica de NexusFlow. Incluye:

1. KPIs principales: ARR (8.2M), NRR (108%), Enterprise Churn (12.3%), Activation Rate (45%)
2. Grafico de linea: ARR trend ultimos 15 meses (context/data/business/ARR-ANALYSIS-2026.csv)
3. Grafico de barras: Churn por plan tier (Starter 8.2%, Professional 4.5%, Enterprise 12.3%)
4. Funnel: Activacion (Signup 100% -> Onboarding 78% -> CRM 52% -> Workflow 45% -> First Run 38% -> Activated 31%)
5. Pie chart: Razones de churn (Integration 28%, Features 25%, Support 22%, Adoption 19%, Pricing 16%)

Usa Chart.js. Los datos estan en context/data/
```

### Dashboards existentes (abrir directamente):
```bash
# Dashboard de churn
open context/data/churn-analysis/churn-dashboard-q1-2026.html

# Dashboard de uso de producto
open context/data/insights/Q1-2026-PRODUCT-USAGE-DASHBOARD.html

# Dashboard KPI principal (nuevo)
open context/data/dashboards/nexusflow-kpi-dashboard.html
```

---

## Archivos de Data Disponibles

| Archivo | Contenido |
|---------|-----------|
| `context/data/business/ARR-ANALYSIS-2026.csv` | 15 meses de revenue |
| `context/data/churn-analysis/churn-q1-2026.csv` | 50 cuentas churned |
| `context/data/business/REVENUE-METRICS-Q1-2026.md` | KPIs financieros |
| `context/data/churn-analysis/CHURN-ANALYSIS-Q1-2026-COMPLETE.md` | Analisis profundo |
| `context/data/insights/ACTIVATION-DROPOFF-ANALYSIS-Q1-2026.md` | Funnel de activacion |

---

## Tips para el Demo

1. **Antes de empezar**: Tener abierto VS Code con el repo
2. **Discovery**: Mostrar como coordina multiples agentes
3. **Dashboard**: Abrir en navegador para mostrar interactividad
4. **Datos**: Los CSV tienen datos sinteticos realistas

---

*Documento preparado para demo del podcast*
