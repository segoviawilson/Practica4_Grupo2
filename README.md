## INTEGRANTES.
| Nombre | Cargo | URL GitHub |
|---|:---:|---:|
| Daniel Alquinga | :technologist: Desarrollador | https://github.com/superdavi/Practica4_Grupo2  |
| Daniel Baldeon | :technologist: Desarrollador | https://github.com/debpdhs/Practica4_Grupo2  |
| Bryan Miño | :technologist: Desarrollador | https://github.com/bmiomi/tarea4-grupo2.git |
| Wilson Segovia | :technologist: Desarrollador | https://github.com/segoviawilson/Practica4_Grupo2.git |
| Leonardo Tuguminago | :technologist: Desarrollador | https://github.com/Tuguminago/Practica4_Grupo2.git |

# 1. Despliegue de entorno de automatización con n8n integrados con PostgreSQL en Docker Compose

El objetivo de este trabajo es desplegar una aplicacion con n8n esta esta integrada con su propia base de datos PostgreSQL, utilizando Docker Compose. Se busca aplicar  conceptos de orquestación de contenedores, persistencia de datos, separación de servicios y buenas prácticas en la gestión de entornos

# 2. Configuración e Instalación

### PASO 1: 📂 Estructura de Archivos

<img width="272" height="262" alt="image" src="https://github.com/user-attachments/assets/135d358c-39e4-4d08-b6e3-4adc96bd15a9" />

### PASO 2: Creacion de la red de docker

```bash
docker network create n8n-network
```
**Salida Esperada**

<img width="440" height="200" alt="image" src="https://github.com/user-attachments/assets/13bde87f-337b-4ea3-9b5d-e99bac57ea07" />


### PASO 3: Despliegue de contenedor de n8n

Nos ubicamos en la carpeta n8n y ejecutar el siguiente comando

```bash
docker compose -f docker-compose-n8.yml up -d
```

**Salida Esperada**

<img width="506" height="106" alt="image" src="https://github.com/user-attachments/assets/44ed4f45-9452-462c-8416-0937b9825567" />

### PASO 4: Despliege de Contenedor Postgres

Ya que nos encontramos en la carpeta n8n  es necesario ejecutar la siguiente linea de comando.

```bash
docker compose -f ../postgres/compose.postgres.yml  up -d
```

**Salida Esperada**

<img width="567" height="128" alt="image" src="https://github.com/user-attachments/assets/fda093fc-4b8b-42b3-ac2b-003cba799bb5" />

### PASO 5: Revisamos contenedores levantados

```bash
    docker ps
```

**Salida Esperada**

<img width="1379" height="100" alt="image" src="https://github.com/user-attachments/assets/3a6ae766-d570-4a3a-b15b-1372d1120fb8" />


### PASO 6: Ingreso al portar del Servidor N8N 

```bash
    http://localhost:5678/
```

**Salida Esperada**

<img width="1192" height="737" alt="image-1" src="https://github.com/user-attachments/assets/0e31d918-7da4-43ad-8f40-5f73810f2d4b" />

### PASO 8: Informacion adicional del Servidor N8N


### PASO 9: Seccion de Gestor de Base de datos en N8N


**Salida Esperada**

<img width="676" height="276" alt="image-3" src="https://github.com/user-attachments/assets/2b2b42aa-f59c-4b24-9d16-bc466b74d5d6" />

### PASO 10: Configuracion de Credenciales 

 Parametros obtenidos del archivos .env del repositorio

```bash
    Host: postgres-db
    Database: postgres
    User: n8nuser
    Password: Super_Segura123!
```
**Salida Esperada**

<img width="1372" height="733" alt="image-4" src="https://github.com/user-attachments/assets/6c3987d2-5bf6-41fe-9ccf-ea62ee83e85a" />

### PASO 11: Verificar Ingresos.
    
   Se verifica  que la conexion sea Exitosa 

**Salida Esperada**

<img width="1331" height="725" alt="image-5" src="https://github.com/user-attachments/assets/1ac4dae2-c47e-4bd6-aa27-381509841bcd" />

### PASO 12:  Verifcacion de N8N con Postgres.

   Se verifica que la conexion de la base de datos este vinculada con el contenedor N8N.

**Salida Esperada**

<img width="1600" height="318" alt="image-6" src="https://github.com/user-attachments/assets/e812f85a-b49c-490b-b8bd-e53ed013a213" />


# 3. Conclusiones y Recomendaciones

- La orquestación con Docker Compose facilita la gestión de múltiples servicios Al desplegar dos instancias de n8n con sus respectivas bases de datos PostgreSQL, se comprobó cómo Docker Compose permite definir, levantar y administrar entornos complejos de forma sencilla y estructurada. Esto reduce errores manuales y mejora la organización del proyecto.

- Separar servicios y usar volúmenes garantiza portabilidad y persistencia Al mantener cada aplicación n8n con su propia base de datos y volumen persistente, se asegura que los datos no se pierdan al reiniciar los contenedores. Además, al evitar bind mounts y usar variables en archivos .env, el proyecto se vuelve más portable y seguro.
  
- Verificar la correcta separación de servicios en el archivo docker-compose.yml, es necesario comprobar que cada instancia de n8n y su respectiva base de datos PostgreSQL estén definidas como servicios independientes, con nombres claros y sin ambigüedades. Esto refleja comprensión de la arquitectura modular y facilita el mantenimiento del entorno.

- Evaluar el uso adecuado de variables de entorno y la ausencia de credenciales en texto plano Es fundamental que todas las configuraciones sensibles (usuarios, contraseñas, puertos, etc.) estén gestionadas mediante el archivo .env., es por ello que se debe  asegurar que no se hayan expuesto datos críticos directamente en el docker-compose.yml, lo cual es una práctica insegura.
