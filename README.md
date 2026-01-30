# Pruebas de funcionamiento y rendimiento

### 1. Instalación de Herramientas de Prueba
Para ejecutar las pruebas de carga, he optado por **ApacheBench**, una herramienta ligera y eficaz incluida en el paquete `apache2-utils`.

**Comando ejecutado:**
```bash
sudo apt install apache2-utils -y
```
![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasDeFuncionamientoYRendimiento/refs/heads/main/1.png)

---

### 2. Prueba de Carga Inicial (Línea Base)
He realizado una primera batería de pruebas lanzando **2000 peticiones** con un nivel de **concurrencia de 50** hacia la página principal de Tomcat.

**Resultado obtenido:**
* **Peticiones por segundo:** 1335.10 [#/sec]
* **Tiempo por petición (media):** 37.450 ms

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasDeFuncionamientoYRendimiento/refs/heads/main/2.png)
---

### 3. Optimización en server.xml
Tras analizar los resultados iniciales, he modificado el archivo `conf/server.xml` para ajustar los parámetros del conector HTTP y mejorar la gestión de hilos y conexiones concurrentes.

He añadido y modificado los siguientes atributos:
* **maxThreads="500"**: Aumenta el número máximo de hilos de ejecución.
* **minSpareThreads="50"**: Asegura un mínimo de hilos siempre activos.
* **maxConnections="10000"**: Eleva el límite de conexiones simultáneas que el servidor puede aceptar.
* **acceptCount="100"**: Define la longitud de la cola de peticiones cuando todos los hilos están ocupados.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasDeFuncionamientoYRendimiento/refs/heads/main/4.png)

---

### 4. Prueba de Carga Final y Comparativa
He repetido la prueba de carga con los mismos parámetros (2000 peticiones, 50 concurrentes) para observar el impacto de los ajustes realizados.

**Resultado tras la optimización:**
* **Peticiones por segundo:** 1127.70 [#/sec]
* **Tiempo por petición (media):** 44.338 ms

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasDeFuncionamientoYRendimiento/refs/heads/main/5.png)
