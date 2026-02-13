# 🏭 IndustrialIoT Monitor

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://reactjs.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> Sistema completo de monitoreo IoT industrial en tiempo real para optimización de líneas de producción

**Desarrollado por:** [Yerson Garcia Dias](https://github.com/YersonGD)  
**Universidad:** Universidad Nacional del Callao (UNAC)  
**Contacto:** [yerdiaz784@gmail.com](mailto:yerdiaz784@gmail.com)

![Dashboard Preview](docs/images/dashboard-preview.png)

## 🎯 Descripción

**IndustrialIoT Monitor** es una plataforma de monitoreo industrial que integra datos de sensores IoT en tiempo real, calcula métricas de producción (OEE), analiza consumo energético y envía alertas automáticas cuando se detectan anomalías.

Este proyecto demuestra capacidades profesionales en:
- ✅ Arquitectura de sistemas IoT industriales
- ✅ Desarrollo full-stack (Python Backend + React Frontend)
- ✅ Procesamiento de datos en tiempo real con WebSockets
- ✅ Integración con protocolos industriales (MQTT)
- ✅ DevOps y containerización con Docker

## ✨ Características Principales

### 📊 Dashboard en Tiempo Real
- Visualización de sensores: temperatura, presión, vibración, consumo energético
- Gráficas interactivas con históricos
- Estados de equipos actualizados en vivo
- Comunicación bidireccional vía WebSockets

### 🏭 Cálculo de OEE (Overall Equipment Effectiveness)
- **Disponibilidad**: Tiempo operativo vs planificado
- **Performance**: Velocidad real vs ideal
- **Calidad**: Productos buenos vs total
- **OEE Total**: Métrica integrada de eficiencia

### ⚡ Monitoreo Energético
- Consumo por equipo en tiempo real
- Análisis de tendencias (día/semana/mes)
- Cálculo de costos estimados
- Detección de picos de consumo

### 🔔 Sistema de Alertas Inteligente
- Detección automática de anomalías
- Umbrales configurables por sensor
- Notificaciones multi-canal:
  - ✅ WhatsApp (Twilio API)
  - ✅ Email (SMTP)
  - ✅ Dashboard en tiempo real

### 📈 Análisis Histórico
- Consulta de datos pasados con filtros avanzados
- Exportación a CSV/Excel
- Reportes personalizables
- Comparativas entre periodos

## 🏗️ Arquitectura del Sistema

```
┌──────────────────────────────────────────────────────┐
│              Frontend (React + TypeScript)           │
│   Dashboard | OEE Analytics | Energy | Alerts        │
└────────────────────┬─────────────────────────────────┘
                     │ WebSocket + REST API
┌────────────────────┴─────────────────────────────────┐
│           Backend (FastAPI + Python 3.12)            │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐            │
│  │ REST API │  │WebSocket │  │  MQTT    │            │
│  │ Endpoints│  │  Server  │  │  Client  │            │
│  └──────────┘  └──────────┘  └──────────┘            │
└────────────────────┬─────────────────────────────────┘
                     │
┌────────────────────┴─────────────────────────────────┐
│              Data Layer                              │
│  ┌──────────────┐      ┌──────────────┐              │
│  │ PostgreSQL   │      │    Redis     │              │
│  │ (Historical) │      │  (Real-time) │              │
│  └──────────────┘      └──────────────┘              │
└──────────────────────────────────────────────────────┘
                     ▲
                     │ MQTT Protocol
┌────────────────────┴─────────────────────────────────┐
│        IoT Sensors Simulator (Python)                │
│  Temperature | Pressure | Vibration | Power | OEE    │
└──────────────────────────────────────────────────────┘
```

## 🛠️ Stack Tecnológico

### Backend
- **Python 3.12** - Lenguaje principal
- **FastAPI** - Framework web moderno con validación automática
- **WebSockets** - Comunicación bidireccional en tiempo real
- **MQTT (Mosquitto)** - Protocolo IoT estándar industrial
- **PostgreSQL** - Base de datos relacional
- **Redis** - Cache y pub/sub para tiempo real
- **SQLAlchemy** - ORM
- **Alembic** - Migraciones de BD
- **Pydantic** - Validación de datos
- **Twilio API** - Notificaciones WhatsApp
- **SMTP** - Notificaciones Email

### Frontend
- **React 18** - Library UI
- **TypeScript** - Tipado estático
- **Vite** - Build tool
- **Recharts** - Gráficas interactivas
- **TailwindCSS** - Framework CSS
- **Zustand** - State management
- **React Query** - Data fetching
- **WebSocket Client** - Tiempo real

### IoT Simulator
- **Python** - Generador de datos
- **Paho MQTT** - Cliente MQTT
- **NumPy** - Datos con ruido realista
- **Threading** - Simulación concurrente

### DevOps
- **Docker** - Containerización
- **Docker Compose** - Orquestación
- **GitHub Actions** - CI/CD
- **pytest** - Testing backend
- **Jest** - Testing frontend

## 🚀 Instalación y Configuración

### Requisitos Previos

- Docker & Docker Compose
- Python 3.12+ (desarrollo local)
- Node.js 18+ (desarrollo local)
- Git

### Quick Start con Docker (Recomendado)

```bash
# 1. Clonar repositorio
git clone https://github.com/YersonGD/industrial-iot-monitor.git
cd industrial-iot-monitor

# 2. Configurar variables de entorno
cp .env.example .env
# Edita .env con tus credenciales (Twilio, SMTP)

# 3. Levantar todo el sistema
docker-compose up -d

# 4. Acceder a la aplicación
# Frontend: http://localhost:3000
# API Docs: http://localhost:8000/docs
# MQTT: localhost:1883
```

**¡Listo!** El sistema completo está corriendo con todos los servicios.

### Desarrollo Local

Ver documentación completa en [GETTING_STARTED.md](GETTING_STARTED.md)

## 📖 Uso

### Dashboard Principal

1. Abre http://localhost:3000
2. Visualiza datos en tiempo real
3. Explora módulos:
   - 🏭 Estado de máquinas
   - 📊 Gráficas de sensores
   - ⚡ Consumo energético
   - 📈 OEE Analytics
   - 🔔 Alertas

### API REST

Documentación interactiva: http://localhost:8000/docs

**Endpoints principales:**

```bash
# Datos en tiempo real
GET /api/v1/sensors/realtime

# Histórico
GET /api/v1/sensors/history?start=2024-01-01&end=2024-01-31

# Cálculo OEE
GET /api/v1/oee/calculate?machine_id=1

# Alertas
GET /api/v1/alerts

# Exportar datos
GET /api/v1/export/csv
```

### WebSocket

```javascript
const ws = new WebSocket('ws://localhost:8000/ws');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log('Sensor data:', data);
};
```

## 🧪 Testing

```bash
# Backend
cd backend
pytest --cov=app

# Frontend
cd frontend
npm test -- --coverage
```

## 📊 Métricas del Proyecto

- **Líneas de código**: ~15,000
- **Cobertura tests**: >80%
- **Performance**: <100ms response time
- **Escalabilidad**: Hasta 1000 sensores simultáneos

## 🗺️ Roadmap

### ✅ Fase 1: MVP Completado
- [x] Dashboard en tiempo real
- [x] Simulador IoT
- [x] Sistema de alertas
- [x] Cálculo de OEE
- [x] Dockerización

### 🚧 Fase 2: En Desarrollo
- [ ] Machine Learning (predicción de fallas)
- [ ] App móvil (React Native)
- [ ] Integración Modbus RTU
- [ ] Multi-tenant
- [ ] Reportes PDF automáticos

### 📅 Fase 3: Futuro
- [ ] Integración con ERP
- [ ] OPC-UA support
- [ ] Gemelo digital (Digital Twin)
- [ ] Realidad aumentada (AR)

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Si tienes ideas o mejoras:

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -m 'Agregar funcionalidad X'`)
4. Push (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la Licencia MIT. Ver [LICENSE](LICENSE) para detalles.

## 👨‍💻 Autor

**Yerson Garcia Dias**

Estudiante de Ingeniería Electrónica y de Sistemas (8vo ciclo)  
Universidad Nacional del Callao (UNAC) - Lima, Perú

- 📧 Email: [yerdiaz784@gmail.com](mailto:yerdiaz784@gmail.com)
- 💼 LinkedIn: [linkedin.com/in/yerson-garcia-dias-4996912a9](https://www.linkedin.com/in/yerson-garcia-dias-4996912a9/)
- 🐙 GitHub: [@YersonGD](https://github.com/YersonGD)

### Certificaciones:
- CCNA CISCO Switching y Wireless
- Ansible: Automatización de TI + IA
- English for IT 2 (B2 Técnico)

### Áreas de Especialización:
- Desarrollo de Software IoT
- Automatización Industrial
- Sistemas Embebidos
- Cloud Computing (AWS/Azure)
- DevOps & Containerización

## 🙏 Agradecimientos

- FastAPI por el excelente framework
- React team por la librería
- Eclipse Foundation por Mosquitto MQTT
- Comunidad open source

---

⭐ **Si este proyecto te resulta útil, dale una estrella en GitHub!**

📧 **Interesado en colaborar o contratar servicios de desarrollo IoT?**  
Contacto: [yerdiaz784@gmail.com](mailto:yerdiaz784@gmail.com)

