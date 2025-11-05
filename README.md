📚 Biblioteca gRPC Service

Este proyecto implementa un servicio remoto para la aplicación Biblioteca utilizando gRPC en Python.
Permite a los usuarios:

Solicitar el préstamo de un libro.

Renovar un préstamo (máximo 2 veces por libro).

Devolver un libro prestado.

Los clientes (Procesos Solicitantes – PS) leen las peticiones desde un archivo .txt y las envían automáticamente al servidor gRPC, que gestiona el estado de los libros.

📝 Requisitos

Asegúrate de tener instalado:

Python 3.8+

grpcio y grpcio-tools

Para instalarlos, abre la consola de comandos y ejecuta:

pip install grpcio grpcio-tools

📂 Estructura del Proyecto
Taller_Biblioteca_gRPC/

├── CLIENTE/
│   ├── biblioteca_client.py             # Cliente gRPC
│   ├── biblioteca_pb2.py                # Generado por protoc
│   ├── biblioteca_pb2_grpc.py           # Generado por protoc
│   └── biblioteca.proto                 # Definición del servicio gRPC

├── SERVIDOR/
│   ├── biblioteca_server.py             # Servidor gRPC
│   ├── biblioteca_pb2.py                # Generado por protoc
│   ├── biblioteca_pb2_grpc.py           # Generado por protoc
│   └── biblioteca.proto                 # Definición del servicio gRPC

├── DATA/
│   ├── solicitudes_cliente1.txt         # Archivo de peticiones de usuario
│   ├── solicitudes_cliente2.txt
│   └── solicitudes_cliente3.txt

├── requirements.txt                     # Dependencias del proyecto
└── README.md                            # Documentación del sistema

🚀 Cómo Generar los Archivos de gRPC

Después de definir el archivo biblioteca.proto, genera los archivos necesarios ejecutando:

python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. biblioteca.proto


Esto creará:

biblioteca_pb2.py
biblioteca_pb2_grpc.py

🛠 Cómo Ejecutar el Proyecto
1️⃣ Iniciar el Servidor

Abre una terminal y ejecuta:

python server\biblioteca_server.py


Verás:

Servidor gRPC Biblioteca escuchando en puerto 50051...

2️⃣ Ejecutar el Cliente

En otra terminal, ejecuta:

python client\biblioteca_client.py data\solicitudes_cliente1.txt Juan


El cliente leerá las peticiones del archivo y enviará las solicitudes al servidor.

Ejemplo de salida:

[Juan] -> Libro1 prestado a Juan
[Juan] -> Libro1 renovado (1 veces)
[Juan] -> Libro1 devuelto correctamente

🤝 Prueba en Red con Dos o Más Computadoras

Si deseas probarlo en distintas máquinas:

Obtén la IP del servidor con ipconfig (Windows) o ifconfig (Linux/macOS).

Modifica en el cliente la línea de conexión:

channel = grpc.insecure_channel("192.168.X.X:50051")  # Reemplaza con la IP real


Ejecuta el servidor en una máquina y los clientes en otras.
