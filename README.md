# 🏥 Health Data Interoperability Hub

## CTS Hackathon | Realistic Hospital Management System

A health data interoperability system connecting two hospitals with different data formats:
- **Hospital A**: City General Hospital (HL7 v2 legacy system)
- **Hospital B**: Metro Medical Center (FHIR R4 modern system)
- **Hub**: Central interoperability hub with AI-powered reconciliation

## Features Added for Hackathon Demo

### Hospital Management
- 👨‍⚕️ **Doctor Dashboard**: Today's appointments, in-patient management, prescriptions
- 👩‍⚕️ **Nurse Dashboard**: Vital signs recording, medication administration, ward status
- 📅 **Appointments**: Scheduling system with time slots
- 🏥 **Hospital Simulation**: Live bed occupancy, ward management

### Interoperability
- HL7 v2 ↔ FHIR R4 format conversion
- ABHA (Ayushman Bharat Health ID) patient matching
- Consent management (ABDM-compliant)
- Audit logging

## Quick Start

### Prerequisites
- Node.js >= 18
- MongoDB >= 6

### Option 1: Automated Startup
```bash
# Run the batch file (Windows)
START_ALL_SERVICES.bat

# Or use the Node control panel
node start_all.js
# Then type 'start' to start all services
```

### Option 2: Manual Startup
```bash
# Terminal 1 - MongoDB (if not running as service)
mongod --dbpath C:\data\db

# Terminal 2 - Hospital A
cd hospital-a && npm install && npm run seed && npm start

# Terminal 3 - Hospital B
cd hospital-b && npm install && npm run seed && npm start

# Terminal 4 - Hub
cd hub && npm install && npm start

# Terminal 5 - Frontend
cd frontend && npm install && npm run dev
```

## Demo URLs

| Service | URL | Description |
|---------|-----|------------|
| Frontend | http://localhost:3000 | Main dashboard |
| Hospital A | http://localhost:5001 | HL7 API |
| Hospital B | http://localhost:5002 | FHIR API |
| Hub | http://localhost:5000 | Interop Hub |

## How to Demo

### 1. View as Different Roles
Open Hospital A or B page and use the role dropdown:
- **Hospital Admin**: Full stats, patient management
- **Doctor**: Today's appointments, write prescriptions
- **Nurse**: Record vitals, administer medications
- **Front Desk**: Schedule appointments

### 2. Patient Workflow
1. Search for a patient
2. View patient details (conditions, medications, allergies)
3. Schedule appointment
4. Admit to ward (in-patient view)
5. Record vitals (nurse role)
6. View in hospital simulation

### 3. Interoperability Demo
1. Search patient in Hospital A
2. Search same patient in Hospital B (different format)
3. Use Hub to reconcile/merge records

## API Endpoints

### Hospital A (HL7-style)
- `GET /api/patients` - List patients
- `GET /api/patients/:id` - Get patient
- `GET /api/doctors` - List doctors
- `GET /api/nurses` - List nurses
- `GET /api/appointments/today` - Today's appointments
- `GET /api/wards/summary` - Hospital bed summary
- `GET /api/admissions/active` - Current in-patients
- `GET /api/stats` - Hospital statistics

### Hospital B (FHIR R4)
- Same endpoints as Hospital A but returns FHIR bundles

### Hub
- `GET /api/patients/unified` - Unified patient search
- `POST /api/consent` - Grant consent
- `GET /api/audit` - Audit logs

## Project Structure

```
hackathon_hms/
├── hospital-a/           # Hospital A (HL7)
│   ├── models/           # DB models
│   ├── routes/          # API routes  
│   ├── data/seed.js     # Demo data
│   └── server.js        # Express server
├── hospital-b/          # Hospital B (FHIR)
│   ├── models/
│   ├── routes/
│   ├── data/seed.js
│   └── server.js
├── hub/                 # Interop Hub
│   ├── models/
│   ├── routes/
│   ├── services/
│   └── server.js
├── frontend/             # React Vite app
│   ├── src/
│   │   ├── api/       # API clients
│   │   ├── components/ # Dashboard components
│   │   └── pages/    # Page views
│   └── .env           # API URLs
└── START_ALL_SERVICES.bat
```

## Demo Data

The seed script populates:
- 10 patients per hospital
- 8 doctors
- 5 nurses
- 8 wards (~100 beds)
- 5 appointments (today)
- 5 active admissions

## Troubleshooting

### MongoDB not starting
```bash
# Check if MongoDB is installed
mongod --version

# Start MongoDB service
net start MongoDB
```

### Port already in use
```bash
# Find process using port
netstat -ano | findstr :5001

# Kill process
taskkill /PID <pid> /F
```

### API errors
```bash
# Test API
curl http://localhost:5001/health

# Check MongoDB connection
# In hospital-a folder:
node -e "require('./models/HL7Patient').countDocuments().then(c => console.log(c))"
```

## Technology Stack

- **Frontend**: React, Vite, React Router, Axios
- **Backend**: Node.js, Express, Mongoose
- **Database**: MongoDB
- **Data Formats**: HL7 v2.5, FHIR R4
- **Styling**: CSS-in-JS (inline styles)

## License
MIT - For hackathon demo purposes
