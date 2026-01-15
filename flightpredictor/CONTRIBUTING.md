# 🟩 FLUJO DE TRABAJO OFICIAL DEL EQUIPO BACKEND

## 🌱 Ramas principales
* **main** → código estable, probado, listo para producción
* **develop** → integración continua del equipo, pruebas internas, perfil develop

> **Nota:** Nadie trabaja directamente sobre `main`. Toda nueva funcionalidad nace desde `develop`.

---

## 🟦 1. Creación de ramas por desarrollador
Cada desarrollador crea su rama a partir de `develop`, nunca desde `main`.

**Flujo recomendado:**
```bash
git checkout dev
git pull origin dev
git checkout -b dev-nombre-tarea
```

**Ejemplos:**
* `dev-api-endpoints`
* `dev-service-prediction`
* `dev-repository-cache`
* `dev-config-resilience4j`
* `dev-infra-docker`
* `dev-tests-service`

Esto evita colisiones y hace que cada PR sea fácil de revisar.

---

## 🟧 2. Áreas de trabajo por desarrollador (según tu distribución real)

### ✔ Desarrollador 1 — API / Controller (Guillermo)
Trabaja en:
* `controller/`
* `dto/`

### ✔ Desarrollador 2 — Servicios / Lógica (Raul)
Trabaja en:
* `service/`
* `util/`
* `resources/python/`
* `resources/model/`

### ✔ Desarrollador 3 — Persistencia / BD (Oscar)
Trabaja en:
* `entity/`
* `repository/`
* `resources/application-*.yml`

### ✔ Desarrollador 4 — Configuración / Resiliencia (mario)
Trabaja en:
* `config/`
* `resources/application-*.yml`

### ✔ Desarrollador 5 — Infraestructura (faner)
Trabaja en:
* `Dockerfile`
* `docker-compose.yml`
* `k8s/`
* `.github/workflows/`
* `skaffold.yaml`

### ✔ Desarrollador 6 — QA / Testing
Trabaja en:
* `test/`

---

## 🟪 3. Flujo de trabajo diario

### 🔹 Paso 1 — Actualizar local
Cada desarrollador comienza su día con:
```bash
git checkout dev
git pull origin dev
```

### 🔹 Paso 2 — Crear su rama de trabajo
```bash
git checkout -b dev-nombre-tarea
```

### 🔹 Paso 3 — Desarrollar SOLO en su área asignada
Esto evita conflictos innecesarios.

### 🔹 Paso 4 — Commits pequeños y descriptivos
Formato recomendado:
* `feat(controller): agrega endpoint de predicción`
* `fix(service): corrige cálculo de fallback`
* `refactor(repository): optimiza consulta de cache`

### 🔹 Paso 5 — Hacer push de su rama
```bash
git push origin dev-nombre-tarea
```

### 🔹 Paso 6 — Crear Pull Request → hacia develop
**Reglas del PR:**
* Debe compilar
* Debe pasar tests
* Debe respetar estructura de carpetas
* No debe modificar áreas de otros desarrolladores
* Debe tener descripción clara

### 🔹 Paso 7 — Revisión por pares
Cada PR debe ser revisado por al menos 1 compañero.

---

## 🟥 4. Integración a develop
Cuando el PR es aprobado:
1. Se hace merge a `develop`
2. Se ejecutan pruebas integradas
3. Se valida que no rompa el perfil develop

> `develop` siempre debe estar estable, aunque no listo para producción.

---

## 🟩 5. Preparación para producción
Cuando se decide liberar una versión:
1. QA valida `develop`
2. Infraestructura genera build Docker
3. Se crea un PR desde `develop` → `main`
4. Se etiqueta la versión: `v1.0.0`
5. Se despliega a producción (Docker/K8s)

---

## 🟦 6. Reglas de oro para evitar conflictos
* ✔ Nadie trabaja directamente en `main`
* ✔ Nadie toca carpetas que no le corresponden
* ✔ Cada cambio va en su propia rama
* ✔ PRs pequeños y frecuentes
* ✔ Revisiones obligatorias
* ✔ `develop` siempre debe compilar
* ✔ `main` siempre debe ser estable
