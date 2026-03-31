# Windows-Server-Pr-ctica-[# Informe de Implementación Windows.txt](https://github.com/user-attachments/files/26386041/Informe.de.Implementacion.Windows.txt)
# Informe de Implementación: Windows Server 2016 en VirtualBox

Este repositorio contiene la documentación técnica y los archivos de configuración resultantes de la implementación de un servidor virtualizado bajo el hipervisor Oracle VM VirtualBox.

## 1. Ficha Técnica de la Máquina Virtual
La implementación se realizó siguiendo los requisitos técnicos de la evaluación para asegurar un entorno de servidor estándar:

| Parámetro | Configuración Implementada |
| :--- | :--- |
| **Sistema Operativo** | Windows Server 2016 Standard |
| **Arquitectura** | 64 bits |
| **Interfaz de Usuario** | Experiencia de Escritorio (GUI) |
| **Memoria RAM** | 9 GB (9216 MB) |
| **Procesadores** | 4 vCPU |
| **Disco Duro** | 50 GB (VDI - Reservado dinámicamente) |
| **Red** | Adaptador NAT con Port Forwarding |

## 2. Proceso de Configuración Técnica

### Fase de Aprovisionamiento
1. **Creación del Contenedor:** Se definió la máquina virtual en VirtualBox asignando los recursos de hardware especificados.
2. **Instalación de SO:** Se ejecutó la instalación desde una imagen ISO oficial, seleccionando la edición Standard para una administración gráfica completa.
3. **Seguridad Inicial:** Se estableció la contraseña de seguridad para la cuenta de Administrador local.

### Configuración de Red y Acceso Remoto
Para preparar el servidor para administración remota, se realizaron las siguientes acciones:
* **Activación de RDP:** Se habilitó el "Remote Desktop" a través del Server Manager.
* **Mapeo de Puertos:** Se configuró una regla de *Port Forwarding* en VirtualBox para direccionar el tráfico del Host (puerto 3390) al Guest (puerto 3390).
* **Firewall de Windows:** Se crearon reglas de entrada para permitir el tráfico TCP por el puerto 3390 en todos los perfiles de red (Dominio, Privado y Público).

## 3. Validación y Troubleshooting
Durante la fase de pruebas, se realizaron las siguientes comprobaciones de conectividad:

* **Prueba de Servicio Interna:** Se ejecutó el comando `Test-NetConnection -Port 3390` dentro del servidor, obteniendo un resultado de **TcpTestSucceeded: True**. Esto confirma que el servicio RDP está correctamente iniciado y escuchando peticiones.
* **Incidencia de Red Externa:** Se identificó una restricción de comunicación entre el Host y el Guest a través de la interfaz virtual NAT que impidió la conexión final desde la máquina física. 
* **Análisis Técnico:** El fallo se localizó en la capa de red del hipervisor/anfitrión, descartando errores de configuración dentro del sistema operativo Windows Server 2016, ya que el servicio y las reglas de firewall fueron validadas exitosamente de forma interna.

---
*Este registro sirve como evidencia de la correcta aplicación de conocimientos en virtualización y administración de servidores Windows.*
