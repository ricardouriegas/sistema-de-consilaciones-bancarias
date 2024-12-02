# Documento de Casos de Uso: Sistema de Conciliaciones Bancarias

## 1. Introducción

### Propósito del documento
Este documento tiene como objetivo describir los requisitos funcionales y no funcionales del Sistema de Conciliaciones Bancarias. Su propósito principal es apoyar a los auditores en su labor, facilitando la revisión y validación de movimientos bancarios.

### Alcance del sistema
El sistema permitirá gestionar múltiples cuentas bancarias, registrar ingresos y egresos, realizar conciliaciones bancarias comparativas y generar reportes detallados para apoyar en auditorías. Está diseñado para un número ilimitado de auditores y optimiza los procesos de conciliación y análisis financiero.

---

## 2. Requisitos Funcionales
### RF1. Iniciar Sesión
- Descripción: El sistema permitirá a los usuarios autenticarse ingresando sus credenciales.
- Regla: Las credenciales ingresadas deben ser verificadas y validadas antes de otorgar acceso. En caso de credenciales incorrectas, se mostrará un mensaje de error.
### RF2. Cerrar Sesión
- Descripción: Los usuarios podrán cerrar sesión de manera segura en el sistema.
- Regla: Al cerrar sesión, se debe invalidar la sesión activa y garantizar la seguridad de los datos del usuario.
### RF3. Gestión de Usuarios
- Descripción: El sistema permitirá a los administradores agregar, modificar y eliminar usuarios.
- Regla: Solo los administradores podrán acceder a esta funcionalidad. Se deben ingresar los datos forzosos al crear o modificar un usuario:
  - Nombre completo
  - Número de folio de credencial de elector o número de INE
  - Fecha de nacimiento
  - Número de cédula profesional
  - Dirección
  - Teléfono
  - Correo electrónico
  - Sexo
- Nota: Los datos no forzosos como edad y peso son opcionales.
### RF4. Gestión de Cuentas Bancarias
- Descripción: El sistema permitirá a los administradores agregar, modificar y eliminar cuentas bancarias.
- Regla: Cada cuenta bancaria debe estar asociada a un usuario válido en el sistema.
### RF5. Gestión de Ingresos y Egresos
- Descripción: El sistema permitirá registrar, modificar y eliminar ingresos y egresos asociados a cuentas bancarias.
- Regla: Solo los administradores y auditores podrán realizar estas operaciones. Se debe validar la información antes de guardarla en la base de datos.
### RF6. Conciliación Bancaria
- Descripción: El sistema permitirá realizar la conciliación bancaria comparando ingresos y egresos internos con el estado de cuenta bancario. Adicionalmente, se comparará el saldo total con el libro contable.
- Regla: La conciliación incluirá:
  - Periodo de tiempo (fecha de inicio y término)
  - Saldo inicial del libro contable del mes anterior
  - Comparación de movimientos internos contra movimientos externos
- Nota: Los movimientos ya conciliados no podrán ser modificados.
### RF7. Generación de Reportes
- Descripción: Los auditores podrán generar reportes detallados de movimientos conciliados y pendientes.
- Regla: Los reportes estarán disponibles en formatos como PDF y Excel para facilitar su análisis y presentación.
### RF8. Consulta del Libro Contable
- Descripción: El sistema permitirá consultar el libro contable, mostrando todos los movimientos registrados y el saldo total.
- Regla: Se podrán aplicar filtros por fecha, tipo de movimiento y otros criterios para una mejor visualización.
### RF9. Seguridad de Acceso
- Descripción: El sistema implementará autenticación y autorización para controlar el acceso a las funcionalidades.
- Regla: Las contraseñas deben estar encriptadas y se utilizará un middleware para gestionar la seguridad. Solo los usuarios con permisos adecuados podrán acceder a ciertas funcionalidades.

## 3. Requisitos No Funcionales
### RNF1. Seguridad
- Descripción: El sistema debe garantizar la seguridad de la información y las comunicaciones entre el cliente y el servidor.
- Regla: Se deben implementar las siguientes medidas:
  - Uso de HTTPS para todas las comunicaciones.
  - Encriptación de contraseñas y datos sensibles.
  - Implementación de middleware de seguridad para proteger la base de datos y las aplicaciones.
### RNF2. Rendimiento
- Descripción: El sistema debe responder de manera eficiente a las acciones del usuario.
- Regla: Las operaciones más comunes deben ejecutarse en un tiempo máximo de 2 segundos para no afectar la experiencia del usuario.
### RNF3. Usabilidad
- Descripción: La interfaz de usuario debe ser intuitiva y fácil de usar, facilitando las tareas de administradores y auditores.
- Regla: Se deben seguir las buenas prácticas de diseño de interfaz y experiencia de usuario, ofreciendo ayuda en línea y mensajes claros.
### RNF4. Compatibilidad
- Descripción: El sistema debe ser compatible con los principales navegadores web y dispositivos.
- Regla: Debe funcionar correctamente en las últimas versiones de Chrome, Firefox, Edge y Safari, así como en dispositivos móviles y tablets.
### RNF5. Mantenibilidad
- Descripción: El sistema debe ser fácil de mantener y actualizar.
- Regla: El código debe estar bien documentado y estructurado siguiendo estándares de programación para facilitar futuras modificaciones.
### RNF6. Escalabilidad
- Descripción: El sistema debe poder manejar un aumento en la cantidad de usuarios y datos sin degradar su rendimiento.
- Regla: La arquitectura del sistema debe permitir la adición de recursos y la distribución de carga si es necesario.
### RNF7. Integridad y Confidencialidad de Datos
- Descripción: La información almacenada debe mantenerse íntegra y confidencial.
- Regla: Se deben implementar backups periódicos y controlar el acceso a la información según los perfiles de usuario.
### RNF8. Disponibilidad
- Descripción: El sistema debe estar disponible para los usuarios siempre que sea necesario.
- Regla: El tiempo de inactividad planificado debe ser mínimo y, preferiblemente, programado fuera de las horas laborales.


## 4. Casos de Uso
### CU1: Iniciar Sesión
- Actor: Usuario (Administrador o Auditor)
- Descripción: El usuario inicia sesión en el sistema proporcionando sus credenciales para acceder a las funcionalidades según su rol.
- Precondiciones:
  - El usuario debe estar registrado en el sistema.
  - El usuario debe tener sus credenciales (correo electrónico y contraseña) activas.
- Flujo Principal:
  1. El usuario accede a la pantalla de inicio de sesión.
  2. El usuario ingresa su correo electrónico y contraseña.
  3. El sistema valida las credenciales ingresadas.
  4. El sistema verifica el rol del usuario (Administrador o Auditor).
  5. El sistema permite el acceso y redirige al usuario al menú principal correspondiente a su rol.
- Flujos Alternativos:
  1. FA1: Credenciales Incorrectas
     - 3a. Si las credenciales son incorrectas, el sistema muestra un mensaje de error indicando que el correo electrónico o contraseña son inválidos.
     - 3b. El usuario puede intentar iniciar sesión nuevamente.
  2. FA2: Cuenta Bloqueada
     - 3a. Si el usuario excede el número máximo de intentos fallidos (3 intentos), el sistema bloquea la cuenta.
     - 3b. El sistema notifica al usuario que su cuenta ha sido bloqueada y debe contactar al administrador.
- Postcondiciones:
  - El usuario ha iniciado sesión y puede utilizar las funcionalidades según su rol.
- Reglas de Negocio:
  - Las contraseñas deben estar encriptadas en la base de datos.
  - Se permite un máximo de 3 intentos fallidos antes de bloquear la cuenta.

### CU2: Cerrar Sesión
- Actor: Usuario (Administrador o Auditor)
- Descripción: El usuario cierra su sesión actual de manera segura para finalizar su uso del sistema.
- Precondiciones:
  - El usuario debe haber iniciado sesión previamente.
- Flujo Principal:
  1. El usuario selecciona la opción de "Cerrar Sesión" en el menú.
  2. El sistema solicita confirmación para cerrar la sesión.
  3. El usuario confirma la acción.
  4. El sistema cierra la sesión y redirige al usuario a la pantalla de inicio de sesión.
- Flujos Alternativos:
  1. FA1: Cancelar Cierre de Sesión
     - 3a. El usuario cancela la confirmación.
     - 3b. El sistema mantiene la sesión activa y regresa al menú principal.
- Postcondiciones:
 - La sesión del usuario se ha terminado y se ha liberado cualquier recurso asociado.
- Reglas de Negocio:
 - El sistema debe invalidar el token de sesión al cerrar la sesión.
 - Se debe garantizar que ningún dato sensible permanezca en caché.

### CU3: Gestión de Usuarios
- Actor: Administrador
- Descripción: El administrador gestiona los usuarios del sistema, pudiendo registrar nuevos usuarios, actualizar información existente o eliminar usuarios.
- Precondiciones:
  - El administrador debe haber iniciado sesión.
- Flujo Principal:
  1. El administrador accede al módulo de gestión de usuarios.
  2. El administrador selecciona la acción a realizar:
    - **Registrar Usuario**
    - **Actualizar Usuario**
    - **Eliminar Usuario**
  3. Registrar Usuario:
    - 3a. El administrador ingresa los datos forzosos del usuario:
      - Nombre completo
      - Número de folio de credencial de elector o número de INE
      - Fecha de nacimiento
      - Número de cédula profesional
      - Dirección
      - Teléfono
      - Correo electrónico
      - Sexo
    - 3b. Opcionalmente ingresa los datos no forzosos (edad, peso).
    - 3c. El sistema valida los datos ingresados.
    - 3d. El sistema guarda el nuevo usuario en la base de datos.
    - 3e. El sistema confirma la creación del usuario.
  4. Actualizar Usuario:
    - 4a. El administrador selecciona el usuario a modificar.
    - 4b. El sistema muestra los datos actuales del usuario.
    - 4c. El administrador modifica los datos deseados.
    - 4d. El sistema valida los datos ingresados.
    - 4e. El sistema actualiza la información en la base de datos.
    - 4f. El sistema confirma la actualización.
  5. Eliminar Usuario:
    - 5a. El administrador selecciona el usuario a eliminar.
    - 5b. El sistema solicita confirmación de eliminación.
    - 5c. El administrador confirma la acción.
    - 5d. El sistema elimina al usuario de la base de datos.
    - 5e. El sistema confirma la eliminación.
- Flujos Alternativos:
  1. FA1: Datos Inválidos
     - 3c/4d. Si los datos ingresados no cumplen con las validaciones (campos obligatorios vacíos, formato incorrecto), el sistema muestra mensajes de error específicos.
     - El administrador corrige los datos y vuelve a intentarlo.
  2. FA2: Cancelación de Acción
     - En cualquier paso antes de la confirmación final, el administrador puede cancelar la acción.
     - El sistema regresa al menú de gestión de usuarios sin realizar cambios.
- Postcondiciones:
  - Los cambios en los usuarios se reflejan en el sistema.
- Reglas de Negocio:
  - Los datos forzosos deben ser proporcionados y válidos.
  - Solo los administradores pueden gestionar usuarios.
  - El número de folio de credencial de elector o INE debe ser único en el sistema.

### CU4: Gestión de Cuentas Bancarias
- Actor: Administrador
- Descripción: El administrador gestiona las cuentas bancarias, pudiendo agregar nuevas cuentas, modificar información o eliminar cuentas existentes.
- Precondiciones:
  - El administrador debe haber iniciado sesión.
- Flujo Principal:
  1. El administrador accede al módulo de gestión de cuentas bancarias.
  2. El administrador selecciona la acción a realizar:
     - Agregar Cuenta Bancaria
     - Modificar Cuenta Bancaria
     - Eliminar Cuenta Bancaria
  3. Agregar Cuenta Bancaria:
     - 3a. El administrador ingresa los datos de la cuenta:
       - Número de cuenta
       - Banco
       - Saldo inicial
       - Usuario asociado
     - 3b. El sistema valida los datos ingresados.
     - 3c. El sistema guarda la cuenta en la base de datos.
     - 3d. El sistema confirma la creación de la cuenta.
  4. Modificar Cuenta Bancaria:
     - 4a. El administrador selecciona la cuenta a modificar.
     - 4b. El sistema muestra los datos actuales de la cuenta.
     - 4c. El administrador modifica los datos deseados.
     - 4d. El sistema valida los cambios.
     - 4e. El sistema actualiza la información en la base de datos.
     - 4f. El sistema confirma la modificación.
  5. Eliminar Cuenta Bancaria:
     - 5a. El administrador selecciona la cuenta a eliminar.
     - 5b. El sistema solicita confirmación de eliminación.
     - 5c. El administrador confirma la acción.
     - 5d. El sistema elimina la cuenta de la base de datos.
     - 5e. El sistema confirma la eliminación.
- Flujos Alternativos:
  1. FA1: Datos Inválidos
     - 3b/4d. Si los datos ingresados no son válidos (por ejemplo, saldo negativo, número de cuenta duplicado), el sistema muestra mensajes de error específicos.
     - El administrador corrige los datos y vuelve a intentarlo.
  2. FA2: Cuenta Asociada a Movimientos
     - 5a. Si la cuenta tiene movimientos asociados, el sistema alerta que no puede ser eliminada.
     - 5b. El administrador debe eliminar los movimientos antes de eliminar la cuenta o cancelar la acción.
- Postcondiciones:
  - Las cuentas bancarias se actualizan en el sistema.
- Reglas de Negocio:
  - Cada cuenta bancaria debe estar asociada a un usuario válido.
  - El número de cuenta debe ser único en el sistema.
  - No se pueden eliminar cuentas con movimientos asociados sin previo manejo.

### CU5: Gestión de Ingresos y Egresos
- Actor: Administrador, Auditor
- Descripción: El usuario registra, modifica o elimina ingresos y egresos asociados a las cuentas bancarias.
- Precondiciones:
  - El usuario debe haber iniciado sesión con permisos adecuados.
- Flujo Principal:
  1. El usuario accede al módulo de gestión de ingresos y egresos.
  2. El usuario selecciona la acción a realizar:
     - Registrar Ingreso/Egreso
     - Modificar Ingreso/Egreso
     - Eliminar Ingreso/Egreso
  3. Registrar Ingreso/Egreso:
     - 3a. El usuario selecciona el tipo de movimiento (Ingreso o Egreso).
     - 3b. El usuario ingresa los datos del movimiento:
       - Fecha
       - Monto
       - Descripción
       - Cuenta bancaria asociada
     - 3c. El sistema valida los datos ingresados.
     - 3d. El sistema guarda el movimiento en la base de datos.
     - 3e. El sistema confirma el registro del movimiento.
  4. Modificar Ingreso/Egreso:
     - 4a. El usuario selecciona el movimiento a modificar.
     - 4b. El sistema muestra los datos actuales del movimiento.
     - 4c. El usuario modifica los datos deseados.
     - 4d. El sistema valida los cambios.
     - 4e. El sistema actualiza la información en la base de datos.
     - 4f. El sistema confirma la modificación.
  5. Eliminar Ingreso/Egreso:
     - 5a. El usuario selecciona el movimiento a eliminar.
     - 5b. El sistema solicita confirmación de eliminación.
     - 5c. El usuario confirma la acción.
     - 5d. El sistema elimina el movimiento de la base de datos.
     - 5e. El sistema confirma la eliminación.
- Flujos Alternativos:
  1. FA1: Datos Inválidos
     - 3c/4d. Si los datos ingresados no son válidos (por ejemplo, monto negativo, fecha inválida), el sistema muestra mensajes de error específicos.
     - El usuario corrige los datos y vuelve a intentarlo.
  2. FA2: Movimiento Conciliado
     - 4a/5a. Si el movimiento ya ha sido conciliado, el sistema no permite su modificación o eliminación.
     - 4b/5b. El sistema informa al usuario que los movimientos conciliados son inalterables.
- Postcondiciones:
  - Los movimientos se reflejan correctamente en la base de datos y en las cuentas bancarias asociadas.
- Reglas de Negocio:
  - Solo usuarios autorizados pueden gestionar ingresos y egresos.
  - Los movimientos conciliados no pueden ser modificados ni eliminados.

### CU6: Conciliación Bancaria
- Actor: Auditor
- Descripción: El auditor realiza la conciliación bancaria comparando los registros internos con los obtenidos del banco y verifica el saldo total con el libro contable.
- Precondiciones:
  - El auditor debe haber iniciado sesión.
  - Deben existir movimientos y estados de cuenta para el periodo seleccionado.
- Flujo Principal:
  1. El auditor accede al módulo de conciliación bancaria.
  2. El auditor selecciona una cuenta bancaria:
     - Clave del banco
     - Nombre del banco
     - RFC del cliente
  3. El auditor define el periodo de tiempo:
     - Fecha de inicio
     - Fecha de término
  4. El sistema obtiene el saldo inicial del libro contable del mes anterior.
  5. El sistema muestra los movimientos internos (ingresos y egresos) y los movimientos externos (estado de cuenta bancario) para el periodo seleccionado.
  6. El auditor compara los movimientos y concilia aquellos que coinciden.
  7. El auditor registra discrepancias o diferencias encontradas.
  8. El sistema actualiza el estado de los movimientos conciliados.
  9. El auditor genera un reporte detallado de la conciliación.
- Flujos Alternativos:
  1. FA1: No Hay Movimientos
     - 5a. Si no existen movimientos en el periodo seleccionado, el sistema informa al auditor que no hay movimientos para conciliar.
     - 5b. El auditor puede seleccionar otro periodo o finalizar el proceso.
  2. FA2: Diferencias en Movimientos
     - 7a. Si se detectan discrepancias significativas, el auditor puede marcar movimientos para seguimiento o investigación.
  3. FA3: Cancelación de Conciliación
     - En cualquier paso antes de finalizar, el auditor puede cancelar el proceso.
     - El sistema no guarda cambios y regresa al menú principal.
- Postcondiciones:
  - Los movimientos conciliados están actualizados en el sistema.
  - Se ha generado un reporte de conciliación.
- Reglas de Negocio:
  - Los movimientos ya conciliados no pueden ser modificados ni eliminados.
  - La conciliación debe realizarse dentro de los periodos establecidos.
  - Se debe mantener un historial de las conciliaciones realizadas.

### CU7: Generación de Reportes
- Actor: Auditor
- Descripción: El auditor genera reportes detallados de movimientos conciliados o pendientes, facilitando el análisis y presentación de información.
- Precondiciones:
  - El auditor debe haber iniciado sesión.
- Flujo Principal:
  1. El auditor accede al módulo de generación de reportes.
  2. El auditor selecciona los parámetros del reporte:
     - Tipo de reporte (Conciliados, Pendientes)
     - Cuenta bancaria
     - Periodo de fechas
     - Otros filtros (tipo de movimiento, monto)
  3. El auditor selecciona el formato de exportación (PDF, Excel).
  4. El sistema genera el reporte con la información solicitada.
  5. El sistema muestra una vista previa del reporte.
  6. El auditor descarga o imprime el reporte.
- Flujos Alternativos:
  1. FA1: No Hay Datos
     - 4a. Si no existen datos que cumplan con los parámetros seleccionados, el sistema informa al auditor.
     - 4b. El auditor puede ajustar los parámetros o cancelar el reporte.
  2. FA2: Error en Generación
     - 4a. Si ocurre un error al generar el reporte, el sistema muestra un mensaje de error y registra el incidente.
     - 4b. El auditor puede intentar nuevamente más tarde o contactar al soporte.
- Postcondiciones:
  - El auditor obtiene el reporte generado para su análisis.
- Reglas de Negocio:
  - Los reportes deben reflejar información actual y precisa.
  - Solo usuarios autorizados pueden generar reportes detallados.

### CU8: Consulta del Libro Contable
- Actor: Administrador, Auditor
- Descripción: El usuario consulta el libro contable para visualizar todos los movimientos registrados y el saldo total.
- Precondiciones:
  - El usuario debe haber iniciado sesión con permisos adecuados.
- Flujo Principal:
  1. El usuario accede al módulo de consulta del libro contable.
  2. El usuario aplica filtros opcionales:
     - Fecha (rango de fechas)
     - Tipo de movimiento (Ingreso, Egreso)
     - Cuenta bancaria
     - Monto
  3. El sistema muestra la lista de movimientos que coinciden con los filtros aplicados, ordenados cronológicamente.
  4. El usuario puede seleccionar un movimiento para ver detalles adicionales.
  5. El sistema muestra los detalles seleccionados.
- Flujos Alternativos:
  1. FA1: No Hay Movimientos
     - 3a. Si no existen movimientos que cumplan con los filtros, el sistema informa al usuario.
     - 3b. El usuario puede ajustar los filtros o consultar todo el libro contable.
- Postcondiciones:
  - El usuario ha visualizado la información del libro contable según los filtros aplicados.
- Reglas de Negocio:
  - La información debe actualizarse en tiempo real reflejando los movimientos más recientes.
  - Solo usuarios autorizados pueden acceder al libro contable.

### CU9: Seguridad de Acceso
- Actor: Administrador, Auditor
- Descripción: El sistema implementa medidas de seguridad para proteger el acceso y la información, incluyendo autenticación, autorización y encriptación de datos.
- Precondiciones:
  - N/A
- Flujo Principal:
  1. El sistema encripta las contraseñas de los usuarios al momento de registrarlas.
  2. Al iniciar sesión, el sistema compara la contraseña ingresada, tras encriptarla, con la almacenada.
  3. El sistema verifica los permisos del usuario tras una autenticación exitosa.
  4. Las comunicaciones entre el cliente y el servidor se realizan a través de conexiones seguras (HTTPS).
- Flujos Alternativos:
  1. FA1: Acceso No Autorizado
     - Si un usuario intenta acceder a una funcionalidad para la cual no tiene permisos, el sistema deniega el acceso y muestra un mensaje informativo.
  2. FA2: Sesión Expirada
     - Si la sesión del usuario expira por inactividad, el sistema cierra la sesión automáticamente y solicita al usuario que inicie sesión nuevamente.
- Postcondiciones:
  - La seguridad del sistema y de los datos de los usuarios está garantizada.
- Reglas de Negocio:
  - Se debe utilizar un middleware para gestionar la seguridad y proteger la base de datos.
  - Todas las contraseñas y datos sensibles deben estar encriptados.
  - El sistema debe cumplir con los estándares de seguridad vigentes.

---

## 5. Riesgos Identificados
### R1: Bloqueo de Cuentas
- **Descripción**: Los usuarios pueden quedarse sin acceso si se bloquean sus cuentas por intentos fallidos de inicio de sesión.
- **Mitigación**: Implementar un sistema de desbloqueo administrado por el administrador y enviar notificaciones al usuario afectado.
### R2: Pérdida de Datos
- **Descripción**: Posibilidad de pérdida de datos por fallos en el sistema o errores humanos.
- **Mitigación**: Realizar backups periódicos y contar con sistemas de recuperación de información.
### R3: Acceso No Autorizado
- **Descripción**: Riesgo de que personas no autorizadas accedan al sistema o a información confidencial.
- **Mitigación**: Implementar medidas de seguridad robustas, incluyendo autenticación de múltiples factores y monitoreo de accesos.
### R4: Errores en la Conciliación
- **Descripción**: Discrepancias no detectadas debido a errores en la conciliación.
- **Mitigación**: Validaciones adicionales y revisión manual de discrepancias significativas.

---

## 6. Aprobación del Documento

| Nombre                 | Rol                  | Firma       | Fecha       |
|------------------------|----------------------|-------------|-------------|
| Auditor Principal      | Encargado de Auditoría |             |             |
| Administrador del Sistema | Encargado del Proyecto |             |             |

---

## 7. Conclusión
Este documento define los requisitos del sistema de conciliaciones bancarias. Su implementación garantizará un buen apoyo para auditores, mejorando la precisión y eficiencia de los procesos de conciliación.

---

## 8. Anexos
- Diagramas de casos de uso.
- Prototipos de interfaz.
- Manual preliminar del usuario.
