# 🚀 Configuración de Jenkins en Docker y Despliegue con Ngrok

Este documento describe los pasos para instalar **Jenkins en Docker**, configurarlo con **GitHub** y ejecutar un **Pipeline de CI/CD**.

---

### **📌 1. Instalación de Docker**

Para ejecutar Jenkins en un contenedor Docker, primero instalamos Docker en tu codespace:

### **🔹 Verificar si Docker está instalado**
```bash
docker --version
```

🔹 Instalar Docker
```bash
sudo apt update && sudo apt install -y docker.io
```

🔹 Agregar permisos al usuario actual
```bash
sudo usermod -aG docker $USER
exec $SHELL
```
Esto permite ejecutar docker sin usar sudo.

### **📌 2. Instalación de Jenkins en Docker**
Ejecuta el siguiente comando para descargar y ejecutar Jenkins LTS en un contenedor Docker:

```bash
docker run -d --name jenkins -p 8080:8080 -p 50000:50000 \
    -v jenkins_home:/var/jenkins_home \
    jenkins/jenkins:lts
```

🔹 Obtener la contraseña inicial de Jenkins
Después de iniciar Jenkins, obtén la contraseña para configurarlo:

```bash

docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```
📌 Copia esta contraseña y pégala en la página de configuración inicial de Jenkins (se disponibiliza el el codespace)



### **📌 3. Modificar el Contenedor de Jenkins e Instalar Python**
Jenkins se ejecuta en un contenedor sin Python preinstalado. Sigue estos pasos para instalar Python y venv en el contenedor:

🔹 Listar los contenedores en ejecución
```bash
docker ps -a
```
🔹 Acceder al contenedor de Jenkins como root
```bash
docker exec -it --user root <Container ID> bash
```
🔹 Instalar Python y herramientas necesarias
```bash
apt update
apt install python3 python3-pip -y
apt install -y python3-venv
exit
```
🔹 Reiniciar el contenedor
```bash
docker restart <Container ID>
```
📌 Esto asegura que Python y venv estén disponibles en Jenkins.

### **📌 4. Instalación de Plugins Comunes**
Una vez dentro de Jenkins:

1. Accede a "Manage Jenkins" > "Manage Plugins".

2. Instala los siguientes plugins recomendados:

- Pipeline

- GitHub

- Docker Pipeline

- Multibranch Pipeline

### **📌 5. Configurar el Proyecto en Jenkins**
🔹 Copiar el Jenkinsfile en tu Repositorio

### **📌 6. Crear un Pipeline en Jenkins**
1. En Jenkins, haz clic en "New Item".

2. Ingresa un nombre para el proyecto (ej. My-Pipeline).

3. Selecciona **Multibranch Pipeline** y haz clic en OK.

4. En **Branch Sources**, haz clic en **Add Source** y elige **GitHub**.

5. Ingresa la URL de tu repositorio de GitHub.