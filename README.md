# 🐾 Peluquería Canina — Sistema de Gestión

Aplicación de escritorio desarrollada en **Java (Swing)** para la gestión integral de una peluquería canina. Permite registrar, consultar, editar y eliminar mascotas junto con los datos de sus dueños, con persistencia en base de datos **MySQL** mediante **JPA (EclipseLink)**.

---

## 📋 Tabla de Contenidos

- [Características](#-características)
- [Arquitectura](#-arquitectura)
- [Tecnologías](#-tecnologías)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación y Configuración](#-instalación-y-configuración)
- [Uso](#-uso)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Modelo de Datos](#-modelo-de-datos)
- [Autor](#-autor)

---

## ✨ Características

- **Alta de mascotas**: Registro completo con nombre, raza, color, alergias, atención especial y observaciones.
- **Datos del dueño**: Cada mascota se vincula a su dueño con nombre y número de celular.
- **Visualización en tabla**: Listado general de todas las mascotas registradas con los datos más relevantes.
- **Edición de registros**: Modificación de cualquier dato de la mascota o su dueño.
- **Eliminación de registros**: Baja de mascotas del sistema.
- **Interfaz gráfica intuitiva**: Ventanas diseñadas con Java Swing para una experiencia de usuario sencilla.

---

## 🏗 Arquitectura

El proyecto sigue una **arquitectura en 3 capas**, separando responsabilidades:

```
┌─────────────────────────────────────────────┐
│           Capa de Presentación (igu)        │
│  Principal · CargaDatos · VerDatos · Editar │
├─────────────────────────────────────────────┤
│          Capa de Lógica de Negocio          │
│            ControladoraLogica               │
├─────────────────────────────────────────────┤
│           Capa de Persistencia              │
│  ControladoraPersistencia · JPA Controllers │
├─────────────────────────────────────────────┤
│              Base de Datos                  │
│          MySQL (peluqueria_canina)          │
└─────────────────────────────────────────────┘
```

| Capa | Paquete | Responsabilidad |
|------|---------|-----------------|
| **Presentación** | `com.mycompany.peluqueriacanina.igu` | Formularios Swing (interfaces de usuario) |
| **Lógica** | `com.mycompany.peluqueriacanina.logica` | Reglas de negocio, entidades JPA y coordinación |
| **Persistencia** | `com.mycompany.peluqueriacanina.persistencia` | Acceso a datos mediante JPA/EclipseLink |

---

## 🛠 Tecnologías

| Tecnología | Versión | Uso |
|------------|---------|-----|
| **Java** | 17 | Lenguaje principal |
| **Java Swing** | — | Interfaz gráfica de usuario |
| **Maven** | — | Gestión de dependencias y build |
| **JPA (EclipseLink)** | 2.7.10 | ORM / Persistencia |
| **MySQL** | 8.0+ | Base de datos relacional |
| **MySQL Connector/J** | 8.0.30 | Driver JDBC |
| **NetBeans IDE** | — | Entorno de desarrollo |

---

## 📌 Requisitos Previos

Antes de ejecutar el proyecto, asegurate de tener instalado:

- [JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html) o superior
- [Apache Maven](https://maven.apache.org/download.cgi)
- [MySQL Server 8.0+](https://dev.mysql.com/downloads/mysql/)
- [NetBeans IDE](https://netbeans.apache.org/) (recomendado) u otro IDE compatible con Maven

---

## 🚀 Instalación y Configuración

### 1. Clonar el repositorio

```bash
git clone https://github.com/ezebarcop/PeluqueriaCanina.git
cd PeluqueriaCanina
```

### 2. Crear la base de datos

Abrí tu cliente MySQL y ejecutá:

```sql
CREATE DATABASE peluqueria_canina;
```

> **Nota:** Las tablas se crean automáticamente gracias a la configuración de JPA (`schema-generation.database.action = create`).

### 3. Configurar la conexión a la base de datos

Editá el archivo `src/main/resources/META-INF/persistence.xml` con tus credenciales:

```xml
<property name="javax.persistence.jdbc.url"
          value="jdbc:mysql://localhost:3306/peluqueria_canina?serverTimezone=UTC"/>
<property name="javax.persistence.jdbc.user" value="root"/>
<property name="javax.persistence.jdbc.password" value="tu_contraseña"/>
```

### 4. Compilar y ejecutar

```bash
# Compilar
mvn clean install

# Ejecutar
mvn exec:java -Dexec.mainClass="com.mycompany.peluqueriacanina.PeluqueriaCanina"
```

O simplemente abrí el proyecto en **NetBeans** y presioná ▶️ **Run**.

---

## 💡 Uso

### Pantalla Principal
Desde la ventana principal podés acceder a:
- **Cargar Datos** → Registrar una nueva mascota con su dueño.
- **Ver Datos** → Consultar, editar o eliminar mascotas existentes.

### Flujo de trabajo típico

1. **Registrar** una mascota completando el formulario con todos sus datos y los de su dueño.
2. **Consultar** el listado general en la tabla de mascotas.
3. **Editar** cualquier registro seleccionándolo en la tabla y haciendo clic en "Editar".
4. **Eliminar** un registro seleccionándolo y haciendo clic en "Eliminar".

---

## 📁 Estructura del Proyecto

```
PeluqueriaCanina/
├── pom.xml                          # Configuración Maven y dependencias
├── README.md                        # Este archivo
└── src/
    └── main/
        ├── java/com/mycompany/peluqueriacanina/
        │   ├── PeluqueriaCanina.java           # Clase principal (main)
        │   ├── igu/                            # Capa de presentación
        │   │   ├── Principal.java              # Ventana principal
        │   │   ├── CargaDatos.java             # Formulario de alta
        │   │   ├── VerDatos.java               # Tabla de consulta
        │   │   └── EditarDatos.java            # Formulario de edición
        │   ├── logica/                         # Capa de lógica de negocio
        │   │   ├── ControladoraLogica.java      # Controlador de negocio
        │   │   ├── Mascota.java                # Entidad JPA - Mascota
        │   │   └── Duenio.java                 # Entidad JPA - Dueño
        │   └── persistencia/                   # Capa de persistencia
        │       ├── ControladoraPersistencia.java # Fachada de persistencia
        │       ├── MascotaJpaController.java    # DAO de Mascota
        │       ├── DuenioJpaController.java     # DAO de Dueño
        │       └── exceptions/                  # Excepciones personalizadas
        └── resources/
            └── META-INF/
                └── persistence.xml             # Configuración JPA
```

---

## 🗄 Modelo de Datos

### Entidades

```
┌──────────────────────┐       ┌──────────────────────────────┐
│       Duenio         │       │          Mascota             │
├──────────────────────┤       ├──────────────────────────────┤
│ id_duenio (PK, auto) │◄──────│ num_cliente (PK, auto)       │
│ nombre               │  1:1  │ nombre                       │
│ celDuenio            │       │ raza                         │
└──────────────────────┘       │ color                        │
                               │ alergico                     │
                               │ atencion_especial            │
                               │ observaciones                │
                               │ unDuenio (FK → Duenio)       │
                               └──────────────────────────────┘
```

**Relación:** Cada `Mascota` está vinculada a un `Duenio` mediante una relación **@OneToOne** unidireccional.

---

## 👤 Autor

Desarrollado por **Ezequiel Barco Palacios** como proyecto de práctica en Java con JPA y Swing.
