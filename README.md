# 🏥 Taller 2.3: Dominio de Joins y Vistas en SQL Server

![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![Oracle](https://img.shields.io/badge/Oracle-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completado-success?style=for-the-badge)

[cite_start]Este repositorio contiene el desarrollo del laboratorio sobre el uso de **Vistas (VIEW)** y **JOINs** aplicado a un caso práctico de gestión clínica ("TodoSalud")[cite: 8, 49, 80].

---

## 📝 Introducción
[cite_start]En este proyecto se aborda el modelado de bases de datos para optimizar el acceso a la información en instituciones de salud[cite: 47]. [cite_start]Se implementan modelos conceptuales, lógicos y físicos para simplificar consultas complejas sin alterar la estructura original de la base de datos[cite: 49, 51].

## 🎯 Objetivos
* [cite_start]**General:** Aplicar conceptos de modelado y vistas para optimizar consultas y mejorar la organización de la información[cite: 54].
* [cite_start]**Específicos:** * Diseñar diagramas entidad-relación (Modelo Conceptual)[cite: 56].
    * [cite_start]Implementar el modelo físico mediante SQL[cite: 57].
    * [cite_start]Crear vistas para simplificar el acceso a datos relacionados[cite: 59].

---

## 🛠️ Fundamento Teórico: ¿Qué es una Vista?
[cite_start]Una **Vista (VIEW)** es una tabla virtual generada a partir de una consulta SQL[cite: 62].
* **Ventajas:**
    * [cite_start]Simplificación de consultas complejas[cite: 71].
    * [cite_start]Mayor seguridad al ocultar datos sensibles[cite: 72].
    * [cite_start]Reutilización de lógica de negocio[cite: 73].
    * [cite_start]Independencia lógica de la estructura de tablas[cite: 74].

---

## 📂 Desarrollo del Laboratorio

### 1. Caso de Estudio: Clínica "TodoSalud"
[cite_start]Se identificaron las siguientes entidades principales[cite: 80, 83]:
* **Pacientes**
* **Médicos**
* **Especialidades**
* **Diagnósticos**
* **Enfermedades**

### 2. Implementación de Vistas (Ejemplos clave)

#### **Vista de Médicos y sus Especialidades**
[cite_start]Relaciona a los médicos con sus áreas de especialización mediante JOINs[cite: 127, 130].
```sql
CREATE OR REPLACE VIEW v_medicos_especialidades AS
SELECT m.*, e.nombreEsp, e.descripcionEsp
FROM tMedico m
JOIN tEspecialidadDelMedico em ON m.codM = em.codM
JOIN tEspecialidad e ON em.codEsp = e.codEsp;
