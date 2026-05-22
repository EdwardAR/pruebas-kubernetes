# Manifiestos YAML de Kubernetes (guía básica)

Este repositorio contiene ejemplos prácticos para aprender conceptos base de Kubernetes usando `kubectl apply -f <archivo>.yaml`.

## ¿Qué hace cada archivo?

- **`mipod.yaml`**  
  Crea un **Pod** con Nginx y monta un volumen `hostPath`.  
  Útil para entender estructura mínima de un Pod, puertos y montaje de volúmenes.

- **`mydeployment.yaml`**  
  Crea un **Deployment** de Nginx con probes (`liveness` y `readiness`) y límites/requests de recursos.  
  Útil para aprender despliegues declarativos, salud de contenedores y gestión de recursos.

- **`service.yaml`**  
  Crea un **Service** tipo `LoadBalancer` para exponer la app.  
  Útil para entender networking básico y cómo acceder a pods mediante un servicio estable.

- **`hpa.yaml`**  
  Crea un **HorizontalPodAutoscaler** para escalar el Deployment `mideployment` según CPU.  
  Útil para practicar autoescalado automático.

- **`miconfig.yaml`**  
  Crea un **ConfigMap** con variables de configuración.  
  Útil para separar configuración de la imagen del contenedor.

- **`misecret2.yaml`**  
  Crea un **Secret** tipo `Opaque` con datos codificados en base64.  
  Útil para gestionar credenciales o datos sensibles.

- **`pod-cm.yaml`**  
  Crea un Pod que consume valores del ConfigMap `miconfig` como variables de entorno.  
  Útil para ver cómo inyectar configuración en runtime.

- **`pod-secret.yaml`**  
  Crea un Pod que consume valores del Secret `misecret2` como variables de entorno.  
  Útil para practicar uso de secretos en aplicaciones.

## Flujo recomendado para practicar

1. Crear recursos:
   ```bash
   kubectl apply -f miconfig.yaml
   kubectl apply -f misecret2.yaml
   kubectl apply -f mydeployment.yaml
   kubectl apply -f service.yaml
   kubectl apply -f hpa.yaml
   kubectl apply -f pod-cm.yaml
   kubectl apply -f pod-secret.yaml
   ```
2. Revisar estado:
   ```bash
   kubectl get pods,deploy,svc,hpa,configmap,secret
   ```
3. Ver detalles:
   ```bash
   kubectl describe deployment mideployment
   kubectl describe hpa bear
   ```
4. Limpiar recursos:
   ```bash
   kubectl delete -f .
   ```

> Nota: `hostPath` en `mipod.yaml` se usa para laboratorio local; en producción se recomienda usar volúmenes administrados (PV/PVC).
