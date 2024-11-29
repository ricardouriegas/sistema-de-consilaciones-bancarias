# Documento de Casos de Uso: Sistema de Conciliaciones Bancarias

---

## 1. Introducción

### Propósito del documento
Este documento tiene como objetivo describir los requisitos funcionales y no funcionales del Sistema de Conciliaciones Bancarias. Su propósito principal es apoyar a los auditores en su labor, facilitando la revisión y validación de movimientos bancarios.

### Alcance del sistema
El sistema permitirá gestionar múltiples cuentas bancarias, registrar ingresos y egresos, y generar reportes detallados para apoyar en auditorías. Está diseñado para un número ilimitado de auditores y optimiza los procesos de conciliación y análisis financiero.

---

## 2. Requisitos Funcionales

### RF1. Inicio de Sesión
- **Descripción:** El sistema permitirá a los usuarios iniciar sesión utilizando su correo electrónico y contraseña.
- **Regla:** Las credenciales incorrectas tres veces consecutivas bloquearán temporalmente el acceso.

### RF2. Cierre de Sesión
- **Descripción:** Los usuarios podrán cerrar sesión de forma segura para proteger su cuenta.
- **Regla:** La sesión activa se eliminará completamente del sistema.

### RF3. Gestión de Usuarios
- **Descripción:** Los administradores podrán registrar, actualizar o eliminar usuarios.
- **Regla:** No se permitirá registrar usuarios con correos duplicados.

### RF4. Gestión de Cuentas Bancarias
- **Descripción:** Los administradores podrán añadir, actualizar o eliminar cuentas bancarias.
- **Regla:** Cada número de cuenta debe ser único en el sistema.

### RF5. Registro de Movimientos
- **Descripción:** Los ingresos y egresos se registrarán manualmente o mediante integración con bancos.
- **Regla:** Los movimientos deben estar asociados a una cuenta bancaria válida.

### RF6. Conciliación Bancaria
- **Descripción:** El sistema permitirá verificar y conciliar movimientos internos contra los estados de cuenta bancarios.
- **Regla:** Los movimientos conciliados no se pueden modificar.

### RF7. Generación de Reportes
- **Descripción:** Los auditores podrán generar reportes detallados de movimientos conciliados o pendientes.
- **Regla:** Los reportes estarán disponibles en formatos como PDF o Excel.

---

## 3. Requisitos No Funcionales

### RNF1. Seguridad
- **Descripción:** Las credenciales de los usuarios estarán cifradas y se usará HTTPS.
- **Regla:** No se permitirá el acceso desde conexiones no seguras.

### RNF2. Usabilidad
- **Descripción:** El sistema tendrá una interfaz intuitiva accesible desde navegadores y dispositivos móviles.
- **Regla:** Las funciones principales no deberán requerir más de tres clics.

### RNF3. Escalabilidad
- **Descripción:** El sistema soportará hasta 10,000 usuarios simultáneamente.
- **Regla:** Mantener el rendimiento bajo alta carga.

### RNF4. Rendimiento
- **Descripción:** Las operaciones deberán responder en menos de 2 segundos.
- **Regla:** Las consultas a la base de datos estarán optimizadas.

---

## 4. Casos de Uso Principales

### CU1: Inicio de Sesión
- **Actor:** Usuario, Administrador, Auditor.
- **Descripción:** Los usuarios ingresan sus credenciales para acceder al sistema.
- **Flujo:** 
  1. Ingresar correo y contraseña.
  2. El sistema valida las credenciales.
  3. Si son correctas, asigna una sesión activa.

### CU2: Gestión de Usuarios
- **Actor:** Administrador.
- **Descripción:** El administrador gestiona usuarios registrando, actualizando o eliminando datos.
- **Flujo:** 
  1. Seleccionar acción (Registrar, Actualizar o Eliminar).
  2. Ingresar datos o seleccionar usuario existente.
  3. Confirmar la acción.

### CU3: Conciliación Bancaria
- **Actor:** Auditor.
- **Descripción:** Los auditores verifican y concilian movimientos internos contra estados bancarios.
- **Flujo:**
  1. Seleccionar cuenta bancaria.
  2. Consultar movimientos.
  3. Marcar como conciliados los movimientos correspondientes.

### CU4: Generación de Reportes
- **Actor:** Auditor.
- **Descripción:** Generar reportes sobre movimientos conciliados o pendientes.
- **Flujo:**
  1. Seleccionar parámetros del reporte (cuenta, fecha, tipo de movimiento).
  2. Generar y exportar el reporte.

---

## 5. Riesgos Identificados

### R1: Bloqueo de cuentas
- **Mitigación:** Implementar un sistema de desbloqueo administrado por el administrador.

### R2: Sobrecarga del sistema
- **Mitigación:** Utilizar servidores redundantes para balancear la carga.

### R3: Discrepancias no conciliadas
- **Mitigación:** Ofrecer herramientas para análisis manual de discrepancias.

---

## 6. Aprobación del Documento

| Nombre                 | Rol                  | Firma       | Fecha       |
|------------------------|----------------------|-------------|-------------|
| Auditor Principal      | Encargado de Auditoría |             |             |
| Administrador del Sistema | Encargado del Proyecto |             |             |

---

## 7. Conclusión
Este documento define los requisitos del sistema de conciliaciones bancarias. Su implementación garantizará un soporte efectivo para auditores, mejorando la precisión y eficiencia de los procesos de conciliación.

---

## 8. Anexos
- Diagramas de casos de uso.
- Prototipos de interfaz.
- Manual preliminar del usuario.
