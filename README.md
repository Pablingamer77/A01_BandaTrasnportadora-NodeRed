# A01 - Banda transportadora inteligente con Node-RED

Proyecto académico que simula una banda transportadora industrial con Node-RED, variables de proceso, detección de alarmas, mensajería MQTT y dashboard web.

Proyecto hecho en NodeRed
## Flujos que contiene

1. **A01 - Motor Físico y MQTT**: inicializa el estado global y ejecuta ecuaciones JSONata cada segundo. Publica telemetría, estado y alarmas por MQTT; recibe comandos MQTT y confirma con ACK.
2. **A01 - Dashboard Web**: página HTML inicial a través de HTTP GET `/control-a01`. Esta versión utiliza valores de visualización local, por lo que se incluye como antecedente; su función de enviar comandos apunta a `/api/command`, ruta no incluida en los flujos exportados.
3. **A01 V2 - Dashboard FUNCIONAL**: interfaz HTML/JS que lee valores del motor simulado desde el contexto global de Node-RED. Expone GET `/a01-v2`, POST `/a01-v2/comando` y GET `/a01-v2/estado`.

## Importación

1. Instalar y abrir **Node-RED**.
2. En el menú (☰) elegir **Importar** y cargar `flujos/A01_proyecto_completo.json`.
3. Importar los flujos en un entorno vacío para evitar nombres de rutas HTTP duplicadas.
4. Pulsar **Implementar** (*Deploy*).
5. Abrir `http://localhost:1880/a01-v2` en el navegador para la versión funcional.

## Configuración relevante

- El motor utiliza el **contexto global** de Node-RED para compartir variables con el dashboard V2.
- El broker del primer flujo es **localhost:1883**. Para que los nodos MQTT conecten, se necesita un broker MQTT local activo (por ejemplo, Mosquitto) o adaptar el broker a uno disponible.
- Para guardar el CSV, revisar el nodo **Guardar Historial CSV**: su ruta original `C:\MisProyectos\A01_ArchivoPersistencia` puede requerir un cambio en otro equipo y no tiene extensión `.csv`.
- Los flujos están exportados sin credenciales. No subir contraseñas, tokens ni archivos `.env` reales al repositorio.
- La visualización de gráficos del dashboard utiliza Chart.js servido por CDN y por ello requiere conexión a internet.

## Demostración

1. Abrir `http://localhost:1880/a01-v2`.
2. Arrancar la banda y cambiar su velocidad.
3. Simular atasco, desatascar y arrancar de nuevo.
4. Activar falla de sensor y repararla.
5. Mostrar Vista de Ingeniería con corriente, temperatura, indicadores y las últimas 20 lecturas.
6. Mostrar los flujos, nodos principales y publicación de telemetría y alarmas.

## Control de versiones

Se usó Git para registrar cambios en los archivos del proyecto y GitHub para alojar el repositorio remoto. `git push` publica commits locales y `git pull` descarga e integra cambios del repositorio remoto.

## Capturas

Las imágenes de la carpeta `capturas/` muestran la organización de los tres flujos en el editor.
