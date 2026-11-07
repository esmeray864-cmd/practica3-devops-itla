# Práctica 3: Configuración Básica de Pipeline CI/CD

**Instituto Tecnológico de las Américas (ITLA)**  
**Asignatura:** DevOps  
**Proyecto:** Aplicación de gestión de tareas con Node.js, Express y GitHub Actions.

## 1. Descripción del proyecto

Este proyecto consiste en implementar un pipeline de Integración Continua y Despliegue Continuo (CI/CD) utilizando GitHub Actions para automatizar la revisión, ejecución de pruebas, construcción y publicación de una aplicación web.

Se utilizó la plantilla oficial proporcionada para la Práctica 3, agregando nuevas funcionalidades y pruebas automatizadas.

## 2. Tecnologías utilizadas

- Node.js 26.13.0.
- npm 11.20.0.
- JavaScript.
- Express.
- Jest y Supertest.
- Git y GitHub.
- GitHub Actions.
- Docker.
- GitHub Pages.

## 3. Estructura del proyecto

```text
plantilla-devops-itla/
│
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── public/
│   └── index.html
│
├── src/
│   ├── app.js
│   └── server.js
│
├── tests/
│   └── app.test.js
│
├── Dockerfile
├── package.json
├── package-lock.json
└── README.md
```

## 4. Funcionalidad implementada

Se agregó la funcionalidad para eliminar tareas mediante el método HTTP DELETE.

**Endpoint:**

`DELETE /api/tareas/:id`

La funcionalidad permite:

- Buscar una tarea por su identificador.
- Eliminar la tarea cuando existe.
- Devolver un código HTTP 404 cuando no se encuentra.
- Mostrar un mensaje de confirmación cuando la eliminación es exitosa.

## 5. Pruebas automatizadas

Se utilizaron Jest y Supertest para comprobar el funcionamiento de la aplicación.

Se agregaron dos pruebas nuevas:

1. Verificar que una tarea existente pueda eliminarse correctamente.
2. Verificar que intentar eliminar una tarea inexistente devuelva un error 404.

**Resultados obtenidos:**

- Total de pruebas: 8.
- Pruebas aprobadas: 8.
- Pruebas fallidas: 0.

### Cobertura de código

| Indicador | Resultado |
|---|---:|
| Statements | 95.55% |
| Branches | 85.71% |
| Functions | 100% |
| Lines | 100% |

## 6. Configuración del pipeline CI/CD

El pipeline se encuentra configurado en:

`.github/workflows/ci.yml`

Se ejecuta automáticamente cuando se realiza un push a la rama `main` o un pull request dirigido a dicha rama.

### Etapas del pipeline

**Etapa 1. Checkout**

Descarga el código fuente del repositorio utilizando GitHub Actions.

**Etapa 2. Configuración de Node.js**

Prepara el entorno de ejecución utilizando Node.js 20.

**Etapa 3. Instalación de dependencias**

Ejecuta `npm install` para instalar los paquetes necesarios.

**Etapa 4. Revisión estática**

Ejecuta `npm run lint` para comprobar la sintaxis de los archivos JavaScript.

**Etapa 5. Pruebas automatizadas**

Ejecuta `npm test` para realizar las pruebas unitarias y de integración con Jest, incluyendo el reporte de cobertura.

**Etapa 6. Construcción de Docker**

Construye una imagen Docker de la aplicación para verificar que pueda empaquetarse correctamente.

**Etapa 7. Despliegue a GitHub Pages**

Cuando el pipeline termina correctamente en un push a `main`, publica automáticamente el contenido de la carpeta `public`.

El despliegue depende de que el trabajo de construcción y pruebas haya finalizado exitosamente.

## 7. Configuración de GitHub Pages

Se habilitó GitHub Pages desde:

Settings → Pages → Build and deployment → Source → GitHub Actions.

La aplicación se encuentra publicada en:

https://esmeray864-cmd.github.io/practica3-devops-itla/

## 8. Demostración del pipeline

Para comprobar el funcionamiento del pipeline se realizaron tres ejecuciones:

| Ejecución | Descripción | Resultado |
|---|---|---|
| #1 | Primera versión del proyecto | SUCCESS |
| #2 | Prueba fallida intencionalmente | FAILURE |
| #3 | Corrección de la prueba | SUCCESS |

### Prueba de fallo

Se introdujo intencionalmente una prueba incorrecta:

```javascript
expect(1).toBe(2);
```

Al subir los cambios al repositorio, GitHub Actions detectó el error y el trabajo de construcción y pruebas falló.

El despliegue no se ejecutó debido a que depende de la aprobación del trabajo anterior.

### Corrección

Se eliminó la prueba incorrecta y se ejecutaron nuevamente las ocho pruebas automatizadas.

Todas las pruebas pasaron y el pipeline volvió a ejecutarse correctamente, incluyendo el despliegue a GitHub Pages.

Esto demuestra que la automatización identifica errores y evita publicar cambios que no superan las validaciones.

## 9. Instrucciones para instalar y ejecutar el proyecto

### Requisitos

- Node.js 20 o superior.
- Git.
- Visual Studio Code u otro editor de código.

### Instalación

Clonar el repositorio:

```bash
git clone https://github.com/esmeray864-cmd/practica3-devops-itla.git
```

Entrar en la carpeta:

```bash
cd practica3-devops-itla
```

Instalar dependencias:

```bash
npm install
```

Ejecutar pruebas:

```bash
npm test
```

Ejecutar revisión estática:

```bash
npm run lint
```

Iniciar la aplicación:

```bash
npm start
```

La aplicación estará disponible localmente en:

`http://localhost:3000`

### Construcción con Docker

```bash
docker build -t tareas-devops .
```

Ejecutar el contenedor:

```bash
docker run -p 3000:3000 tareas-devops
```

## 10. Guía de contribución

Para contribuir al proyecto:

1. Clonar el repositorio.
2. Crear una rama para los cambios.
3. Implementar las modificaciones.
4. Agregar o actualizar las pruebas.
5. Ejecutar `npm test`.
6. Ejecutar `npm run lint`.
7. Realizar un commit.
8. Subir los cambios y crear un pull request.

Los cambios deben superar las validaciones automatizadas antes de integrarse a la rama principal.

## 11. Conclusiones

La práctica permitió implementar un pipeline CI/CD básico utilizando GitHub Actions.

Se logró automatizar la revisión estática, las pruebas, la construcción de una imagen Docker y el despliegue de una aplicación web mediante GitHub Pages.

También se implementó una nueva funcionalidad para eliminar tareas y se agregaron pruebas automatizadas para validar su funcionamiento.

Finalmente, se comprobó la capacidad del pipeline para detectar errores y recuperarse después de su corrección.

El proyecto demuestra la importancia de la automatización en los procesos de desarrollo de software y la integración continua.

---

**Repositorio GitHub:**  
https://github.com/esmeray864-cmd/practica3-devops-itla

**Aplicación publicada:**  
https://esmeray864-cmd.github.io/practica3-devops-itla/