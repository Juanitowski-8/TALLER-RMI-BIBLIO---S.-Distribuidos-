# 📚 Biblioteca gRPC Service

Este proyecto implementa un **servicio remoto distribuido** para la aplicación **Biblioteca**, utilizando **gRPC en Python**.  
Permite a los usuarios:

- 📖 Solicitar el préstamo de un libro  
- 🔁 Renovar un préstamo (máximo 2 veces por libro)  
- 📦 Devolver un libro prestado  

Los clientes (Procesos Solicitantes – PS) leen las peticiones desde un menú interactivo y las envían automáticamente al servidor gRPC, que gestiona el estado de los libros con una base de datos SQLite local.

# Estructura del Proyecto
Taller-gRPC/
├── client/
│   └── app.py
├── lib/
│   ├── library_pb2.py
│   └── library_pb2_grpc.py
├── proto/
│   └── library.proto
├── server/
│   ├── app.py
│   ├── dao.py
│   └── db_init.py
└── README.md
---

## 1) Requisitos

- **Python 3.10+**
- **Librerías necesarias:**
- 
pip install grpcio protobuf

## 2) Inicializar la base de datos (solo una vez)

### En la máquina del servidor, ejecutar:

python -m server.db_init

### Salida esperada:

BD inicializada en: .../server/library.db


## Este paso crea la base de datos SQLite (library.db) y siembra los datos iniciales de los libros.

## 3) Levantar el servidor gRPC

### En la máquina del servidor, ejecutar:

python -m server.app

### Salida esperada:

Servidor gRPC en puerto 8080

El servidor escucha en 0.0.0.0:8080, aceptando conexiones desde cualquier IP dentro de la red local o VPN.
---

## 4) Probar desde el cliente

### En la máquina cliente (Windows o Linux), con Python instalado:

python -m client.app

### Menú interactivo del cliente:

1) Consulta ISBN
2) Préstamo ISBN
3) Préstamo Título
4) Devolución ISBN
0) Salir

El cliente apunta a la IP del servidor configurada en client/app.py.
--- 

Taller desarrollado para **Sistemas Distribuidos**  
Autor: Juan Esteban Camargo V 
Pontificia Universidad Javeriana – 2025  
Taller: **– Implementación gRPC Biblioteca**
