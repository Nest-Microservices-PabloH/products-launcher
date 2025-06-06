# 🚀 Comandos de Kubernetes y Helm

## 📦 Helm

| Comando | Descripción |
|---------|-------------|
| `helm create <nombre>` | Crear nueva configuración |
| `helm install <nombre> .` | Aplicar configuración inicial |
| `helm upgrade <nombre> .` | Aplicar actualizaciones |

## 🛠️ Kubernetes

### 📋 Comandos Básicos

| Comando | Descripción |
|---------|-------------|
| `kubectl get <pods \| deployments \| services>` | Listar recursos |
| `kubectl describe pods` | Ver detalles de todos los pods |
| `kubectl describe pod <nombre>` | Ver detalles de un pod específico |
| `kubectl delete pod <nombre>` | Eliminar un pod |
| `kubectl logs <nombre>` | Ver logs de un pod |

### 🏗️ Crear Recursos

#### Deployment
```bash
kubectl create deployment <nombre> --image=<registro/url/imagen> --dry-run=client -o yaml > deployment.yml
```

#### Service
```bash
# Para acceso interno al cluster
kubectl create service clusterip <nombre> --tcp=<8888> --dry-run=client -o yaml > service.yml 

# Para acceso externo al cluster
kubectl create service nodeport <nombre> --tcp=<3000> --dry-run=client -o yaml > service.yml
```

## 🔐 Secrets

### Crear Secrets
```bash
# Un solo secreto
kubectl create secret generic <nombre> --from-literal=key=value

# Múltiples secretos
kubectl create secret generic secret1 --from-literal=key1=value1 --from-literal=key2=value2
```

### Gestionar Secrets
| Comando | Descripción |
|---------|-------------|
| `kubectl get secrets` | Listar todos los secrets |
| `kubectl get secrets <nombre> -o yaml` | Ver contenido de un secret |

### 📝 Editar un Secret

1. Abrir editor: `kubectl edit secret <nombre>`
2. Cambiar valor (usar [conversor base64 online](https://www.rapidtables.com/web/tools/base64-decode.html))
3. Presionar **i** para insertar
4. Agregar valor a decodificar en nueva línea
5. Presionar **esc** y luego `:. ! base64 -D` para decodificar
6. Presionar **i** para editar valor
7. Presionar **esc** y luego `:. ! base64` para codificar
8. Presionar **i** para ajustar posición
9. Presionar **esc** y luego **:wq** para guardar

## ☁️ Configuración con Google Cloud

### 1. Crear Secret para GCR
```bash
kubectl create secret docker-registry gcr-json-key \
  --docker-server=SERVIDOR-DE-GOOGLE-docker.pkg.dev \
  --docker-username=_json_key \
  --docker-password="$(cat 'PATH/DE/Tienda Microservices IAM.json')" \
  --docker-email=TU_CORREO@gmail.com
```

### 2. Configurar Service Account
```bash
kubectl patch serviceaccounts default -p '{ "imagePullSecrets": [{ "name":"gcr-json-key" }] }'
```

## 📤 Exportar y Aplicar Configuraciones

### Exportar
```bash
kubectl get secret <nombre> -o yaml > <nombre>.yml
```

### Aplicar
```bash
kubectl create -f <nombre>.yml
```

