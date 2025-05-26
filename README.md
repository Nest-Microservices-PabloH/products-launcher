# Microservicios - Products Launcher

## 🚀 Desarrollo

### Requisitos Previos
1. Clonar el repositorio
2. Crear un archivo `.env` basado en el `.env.template`
3. Ejecutar el comando para reconstruir los sub-módulos:
   ```bash
   git submodule update --init --recursive
   ```
4. Iniciar los servicios con Docker:
   ```bash
   docker compose up --build --watch
   ```

## 📦 Gestión de Git Submodules

### Creación de Submodules
1. Crear un nuevo repositorio en GitHub
2. Clonar el repositorio en la máquina local
3. Añadir el submodule:
   ```bash
   git submodule add <repository_url> <directory_name>
   ```
   > Nota: `directory_name` debe ser una carpeta que no exista en el proyecto

4. Confirmar los cambios:
   ```bash
   git add .
   git commit -m "Add submodule"
   git push
   ```

### Comandos Útiles
- Inicializar y actualizar sub-módulos (para nuevos clones):
  ```bash
  git submodule update --init --recursive
  ```
- Actualizar referencias de sub-módulos:
  ```bash
  git submodule update --remote
  ```

## ⚠️ Importante
Al trabajar con sub-módulos, seguir este orden:
1. **Primero**: Actualizar y hacer push en el sub-módulo
2. **Después**: Actualizar y hacer push en el repositorio principal

> ⚠️ Si se hace en orden inverso, se perderán las referencias de los sub-módulos y habrá que resolver conflictos.

## 🚀 Producción

### Requisitos Previos
1. Clonar el repositorio
2. Crear un archivo `.env` basado en el `.env.template`
3. Ejecutar el comando para reconstruir los sub-módulos:
   ```bash
   git submodule update --init --recursive
   ```

### Despliegue
1. Construir las imágenes de producción:
   ```bash
   docker compose -f docker-compose.prod.yml build
   ```

2. Iniciar los servicios en modo producción:
   ```bash
   docker compose -f docker-compose.prod.yml up -d
   ```

> ⚠️ Asegúrate de que todas las variables de entorno necesarias estén configuradas correctamente en el archivo `.env` antes de desplegar en producción.