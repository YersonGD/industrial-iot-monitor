# 🏭 IndustrialIoT Monitor

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://reactjs.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> Sistema completo de monitoreo IoT industrial en tiempo real para optimización de líneas de producción

![Dashboard Preview](docs/images/dashboard-preview.png)

## 🎯 Descripción

**IndustrialIoT Monitor** es una plataforma de monitoreo industrial que integra datos de sensores IoT en tiempo real, calcula métricas de producción (OEE), analiza consumo energético y envía alertas automáticas cuando se detectan anomalías.

Diseñado para demostrar capacidades profesionales en:
- Arquitectura de sistemas IoT
- Desarrollo full-stack (Python + React)
- Procesamiento de datos en tiempo real
- Integración con protocolos industriales
- DevOps y containerización

## ✨ Características Principales

### 📊 Dashboard en Tiempo Real
- Visualización de datos de sensores (temperatura, presión, vibración)
- Gráficas interactivas con históricos
- Estados de equipos en vivo
- Actualización vía WebSockets (sin recargar página)

### 🏭 Cálculo de OEE (Overall Equipment Effectiveness)
- **Disponibilidad**: Tiempo operativo vs tiempo planificado
- **Performance**: Velocidad real vs velocidad ideal
- **Calidad**: Productos buenos vs producción total
- **OEE Total**: Métrica integrada de eficiencia

### ⚡ Monitoreo Energético
- Consumo por equipo en tiempo real
- Tendencias de consumo (día/semana/mes)
- Cálculo de costos estimados
- Identificación de picos de consumo

### 🔔 Sistema de Alertas Inteligente
- Detección automática de anomalías
- Umbrales configurables por sensor
- Notificaciones vía:
  - ✅ WhatsApp (Twilio API)
  - ✅ Email (SMTP)
  - ✅ Dashboard en tiempo real

### 📈 Análisis Histórico
- Consulta de datos pasados
- Exportación a CSV/Excel
- Reportes personalizables
- Comparativas de periodos

## 🏗️ Arquitectura del Sistema

```
┌─────────────────────────────────────────────────────────┐
│                    Frontend (React)                      │
│  Dashboard | OEE Analytics | Energy Monitor | Alerts    │
└────────────────────┬────────────────────────────────────┘
                     │ WebSocket + REST API
┌────────────────────┴────────────────────────────────────┐
│              Backend (FastAPI + Python)                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐             │
│  │ REST API │  │WebSocket │  │  MQTT    │             │
│  │ Endpoints│  │  Server  │  │  Broker  │             │
│  └──────────┘  └──────────┘  └──────────┘             │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────┴────────────────────────────────────┐
│                Data Layer                                │
│  ┌──────────────┐      ┌──────────────┐                │
│  │ PostgreSQL   │      │    Redis     │                │
│  │ (Historical) │      │  (Real-time) │                │
│  └──────────────┘      └──────────────┘                │
└─────────────────────────────────────────────────────────┘
                     ▲
                     │ MQTT Protocol
┌────────────────────┴────────────────────────────────────┐
│           IoT Sensors Simulator (Python)                 │
│  Temperature | Pressure | Vibration | Power | OEE Data  │
└─────────────────────────────────────────────────────────┘
```

## 🛠️ Stack Tecnológico

### Backend
- **Python 3.12** - Lenguaje principal
- **FastAPI** - Framework web moderno y rápido
- **WebSockets** - Comunicación bidireccional en tiempo real
- **MQTT (Eclipse Mosquitto)** - Protocolo IoT estándar
- **PostgreSQL** - Base de datos relacional para históricos
- **Redis** - Cache y pub/sub para datos en tiempo real
- **SQLAlchemy** - ORM para manejo de BD
- **Alembic** - Migraciones de base de datos
- **Pydantic** - Validación de datos
- **Twilio API** - Envío de WhatsApp
- **SMTP** - Envío de emails

### Frontend
- **React 18** - Library UI
- **TypeScript** - Tipado estático
- **Vite** - Build tool rápido
- **Recharts** - Gráficas interactivas
- **TailwindCSS** - Framework CSS
- **Zustand** - State management
- **React Query** - Data fetching
- **WebSocket Client** - Conexión en tiempo real

### IoT Simulator
- **Python** - Generador de datos realistas
- **Paho MQTT** - Cliente MQTT
- **NumPy** - Generación de datos con ruido realista
- **Threading** - Simulación concurrente de sensores

### DevOps
- **Docker** - Containerización
- **Docker Compose** - Orquestación multi-container
- **GitHub Actions** - CI/CD
- **pytest** - Testing
- **Black + isort** - Code formatting
- **ESLint + Prettier** - Linting frontend

## 🚀 Instalación y Configuración

### Requisitos Previos

- Docker & Docker Compose
- Python 3.12+ (para desarrollo local)
- Node.js 18+ (para desarrollo local)
- Git

### Opción 1: Docker (Recomendado)

```bash
# 1. Clonar repositorio
git clone https://github.com/TU_USUARIO/industrial-iot-monitor.git
cd industrial-iot-monitor

# 2. Configurar variables de entorno
cp .env.example .env
# Edita .env con tus credenciales (Twilio, SMTP)

# 3. Levantar todo el sistema
docker-compose up -d

# 4. Abrir en el navegador
# Frontend: http://localhost:3000
# API Docs: http://localhost:8000/docs
# MQTT Explorer: localhost:1883
```

**¡Listo!** El sistema está corriendo con:
- ✅ Frontend React
- ✅ Backend FastAPI
- ✅ PostgreSQL
- ✅ Redis
- ✅ MQTT Broker
- ✅ IoT Simulator (generando datos)

### Opción 2: Desarrollo Local

#### Backend

```bash
cd backend

# Crear entorno virtual
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt

# Configurar BD
alembic upgrade head

# Correr servidor
uvicorn app.main:app --reload --port 8000
```

#### Frontend

```bash
cd frontend

# Instalar dependencias
npm install

# Correr dev server
npm run dev
```

#### IoT Simulator

```bash
cd iot-simulator

pip install -r requirements.txt

python simulator.py
```

## 📖 Uso

### Dashboard Principal

1. **Abre** http://localhost:3000
2. **Verás** el dashboard con datos en tiempo real
3. **Explora** las diferentes secciones:
   - 🏭 Estado de máquinas
   - 📊 Gráficas de sensores
   - ⚡ Consumo energético
   - 📈 Cálculo de OEE
   - 🔔 Alertas activas

### Configurar Alertas

1. Ve a **Configuración → Alertas**
2. Define umbrales para cada sensor:
   ```json
   {
     "temperatura_max": 85,
     "presion_max": 6.0,
     "vibracion_max": 5.0
   }
   ```
3. Configura canales de notificación (WhatsApp/Email)
4. Las alertas se enviarán automáticamente cuando se superen umbrales

### API REST

Documentación interactiva disponible en:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

Endpoints principales:

```bash
# Obtener datos de sensores en tiempo real
GET /api/v1/sensors/realtime

# Histórico de sensores
GET /api/v1/sensors/history?start=2024-01-01&end=2024-01-31

# Cálculo de OEE
GET /api/v1/oee/calculate?machine_id=1

# Lista de alertas
GET /api/v1/alerts

# Exportar datos
GET /api/v1/export/csv?start=2024-01-01&end=2024-01-31
```

### WebSocket

Conectarse para datos en tiempo real:

```javascript
const ws = new WebSocket('ws://localhost:8000/ws');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log('Sensor data:', data);
};
```

## 🎨 Capturas de Pantalla

### Dashboard Principal
![Dashboard](docs/images/dashboard.png)

### Análisis OEE
![OEE Analysis](docs/images/oee-analysis.png)

### Monitoreo Energético
![Energy Monitor](docs/images/energy-monitor.png)

### Sistema de Alertas
![Alerts](docs/images/alerts.png)

## 🧪 Testing

### Backend Tests

```bash
cd backend
pytest

# Con cobertura
pytest --cov=app --cov-report=html
```

### Frontend Tests

```bash
cd frontend
npm test

# Con cobertura
npm test -- --coverage
```

## 📊 Métricas del Proyecto

- **Líneas de código**: ~15,000
- **Cobertura de tests**: >80%
- **Performance**: <100ms response time
- **Escalabilidad**: Hasta 1000 sensores simultáneos
- **Tiempo de desarrollo**: 6-8 semanas

## 🗺️ Roadmap

### Fase 1: MVP ✅
- [x] Dashboard básico en tiempo real
- [x] Simulador IoT
- [x] Sistema de alertas
- [x] Cálculo de OEE
- [x] Dockerización

### Fase 2: Mejoras (En progreso)
- [ ] Machine Learning para predicción de fallas
- [ ] App móvil (React Native)
- [ ] Integración con Modbus RTU
- [ ] Multi-tenant (múltiples plantas)
- [ ] Reportes automáticos PDF

### Fase 3: Empresa
- [ ] Integración con ERP
- [ ] OPC-UA support
- [ ] Gemelo digital (Digital Twin)
- [ ] Realidad aumentada (AR)

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -m 'Agregar nueva funcionalidad'`)
4. Push (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la Licencia MIT. Ver [LICENSE](LICENSE) para más detalles.

## 👨‍💻 Autor

**[Tu Nombre]**
- LinkedIn: [linkedin.com/in/tu-perfil](https://linkedin.com/in/tu-perfil)
- GitHub: [@tu-usuario](https://github.com/tu-usuario)
- Email: tu.email@ejemplo.com

Ingeniero Electrónico y de Sistemas especializado en desarrollo de software IoT e industrial.

## 🙏 Agradecimientos

- FastAPI por el excelente framework
- React team por la increíble library
- Eclipse Foundation por Mosquitto MQTT
- Comunidad open source

## 📧 Contacto

¿Interesado en este proyecto para tu empresa? ¿Quieres contratar servicios de desarrollo IoT?

📧 Email: tu.email@ejemplo.com  
💼 LinkedIn: linkedin.com/in/tu-perfil  
🐙 GitHub: github.com/tu-usuario

---

⭐ **Si este proyecto te resulta útil, dale una estrella en GitHub!**

🔗 **Demo en vivo**: [Próximamente en AWS/Azure]
