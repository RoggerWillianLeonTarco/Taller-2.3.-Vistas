-- 1. ELIMINAR TABLAS
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE tEnfermedadEnElDiagnostico CASCADE CONSTRAINTS';
   EXECUTE IMMEDIATE 'DROP TABLE tEspecialidadDelMedico CASCADE CONSTRAINTS';
   EXECUTE IMMEDIATE 'DROP TABLE tDiagnostico CASCADE CONSTRAINTS';
   EXECUTE IMMEDIATE 'DROP TABLE tEnfermedad CASCADE CONSTRAINTS';
   EXECUTE IMMEDIATE 'DROP TABLE tEspecialidad CASCADE CONSTRAINTS';
   EXECUTE IMMEDIATE 'DROP TABLE tMedico CASCADE CONSTRAINTS';
   EXECUTE IMMEDIATE 'DROP TABLE tPaciente CASCADE CONSTRAINTS';
EXCEPTION WHEN OTHERS THEN NULL;
END;
/
-- 2. CREACIÓN DE TABLAS
CREATE TABLE tPaciente (
    codP VARCHAR2(4) PRIMARY KEY,
    tipoDocP VARCHAR2(15),
    nroDocP VARCHAR2(12),
    paternoP VARCHAR2(50),
    maternoP VARCHAR2(50),
    nombresP VARCHAR2(50),
    fechaNacimientoP DATE,
    generoP CHAR(1)
);

CREATE TABLE tMedico (
    codM VARCHAR2(4) PRIMARY KEY,
    tipoDocM VARCHAR2(15),
    nroDocM VARCHAR2(12),
    paternoM VARCHAR2(50),
    maternoM VARCHAR2(50),
    nombresM VARCHAR2(50),
    celularM VARCHAR2(12),
    fechaNacimientoM DATE,
    generoM CHAR(1)
);

CREATE TABLE tEspecialidad (
    codEsp VARCHAR2(4) PRIMARY KEY,
    nombreEsp VARCHAR2(70),
    descripcionEsp VARCHAR2(100)
);

CREATE TABLE tEnfermedad (
    codE VARCHAR2(4) PRIMARY KEY,
    nombreE VARCHAR2(50),
    descripcionE VARCHAR2(100)
);

CREATE TABLE tDiagnostico (
    codD VARCHAR2(4) PRIMARY KEY,
    fechaHoraD TIMESTAMP,
    descripcionD VARCHAR2(100),
    codP VARCHAR2(4),
    codM VARCHAR2(4),
    FOREIGN KEY (codP) REFERENCES tPaciente(codP),
    FOREIGN KEY (codM) REFERENCES tMedico(codM)
);

CREATE TABLE tEspecialidadDelMedico (
    codEspM VARCHAR2(4) PRIMARY KEY,
    codEsp VARCHAR2(4),
    codM VARCHAR2(4),
    fechaDeObtencion DATE,
    FOREIGN KEY (codEsp) REFERENCES tEspecialidad(codEsp),
    FOREIGN KEY (codM) REFERENCES tMedico(codM)
);

CREATE TABLE tEnfermedadEnElDiagnostico (
    codED VARCHAR2(4) PRIMARY KEY,
    codE VARCHAR2(4),
    codD VARCHAR2(4),
    FOREIGN KEY (codE) REFERENCES tEnfermedad(codE),
    FOREIGN KEY (codD) REFERENCES tDiagnostico(codD)
);


-- 3. INSERCIÓN DE DATOS
INSERT INTO tPaciente VALUES ('P01','DNI','11111111','Salas','Rivas','Juan',TO_DATE('2000-02-02','YYYY-MM-DD'),'M');
INSERT INTO tPaciente VALUES ('P02','DNI','22222222','Perez','Rozas','Elena',TO_DATE('2020-10-01','YYYY-MM-DD'),'F');
INSERT INTO tPaciente VALUES ('P03','DNI','33333333','Lopez','Gomez','Carlos',TO_DATE('1995-05-10','YYYY-MM-DD'),'M');
INSERT INTO tPaciente VALUES ('P04','DNI','44444444','Torres','Diaz','Lucia',TO_DATE('2001-07-15','YYYY-MM-DD'),'F');
INSERT INTO tPaciente VALUES ('P05','DNI','55555555','Vargas','Mendoza','Pedro',TO_DATE('1988-03-20','YYYY-MM-DD'),'M');

INSERT INTO tMedico VALUES ('M1','DNI','33333333','Zela','Ramirez','Javier','999999999',TO_DATE('1970-10-10','YYYY-MM-DD'),'M');
INSERT INTO tMedico VALUES ('M2','Carnet','7777','Cabral','Desousa','Alejandra','988888877',TO_DATE('1975-12-06','YYYY-MM-DD'),'F');
INSERT INTO tMedico VALUES ('M3','DNI','88888888','Rojas','Paredes','Luis','977777777',TO_DATE('1980-01-05','YYYY-MM-DD'),'M');
INSERT INTO tMedico VALUES ('M4','DNI','99999999','Castro','Fernandez','Maria','966666666',TO_DATE('1985-09-12','YYYY-MM-DD'),'F');

INSERT INTO tEspecialidad VALUES ('Esp1','Otorrinolaringologia','Ojos, nariz y boca');
INSERT INTO tEspecialidad VALUES ('Esp2','Pediatria','Neonato, niño y adolescente');
INSERT INTO tEspecialidad VALUES ('Esp3','Cardiologia','Corazon');
INSERT INTO tEspecialidad VALUES ('Esp4','Odontologia','Dientes');
INSERT INTO tEspecialidad VALUES ('Esp5','Dermatologia','Piel');
INSERT INTO tEspecialidad VALUES ('Esp6','Neurologia','Sistema nervioso');

INSERT INTO tEnfermedad VALUES ('E1','Alergia respiratoria','Sistema respiratorio');
INSERT INTO tEnfermedad VALUES ('E2','Sinusitis','Gripe cronica');
INSERT INTO tEnfermedad VALUES ('E3','Artritis','Huesos');
INSERT INTO tEnfermedad VALUES ('E4','Dermatitis','Problemas en la piel');
INSERT INTO tEnfermedad VALUES ('E5','Migraña','Dolor de cabeza intenso');
INSERT INTO tEnfermedad VALUES ('E6','Gripe','Infeccion viral');

INSERT INTO tDiagnostico VALUES ('D1',TO_TIMESTAMP('2022-02-25 10:00:00','YYYY-MM-DD HH24:MI:SS'),'Sinusitis aguda y alergia','P01','M1');
INSERT INTO tDiagnostico VALUES ('D2',TO_TIMESTAMP('2022-02-28 12:00:00','YYYY-MM-DD HH24:MI:SS'),'Niña sana','P02','M2');
INSERT INTO tDiagnostico VALUES ('D3',TO_TIMESTAMP('2022-03-01 09:00:00','YYYY-MM-DD HH24:MI:SS'),'Dermatitis leve','P03','M3');
INSERT INTO tDiagnostico VALUES ('D4',TO_TIMESTAMP('2022-03-02 11:30:00','YYYY-MM-DD HH24:MI:SS'),'Migraña crónica','P04','M4');
INSERT INTO tDiagnostico VALUES ('D5',TO_TIMESTAMP('2022-03-03 15:00:00','YYYY-MM-DD HH24:MI:SS'),'Gripe estacional','P05','M1');

INSERT INTO tEspecialidadDelMedico VALUES ('EM1','Esp1','M1',TO_DATE('2010-12-12','YYYY-MM-DD'));
INSERT INTO tEspecialidadDelMedico VALUES ('EM2','Esp2','M2',TO_DATE('2009-02-02','YYYY-MM-DD'));
INSERT INTO tEspecialidadDelMedico VALUES ('EM3','Esp3','M2',TO_DATE('2019-11-21','YYYY-MM-DD'));
INSERT INTO tEspecialidadDelMedico VALUES ('EM4','Esp5','M3',TO_DATE('2015-06-10','YYYY-MM-DD'));
INSERT INTO tEspecialidadDelMedico VALUES ('EM5','Esp6','M4',TO_DATE('2018-08-20','YYYY-MM-DD'));
INSERT INTO tEspecialidadDelMedico VALUES ('EM6','Esp4','M3',TO_DATE('2020-01-01','YYYY-MM-DD'));

INSERT INTO tEnfermedadEnElDiagnostico VALUES ('ED1','E1','D1');
INSERT INTO tEnfermedadEnElDiagnostico VALUES ('ED2','E2','D1');
INSERT INTO tEnfermedadEnElDiagnostico VALUES ('ED3','E4','D3');
INSERT INTO tEnfermedadEnElDiagnostico VALUES ('ED4','E5','D4');
INSERT INTO tEnfermedadEnElDiagnostico VALUES ('ED5','E6','D5');
COMMIT;

-- RESOLUCIÓN DE EJERCICIOS

-- 5.1. Crear una vista para mostrar todos los datos de los médicos y sus especialidades.
CREATE OR REPLACE VIEW v_medicos_especialidades AS
SELECT m.*, e.nombreEsp, e.descripcionEsp
FROM tMedico m
JOIN tEspecialidadDelMedico em ON m.codM = em.codM
JOIN tEspecialidad e ON em.codEsp = e.codEsp;

-- 5.2. A partir de la vista anterior, mostrar cuántas especialidades tiene cada médico.
-- Ejecución:
SELECT nombresM, paternoM, COUNT(*) AS cantidad_especialidades
FROM v_medicos_especialidades
GROUP BY nombresM, paternoM;

-- 5.3. A partir de la vista anterior, mostrar solamente a los médicos que tengan 2 a más especialidades.
-- Ejecución:
SELECT nombresM, paternoM, COUNT(*) AS cantidad_especialidades
FROM v_medicos_especialidades
GROUP BY nombresM, paternoM
HAVING COUNT(*) >= 2;

-- 5.4. Crear una vista que muestre solamente a las enfermedades que aún no se hayan detectado.
CREATE OR REPLACE VIEW v_enfermedades_no_detectadas AS
SELECT *
FROM tEnfermedad
WHERE codE NOT IN (SELECT codE FROM tEnfermedadEnElDiagnostico);

-- 5.5. Crear una vista que muestre especialidades sin médicos en la Clínica.
CREATE OR REPLACE VIEW v_especialidades_sin_medico AS
SELECT *
FROM tEspecialidad
WHERE codEsp NOT IN (SELECT codEsp FROM tEspecialidadDelMedico);

-- 5.6. A partir de la vista anterior, mostrar cuántas especialidades aún no tienen médico.
-- Ejecución:
SELECT COUNT(*) AS total_especialidades_sin_medico
FROM v_especialidades_sin_medico;

-- 5.7. Crear una vista que muestre los nombres de los pacientes cuyos diagnósticos no tengan enfermedad.
CREATE OR REPLACE VIEW v_pacientes_sin_enfermedad AS
SELECT DISTINCT p.nombresP, p.paternoP, p.maternoP
FROM tPaciente p
JOIN tDiagnostico d ON p.codP = d.codP
WHERE d.codD NOT IN (SELECT codD FROM tEnfermedadEnElDiagnostico);

-- CONSULTA FINAL PARA VER EL RESULTADO DE LA ÚLTIMA VISTA:
SELECT * FROM v_pacientes_sin_enfermedad;

