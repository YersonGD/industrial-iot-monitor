# 🚀 Guía de Inicio Rápido - IndustrialIoT Monitor

## 📋 Estructura del Proyecto Completo

```
industrial-iot-monitor/
├── backend/                    # API Backend (FastAPI + Python)
│   ├── app/
│   │   ├── api/               # Endpoints REST
│   │   │   ├── v1/
│   │   │   │   ├── sensors.py
│   │   │   │   ├── oee.py
│   │   │   │   ├── energy.py
│   │   │   │   └── alerts.py
│   │   │   └── websocket.py   # WebSocket handler
│   │   ├── core/              # Configuración
│   │   │   ├── config.py
│   │   │   └── security.py
│   │   ├── db/                # Base de datos
│   │   │   ├── base.py
│   │   │   └── session.py
│   │   ├── models/            # Modelos SQLAlchemy
│   │   │   ├── sensor.py
│   │   │   ├── machine.py
│   │   │   ├── oee_data.py
│   │   │   └── alert.py
│   │   ├── schemas/           # Pydantic schemas
│   │   │   ├── sensor.py
│   │   │   ├── oee.py
│   │   │   └── alert.py
│   │   ├── services/          # Lógica de negocio
│   │   │   ├── mqtt_service.py
│   │   │   ├── alert_service.py
│   │   │   ├── oee_calculator.py
│   │   │   └── notification_service.py
│   │   └── main.py            # Entry point
│   ├── alembic/               # Migraciones DB
│   ├── tests/
│   ├── Dockerfile
│   └── requirements.txt
│
├── frontend/                   # Frontend (React + TypeScript)
│   ├── src/
│   │   ├── components/        # Componentes reutilizables
│   │   │   ├── Dashboard/
│   │   │   │   ├── MachineCard.tsx
│   │   │   │   ├── SensorChart.tsx
│   │   │   │   └── OEEGauge.tsx
│   │   │   ├── Alerts/
│   │   │   │   └── AlertList.tsx
│   │   │   └── Layout/
│   │   │       ├── Header.tsx
│   │   │       └── Sidebar.tsx
│   │   ├── pages/             # Páginas
│   │   │   ├── Dashboard.tsx
│   │   │   ├── OEEAnalytics.tsx
│   │   │   ├── EnergyMonitor.tsx
│   │   │   ├── Alerts.tsx
│   │   │   └── Settings.tsx
│   │   ├── hooks/             # Custom hooks
│   │   │   ├── useWebSocket.ts
│   │   │   └── useSensorData.ts
│   │   ├── services/          # API calls
│   │   │   └── api.ts
│   │   ├── utils/             # Utilidades
│   │   ├── App.tsx
│   │   └── main.tsx
│   ├── Dockerfile
│   ├── package.json
│   └── tsconfig.json
│
├── iot-simulator/              # Simulador IoT
│   ├── simulator.py           # Main simulator
│   ├── machines/
│   │   ├── machine_base.py
│   │   └── production_line.py
│   ├── sensors/
│   │   ├── temperature.py
│   │   ├── pressure.py
│   │   ├── vibration.py
│   │   └── power.py
│   ├── Dockerfile
│   └── requirements.txt
│
├── mosquitto/                  # MQTT Config
│   └── config/
│       └── mosquitto.conf
│
├── docs/                       # Documentación
│   ├── images/
│   ├── architecture/
│   │   ├── system-architecture.md
│   │   └── data-flow.md
│   └── api/
│       └── endpoints.md
│
├── .github/
│   └── workflows/
│       ├── backend-tests.yml
│       └── frontend-tests.yml
│
├── docker-compose.yml          # Orquestación completa
├── .env.example                # Variables de entorno
├── .gitignore
├── README.md
└── LICENSE
```

## 🎯 Fase de Desarrollo (6-8 semanas)

### **Semana 1-2: Fundamentos**
- [x] Estructura del proyecto
- [ ] Setup de base de datos (PostgreSQL + Redis)
- [ ] MQTT Broker configurado
- [ ] Backend básico (FastAPI)
- [ ] Frontend básico (React)
- [ ] Docker Compose funcionando

### **Semana 3-4: Core Features**
- [ ] Simulador IoT completo
- [ ] WebSocket para tiempo real
- [ ] Dashboard con gráficas
- [ ] Sistema de alertas básico
- [ ] Cálculo de OEE

### **Semana 5-6: Features Avanzadas**
- [ ] Notificaciones WhatsApp
- [ ] Notificaciones Email
- [ ] Históricos y consultas
- [ ] Exportación de datos
- [ ] Configuración de umbrales

### **Semana 7-8: Polish & Deploy**
- [ ] Tests unitarios
- [ ] Tests de integración
- [ ] Documentación completa
- [ ] CI/CD con GitHub Actions
- [ ] Deploy en cloud (AWS/Azure)
- [ ] Video demo

## 🛠️ Empezar a Desarrollar

### Paso 1: Configuración Inicial

```bash
# Clonar el proyecto
git clone https://github.com/TU_USUARIO/industrial-iot-monitor.git
cd industrial-iot-monitor

# Copiar variables de entorno
cp .env.example .env

# Editar .env con tus credenciales
nano .env
```

### Paso 2: Levantar con Docker

```bash
# Construir y levantar todos los servicios
docker-compose up --build

# O en background:
docker-compose up -d

# Ver logs:
docker-compose logs -f
```

### Paso 3: Verificar que Todo Funciona

```bash
# Backend API
curl http://localhost:8000/health

# Frontend
# Abrir: http://localhost:3000

# MQTT
mosquitto_sub -h localhost -t "sensors/#"
```

### Paso 4: Desarrollo Local (Opcional)

#### Backend
```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Migraciones
alembic upgrade head

# Correr servidor
uvicorn app.main:app --reload
```

#### Frontend
```bash
cd frontend
npm install
npm run dev
```

#### IoT Simulator
```bash
cd iot-simulator
pip install -r requirements.txt
python simulator.py
```

## 📊 Implementación por Módulos

### 1️⃣ Módulo de Sensores (Prioridad Alta)

**Backend:**
```python
# backend/app/models/sensor.py
class SensorReading(Base):
    __tablename__ = "sensor_readings"
    
    id = Column(Integer, primary_key=True)
    machine_id = Column(Integer, ForeignKey("machines.id"))
    sensor_type = Column(String)  # temperature, pressure, vibration
    value = Column(Float)
    unit = Column(String)
    timestamp = Column(DateTime, default=datetime.utcnow)
```

**Frontend:**
```tsx
// frontend/src/components/Dashboard/SensorChart.tsx
import { LineChart, Line, XAxis, YAxis } from 'recharts';

export const SensorChart = ({ data, sensorType }) => {
  return (
    <LineChart data={data}>
      <Line type="monotone" dataKey="value" stroke="#8884d8" />
      <XAxis dataKey="timestamp" />
      <YAxis />
    </LineChart>
  );
};
```

**Simulator:**
```python
# iot-simulator/sensors/temperature.py
class TemperatureSensor:
    def __init__(self, base_temp=75, variance=5):
        self.base_temp = base_temp
        self.variance = variance
    
    def read(self):
        noise = np.random.normal(0, self.variance)
        return self.base_temp + noise
```

### 2️⃣ Módulo OEE (Prioridad Alta)

**Cálculo:**
```python
# backend/app/services/oee_calculator.py
def calculate_oee(machine_id, start_time, end_time):
    # Availability = Operating Time / Planned Production Time
    availability = calculate_availability(machine_id, start_time, end_time)
    
    # Performance = (Ideal Cycle Time × Total Count) / Operating Time
    performance = calculate_performance(machine_id, start_time, end_time)
    
    # Quality = Good Count / Total Count
    quality = calculate_quality(machine_id, start_time, end_time)
    
    # OEE = Availability × Performance × Quality
    oee = availability * performance * quality
    
    return {
        "oee": oee * 100,
        "availability": availability * 100,
        "performance": performance * 100,
        "quality": quality * 100
    }
```

### 3️⃣ Módulo de Alertas (Prioridad Media)

**Backend:**
```python
# backend/app/services/alert_service.py
class AlertService:
    async def check_thresholds(self, sensor_data):
        alerts = []
        
        if sensor_data.temperature > TEMP_THRESHOLD:
            alert = Alert(
                machine_id=sensor_data.machine_id,
                alert_type="temperature_high",
                message=f"Temperatura alta: {sensor_data.temperature}°C",
                severity="warning"
            )
            alerts.append(alert)
            await self.send_notifications(alert)
        
        return alerts
    
    async def send_notifications(self, alert):
        # WhatsApp
        await self.send_whatsapp(alert)
        
        # Email
        await self.send_email(alert)
```

### 4️⃣ Módulo Energético (Prioridad Media)

**Dashboard:**
```tsx
// frontend/src/pages/EnergyMonitor.tsx
export const EnergyMonitor = () => {
  const { data } = useEnergyData();
  
  return (
    <div>
      <h1>Monitoreo Energético</h1>
      
      <div className="grid grid-cols-3 gap-4">
        <EnergyCard
          title="Consumo Total"
          value={data.totalConsumption}
          unit="kWh"
        />
        <EnergyCard
          title="Costo Estimado"
          value={data.estimatedCost}
          unit="USD"
        />
        <EnergyCard
          title="Eficiencia"
          value={data.efficiency}
          unit="%"
        />
      </div>
      
      <EnergyChart data={data.history} />
    </div>
  );
};
```

## 🎥 Preparación de Demo

### Script para Demostración (5 minutos)

1. **Intro (30 seg)**
   - "Sistema de monitoreo IoT industrial en tiempo real"
   - "Tecnologías: Python, FastAPI, React, MQTT, PostgreSQL"

2. **Dashboard (1 min)**
   - Mostrar datos en tiempo real
   - Gráficas actualizándose
   - Estados de máquinas

3. **OEE Analytics (1 min)**
   - Cálculo de disponibilidad, performance, calidad
   - Métricas de producción

4. **Sistema de Alertas (1 min)**
   - Simular alerta (subir temperatura)
   - Mostrar notificación en dashboard
   - Mostrar WhatsApp/Email recibido

5. **Arquitectura (1 min)**
   - Explicar componentes del sistema
   - Mostrar docker-compose
   - Mencionar escalabilidad

6. **Código (30 seg)**
   - Mostrar un endpoint importante
   - Mencionar buenas prácticas

## 📝 Documentación para Empleadores

### En tu CV:

```markdown
## Proyecto Destacado: IndustrialIoT Monitor

Sistema completo de monitoreo IoT industrial desarrollado con Python (FastAPI), 
React, MQTT, PostgreSQL y Redis. Incluye:

- Dashboard en tiempo real con WebSockets
- Cálculo de OEE (Overall Equipment Effectiveness)
- Sistema de alertas con notificaciones WhatsApp/Email
- Arquitectura de microservicios con Docker
- CI/CD con GitHub Actions

Tecnologías: Python, FastAPI, React, TypeScript, PostgreSQL, Redis, MQTT, 
Docker, WebSockets, Twilio API

🔗 GitHub: github.com/tu-usuario/industrial-iot-monitor
🎥 Demo: youtube.com/tu-demo
```

### En LinkedIn:

```markdown
🏭 Nuevo Proyecto: Sistema de Monitoreo IoT Industrial

He desarrollado una plataforma completa para monitoreo de líneas de producción 
que demuestra:

✅ Arquitectura full-stack profesional
✅ Procesamiento de datos en tiempo real
✅ Integración con protocolos industriales (MQTT)
✅ Notificaciones automatizadas
✅ Cálculo de métricas industriales (OEE)

Diseñado para demostrar capacidades en desarrollo de software IoT 
y automatización industrial.

#IoT #IndustrialAutomation #Python #React #SoftwareEngineering

[Link al GitHub]
[Link a demo video]
```

## 🎯 Próximos Pasos

1. **Ahora mismo:**
   - [ ] Configura tu entorno con Docker
   - [ ] Familiarízate con la estructura
   - [ ] Lee la documentación de FastAPI y React

2. **Esta semana:**
   - [ ] Implementa el módulo de sensores
   - [ ] Crea el dashboard básico
   - [ ] Conecta el simulador

3. **Próximas 2 semanas:**
   - [ ] Implementa OEE
   - [ ] Sistema de alertas
   - [ ] Notificaciones

4. **Al mes:**
   - [ ] Tests completos
   - [ ] Deploy en cloud
   - [ ] Graba demo video

## 💡 Tips de Desarrollo

1. **Commits profesionales:**
   ```bash
   git commit -m "feat: Add real-time sensor data WebSocket endpoint"
   git commit -m "fix: Resolve OEE calculation bug for edge cases"
   git commit -m "docs: Update API documentation with new endpoints"
   ```

2. **Branches organizadas:**
   ```bash
   git checkout -b feature/oee-calculator
   git checkout -b feature/whatsapp-alerts
   git checkout -b fix/sensor-data-validation
   ```

3. **Issues y Milestones en GitHub:**
   - Crea issues para cada feature
   - Usa milestones para versiones
   - Documenta decisiones técnicas

---

¿Listo para empezar? 🚀

**Siguiente paso:** Configura tu entorno y corre `docker-compose up`
