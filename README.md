# 🏥 Portal Médico - Sistema de Radiografías

Bienvenido al repositorio principal del **Portal Médico**, una plataforma Full Stack diseñada para la gestión integral de pacientes, doctores, almacenamiento de estudios médicos (imágenes radiográficas/DICOM) y generación de informes.

## 🚀 Tecnologías Utilizadas

El proyecto está dividido en dos partes principales y utiliza las siguientes tecnologías modernas:

### 💻 Frontend (Cliente)
- **React 19** + **Vite** para una experiencia de usuario rápida y fluida.
- **Tailwind CSS** para un diseño moderno y 100% responsivo.
- **Stone Web Viewer** como visor DICOM profesional embebido, para manipulación y visualización avanzada de radiografías.
- **Zustand** para el manejo de estado global (ej. autenticación).
- **React Router v7** para la navegación de la aplicación.
- **Axios** para la comunicación con la API.

### ⚙️ Backend (Servidor)
- **Node.js** + **Express.js** como motor del servidor.
- **Prisma ORM** para la interacción segura y tipada con la base de datos.
- **Neon PostgreSQL** como base de datos relacional en la nube.
- **Orthanc (PACS)** como servidor especializado en almacenamiento y distribución de estudios DICOM.
- **JWT (JSON Web Tokens)** y **Bcrypt** para un sistema de autenticación robusto y seguro.
- **Proxy Inverso Seguro** para servir imágenes de Orthanc mediante tokens dinámicos temporales.

---

## 📁 Estructura del Proyecto

```text
Radiografia/
├── backend/          # API RESTful, proxy de Orthanc y lógica de negocio
├── frontend/         # Aplicación React, dashboard y visor web de radiografías
└── README.md         # Documentación principal del proyecto
```

---

## 🛠️ Instalación y Configuración Local

Para ejecutar este proyecto en tu entorno local, necesitas tener instalado [Node.js](https://nodejs.org/) y seguir estos pasos:

### 1. Clonar el repositorio
```bash
git clone <url-del-repositorio>
cd Radiografia
```

### 2. Levantar el Backend
Abre una terminal y navega a la carpeta del backend:
```bash
cd backend
npm install
```
> **Nota importante:** Asegúrate de crear un archivo `.env` en la carpeta `backend` con las variables de entorno necesarias (URL de base de datos Neon, Secret JWT, y credenciales de acceso a Orthanc).

Inicia el servidor en modo desarrollo:
```bash
npm run dev
```
*El backend estará corriendo en `http://localhost:3000`*

### 3. Levantar el Frontend
Abre una **nueva terminal**, vuelve a la raíz del proyecto y navega a la carpeta del frontend:
```bash
cd frontend
npm install
npm run dev
```
*La aplicación web estará disponible en `http://localhost:5173` (o el puerto que asigne Vite)*

---

## 👥 Roles del Sistema

El sistema maneja un control de acceso basado en roles (RBAC) y un enfoque multi-tenant:

- 👑 **ADMIN**: Acceso total. Puede crear/gestionar usuarios, ver y asignar todos los estudios, y administrar el sistema.
- 👨‍⚕️ **DOCTOR**: Acceso a la visualización de los estudios que le han sido asignados y capacidad para redactar informes médicos.
- 🤒 **PATIENT (Paciente)**: Acceso restringido únicamente a su historial personal, estudios e informes médicos.

---

## 🚀 Despliegue en Producción

El proyecto está diseñado para funcionar en los siguientes entornos de producción:
- **Frontend**: Alojado en **Vercel** (`https://diagnostico-lopez.vercel.app` / `www.diagnosticolopez.com`) con integración continua (CI/CD) al hacer push a la rama `main`.
- **Backend y PACS (Orthanc)**: Alojados en un VPS Ubuntu, servidos a través de PM2 (para Node.js) y Docker (para Orthanc), con Nginx gestionando el tráfico.

---

*Desarrollado para Diagnóstico López*
