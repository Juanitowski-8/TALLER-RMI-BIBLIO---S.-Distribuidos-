# 📚 Biblioteca gRPC Service

Este proyecto implementa un **servicio remoto para la aplicación Biblioteca** utilizando **gRPC en Python**.  
Permite a los usuarios:

- Solicitar el préstamo de un libro.  
- Renovar un préstamo (máximo 2 veces por libro).  
- Devolver un libro prestado.  

Los clientes (Procesos Solicitantes – PS) leen las peticiones desde un archivo `.txt` y las envían automáticamente al servidor gRPC, que gestiona el estado de los libros.

## 📝 Requisitos

Asegúrate de tener instalado:

- **Python 3.8+**
- **grpcio** y **grpcio-tools**

Para instalarlos, abre la consola de comandos y ejecuta:

pip install grpcio grpcio-tools

---

### 🧩 **3️⃣ Estructura del Proyecto**

## 📂 Estructura del Proyecto

Taller_Biblioteca_gRPC/

├── CLIENTE/
│ ├── biblioteca_client.py # Cliente gRPC
│ ├── biblioteca_pb2.py # Generado por protoc
│ ├── biblioteca_pb2_grpc.py # Generado por protoc
│ └── biblioteca.proto # Definición del servicio gRPC

├── SERVIDOR/
│ ├── biblioteca_server.py # Servidor gRPC
│ ├── biblioteca_pb2.py # Generado por protoc
│ ├── biblioteca_pb2_grpc.py # Generado por protoc
│ └── biblioteca.proto # Definición del servicio gRPC

├── DATA/
│ ├── solicitudes_cliente1.txt # Archivo de peticiones de usuario
│ ├── solicitudes_cliente2.txt
│ └── solicitudes_cliente3.txt

├── requirements.txt # Dependencias del proyecto
└── README.md # Documentación del sistema
## 🚀 Cómo Generar los Archivos de gRPC

Después de definir el archivo `biblioteca.proto`, genera los archivos necesarios ejecutando:
python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. biblioteca.proto

Esto creará:
biblioteca_pb2.py
biblioteca_pb2_grpc.py

---

### 🧩 **5️⃣ Ejecución del Proyecto**
## 🛠️ Cómo Ejecutar el Proyecto

### 🖥️ Iniciar el Servidor

Abre una terminal y ejecuta:
python server\biblioteca_server.py

Verás el mensaje:

Servidor gRPC Biblioteca escuchando en puerto 50051...

### 💻 Ejecutar el Cliente

En otra terminal, ejecuta:

python client\biblioteca_client.py data\solicitudes_cliente1.txt Juan

El cliente leerá las peticiones del archivo y enviará las solicitudes al servidor.

## 📄 Ejemplo de archivo solicitudes_cliente1.txt:
SOLICITAR Libro1
RENOVAR Libro1
RENOVAR Libro1
DEVOLVER Libro1
SOLICITAR Libro2

## 🧾 Ejemplo de salida:
[Juan] -> Libro1 prestado a Juan

[Juan] -> Libro1 renovado (1 veces)

[Juan] -> Libro1 devuelto correctamente

---

### 🧩 **6️⃣ Pruebas en Red**
## 🌐 Prueba en Red con Dos o Más Computadoras

Si deseas probarlo en distintas máquinas:

1. Obtén la IP del servidor con `ipconfig` (Windows) o `ifconfig` (Linux/macOS).  
2. Modifica en el cliente la línea de conexión:
   channel = grpc.insecure_channel("192.168.X.X:50051")  # Reemplaza con la IP real

---

### 🧩 **7️⃣ Detalles Técnicos**
## 🧠 Detalles Técnicos

- Tres métodos RPC: `SolicitarLibro`, `RenovarLibro`, `DevolverLibro`.  
- Control de préstamos concurrentes.  
- Renovaciones limitadas a dos por libro.  
- Comunicación local (`localhost:50051`) por defecto, adaptable a IP externas.  
- Compatible con **Python 3.10+**.


---

Proyecto desarrollado para el curso **Sistemas Distribuidos**  
Autores: Juan Esteban Camargo V y Diego Andres Martinez  
Pontificia Universidad Javeriana – 2025  
Versión: **1.0 – Implementación gRPC Biblioteca**
