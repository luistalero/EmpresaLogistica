# EmpresaLogistica
## Creación de tablas
```sql
CREATE TABLE Pais (
    ID_Pais INT AUTO_INCREMENT,
    Nombre_Pais VARCHAR(100) NOT NULL,
    PRIMARY KEY (ID_Pais)
);

CREATE TABLE Ciudad (
    ID_Ciudad INT AUTO_INCREMENT,
    Nombre_Ciudad VARCHAR(100) NOT NULL,
    ID_Pais INT,
    PRIMARY KEY (ID_Ciudad),
    CONSTRAINT FK_Ciudad_Pais FOREIGN KEY (ID_Pais) REFERENCES Pais(ID_Pais)
);

CREATE TABLE Sucursal (
    ID_Sucursal INT AUTO_INCREMENT,
    Nombre_Sucursal VARCHAR(100) NOT NULL,
    Direccion VARCHAR(255) NOT NULL,
    ID_Ciudad INT,
    PRIMARY KEY (ID_Sucursal),
    CONSTRAINT FK_Sucursal_Ciudad FOREIGN KEY (ID_Ciudad) REFERENCES Ciudad(ID_Ciudad)
);

CREATE TABLE Cliente (
    ID_Cliente INT AUTO_INCREMENT,
    Nombre_Cliente VARCHAR(100) NOT NULL,
    Correo VARCHAR(100) NOT NULL,
    Telefono VARCHAR(20),
    Direccion VARCHAR(255),
    Cedula VARCHAR(20) NOT NULL,
    PRIMARY KEY (ID_Cliente)
);

CREATE TABLE Paquete (
    ID_Paquete INT AUTO_INCREMENT,
    Numero_Seguimiento VARCHAR(50) NOT NULL,
    Peso DECIMAL(10, 2),
    Dimensiones VARCHAR(50),
    Contenido VARCHAR(255),
    Valor_Declarado DECIMAL(10, 2),
    PRIMARY KEY (ID_Paquete)
);

CREATE TABLE Vehiculo (
    ID_Vehiculo INT AUTO_INCREMENT,
    Placa_Vehiculo VARCHAR(20) NOT NULL,
    Capacidad DECIMAL(10, 2),
    Tipo VARCHAR(50),
    PRIMARY KEY (ID_Vehiculo)
);

CREATE TABLE Conductor (
    ID_Conductor INT AUTO_INCREMENT,
    Nombre_Conductor VARCHAR(100) NOT NULL,
    Telefono_Conductor VARCHAR(20),
    Cedula VARCHAR(20) NOT NULL,
    PRIMARY KEY (ID_Conductor)
);

CREATE TABLE Ruta (
    ID_Ruta INT AUTO_INCREMENT,
    Descripcion_Ruta VARCHAR(255) NOT NULL,
    ID_Vehiculo INT,
    ID_Conductor INT,
    PRIMARY KEY (ID_Ruta),
    CONSTRAINT FK_Ruta_Vehiculo FOREIGN KEY (ID_Vehiculo) REFERENCES Vehiculo(ID_Vehiculo),
    CONSTRAINT FK_Ruta_Conductor FOREIGN KEY (ID_Conductor) REFERENCES Conductor(ID_Conductor)
);

CREATE TABLE Auxiliar_de_Reparto (
    ID_Auxiliar INT AUTO_INCREMENT,
    Nombre_Auxiliar VARCHAR(100) NOT NULL,
    Telefono_Auxiliar VARCHAR(20),
    Cedula VARCHAR(20) NOT NULL,
    PRIMARY KEY (ID_Auxiliar)
);

CREATE TABLE Envio (
    ID_Envio INT AUTO_INCREMENT,
    Fecha_Envio DATE NOT NULL,
    Estado VARCHAR(50),
    ID_Cliente INT,
    ID_Paquete INT,
    ID_Ruta INT,
    ID_Sucursal INT,
    ID_Auxiliar INT,
    PRIMARY KEY (ID_Envio),
    CONSTRAINT FK_Envio_Cliente FOREIGN KEY (ID_Cliente) REFERENCES Cliente(ID_Cliente),
    CONSTRAINT FK_Envio_Paquete FOREIGN KEY (ID_Paquete) REFERENCES Paquete(ID_Paquete),
    CONSTRAINT FK_Envio_Ruta FOREIGN KEY (ID_Ruta) REFERENCES Ruta(ID_Ruta),
    CONSTRAINT FK_Envio_Sucursal FOREIGN KEY (ID_Sucursal) REFERENCES Sucursal(ID_Sucursal),
    CONSTRAINT FK_Envio_Auxiliar FOREIGN KEY (ID_Auxiliar) REFERENCES Auxiliar_de_Reparto(ID_Auxiliar)
);

CREATE TABLE Evento_de_Seguimiento (
    ID_Evento INT AUTO_INCREMENT,
    Fecha_Evento DATE NOT NULL,
    Ubicacion VARCHAR(255) NOT NULL,
    Estado_Paquete VARCHAR(50),
    ID_Paquete INT,
    PRIMARY KEY (ID_Evento),
    CONSTRAINT FK_Evento_Paquete FOREIGN KEY (ID_Paquete) REFERENCES Paquete(ID_Paquete)
);

```
## Contenido de las Tablas
```sql
INSERT INTO Pais (Nombre_Pais) VALUES 
('Colombia'),
('Ecuador'),
('Perú'),
('México'),
('Argentina');

INSERT INTO Ciudad (Nombre_Ciudad, ID_Pais) VALUES 
('Bogotá', 1),
('Medellín', 1),
('Cali', 1),
('Quito', 2),
('Lima', 3),
('Ciudad de México', 4),
('Buenos Aires', 5);

INSERT INTO Sucursal (Nombre_Sucursal, Direccion, ID_Ciudad) VALUES 
('Sucursal Centro Bogotá', 'Calle 26 #12-45', 1),
('Sucursal Norte Medellín', 'Carrera 70 #43-12', 2),
('Sucursal Sur Cali', 'Avenida 3N #23-40', 3),
('Sucursal Principal Quito', 'Av. 6 de Diciembre N34-45', 4),
('Sucursal Centro Lima', 'Av. Arequipa 1235', 5);

INSERT INTO Cliente (Nombre_Cliente, Correo, Telefono, Direccion, Cedula) VALUES 
('Juan Pérez', 'juan.perez@email.com', '3001234567', 'Calle 45 #23-12', '80123456'),
('María López', 'maria.lopez@email.com', '3109876543', 'Carrera 30 #15-45', '79876543'),
('Carlos Rodríguez', 'carlos.rod@email.com', '3203456789', 'Avenida 68 #56-78', '81234567'),
('Ana Martínez', 'ana.martinez@email.com', '3154567890', 'Calle 80 #45-67', '82345678'),
('Pedro Gómez', 'pedro.gomez@email.com', '3167890123', 'Carrera 7 #45-23', '83456789'),
('Laura Sánchez', 'laura.sanchez@email.com', '3178901234', 'Avenida 2 #34-56', '84567890'),
('Ricardo Torres', 'ricardo.torres@email.com', '3189012345', 'Carrera 3 #45-67', '85678901');

INSERT INTO Paquete (Numero_Seguimiento, Peso, Dimensiones, Contenido, Valor_Declarado) VALUES 
('PKT001', 5.2, '30x25x20', 'Documentos', 150000.00),
('PKT002', 10.5, '50x40x30', 'Ropa', 300000.00),
('PKT003', 2.3, '20x15x10', 'Electrónicos', 800000.00),
('PKT004', 15.7, '60x45x35', 'Libros', 250000.00),
('PKT005', 7.8, '40x30x25', 'Accesorios', 450000.00),
('PKT006', 3.0, '25x20x15', 'Ropa', 120000.00),
('PKT007', 4.0, '30x25x20', 'Zapatos', 150000.00),
('PKT008', 2.0, '20x15x10', 'Accesorios', 90000.00),
('PKT009', 6.5, '35x30x25', 'Equipos electrónicos', 500000.00),
('PKT010', 8.0, '45x35x30', 'Herramientas', 350000.00);

INSERT INTO Vehiculo (Placa_Vehiculo, Capacidad, Tipo) VALUES 
('ABC123', 1000.00, 'Camión'),
('DEF456', 500.00, 'Furgoneta'),
('GHI789', 2000.00, 'Camión Grande'),
('JKL012', 750.00, 'Furgoneta'),
('MNO345', 1500.00, 'Camión');

INSERT INTO Conductor (Nombre_Conductor, Telefono_Conductor, Cedula) VALUES 
('Luis Ramírez', '3201234567', '91234567'),
('José García', '3112345678', '92345678'),
('Roberto Sánchez', '3123456789', '93456789'),
('Miguel Torres', '3134567890', '94567890'),
('Diego Castro', '3145678901', '95678901');

INSERT INTO Ruta (Descripcion_Ruta, ID_Vehiculo, ID_Conductor) VALUES 
('Ruta Norte Bogotá', 1, 1),
('Ruta Sur Medellín', 2, 2),
('Ruta Centro Cali', 3, 3),
('Ruta Este Quito', 4, 4),
('Ruta Oeste Lima', 5, 5);

INSERT INTO Auxiliar_de_Reparto (Nombre_Auxiliar, Telefono_Auxiliar, Cedula) VALUES 
('Fernando López', '3156789012', '96789012'),
('Ricardo Mejía', '3167890123', '97890123'),
('Santiago Díaz', '3178901234', '98901234'),
('Andrés Vargas', '3189012345', '99012345'),
('Juan Morales', '3190123456', '90123456');

INSERT INTO Envio (Fecha_Envio, Estado, ID_Cliente, ID_Paquete, ID_Ruta, ID_Sucursal, ID_Auxiliar) VALUES 
('2024-01-01', 'Entregado', 1, 1, 1, 1, 1),
('2024-01-03', 'Entregado', 1, 2, 1, 1, 1),
('2024-01-05', 'Entregado', 1, 3, 1, 1, 1),
('2024-01-07', 'En tránsito', 1, 4, 1, 1, 1),
('2024-01-09', 'Pendiente', 1, 5, 1, 1, 1),
('2024-01-11', 'Entregado', 2, 6, 2, 2, 2),
('2024-01-13', 'Entregado', 2, 7, 2, 2, 2),
('2024-01-15', 'En tránsito', 2, 8, 2, 2, 2),
('2024-01-17', 'Pendiente', 2, 9, 2, 2, 2),
('2024-01-19', 'Entregado', 3, 10, 3, 3, 3);

INSERT INTO Evento_de_Seguimiento (Fecha_Evento, Ubicacion, Estado_Paquete, ID_Paquete) VALUES 
('2024-01-01', 'Centro de distribución Bogotá', 'Recibido', 1),
('2024-01-02', 'En ruta', 'En tránsito', 1),
('2024-01-03', 'Sucursal destino', 'En sucursal', 1),
('2024-01-04', 'Dirección final', 'Entregado', 1),
('2024-01-03', 'Centro de distribución Medellín', 'Recibido', 2),
('2024-01-04', 'En ruta', 'En tránsito', 2),
('2024-01-05', 'Sucursal destino', 'En sucursal', 2),
('2024-01-06', 'Dirección final', 'Entregado', 2),

('2024-01-05', 'Centro de distribución Cali', 'Recibido', 3),
('2024-01-06', 'En ruta', 'En tránsito', 3),
('2024-01-07', 'Sucursal destino', 'En sucursal', 3),
('2024-01-08', 'Dirección final', 'Entregado', 3),

('2024-01-15', 'Centro distribución Quito', 'En proceso', 4),
('2024-01-16', 'Centro distribución Lima', 'En clasificación', 5),
('2024-01-17', 'Sucursal Medellín', 'En proceso de entrega', 6),
('2024-01-18', 'Sucursal Bogotá', 'En clasificación', 7),
('2024-01-19', 'Centro distribución Cali', 'En ruta final', 8);

```
## Consultas
```sql
SELECT 
    e.ID_Envio,
    c.Nombre_Cliente,
    p.Numero_Seguimiento,
    e.Fecha_Envio,
    e.Estado
FROM Envio e
JOIN Cliente c ON e.ID_Cliente = c.ID_Cliente
JOIN Paquete p ON e.ID_Paquete = p.ID_Paquete;

SELECT 
    c.Nombre_Cliente,
    c.Correo,
    (SELECT COUNT(*) FROM Envio e WHERE e.ID_Cliente = c.ID_Cliente) as Total_Envios
FROM Cliente c
WHERE (SELECT COUNT(*) FROM Envio e WHERE e.ID_Cliente = c.ID_Cliente) > 3;

SELECT 
    p.Numero_Seguimiento,
    e.Estado as Estado_Envio,
    es.Fecha_Evento,
    es.Ubicacion,
    es.Estado_Paquete
FROM Paquete p
JOIN Envio e ON p.ID_Paquete = e.ID_Paquete
JOIN Evento_de_Seguimiento es ON p.ID_Paquete = es.ID_Paquete
ORDER BY es.Fecha_Evento;

SELECT 
    p.Nombre_Pais,
    c.Nombre_Ciudad,
    s.Nombre_Sucursal,
    COUNT(e.ID_Envio) as Total_Envios
FROM Sucursal s
JOIN Ciudad c ON s.ID_Ciudad = c.ID_Ciudad
JOIN Pais p ON c.ID_Pais = p.ID_Pais
LEFT JOIN Envio e ON s.ID_Sucursal = e.ID_Sucursal
GROUP BY p.Nombre_Pais, c.Nombre_Ciudad, s.Nombre_Sucursal
ORDER BY Total_Envios DESC;

SELECT DISTINCT 
    c.Nombre_Conductor,
    c.Telefono_Conductor
FROM Conductor c
WHERE c.ID_Conductor IN (
    SELECT r.ID_Conductor 
    FROM Ruta r
    JOIN Envio e ON r.ID_Ruta = e.ID_Ruta
    JOIN Paquete p ON e.ID_Paquete = p.ID_Paquete
    WHERE p.Valor_Declarado > 1000
);

SELECT 
    ar.Nombre_Auxiliar,
    COUNT(e.ID_Envio) as Total_Entregas,
    AVG(p.Peso) as Peso_Promedio_Paquetes,
    SUM(p.Valor_Declarado) as Valor_Total_Entregado
FROM Auxiliar_de_Reparto ar
LEFT JOIN Envio e ON ar.ID_Auxiliar = e.ID_Auxiliar
LEFT JOIN Paquete p ON e.ID_Paquete = p.ID_Paquete
GROUP BY ar.ID_Auxiliar, ar.Nombre_Auxiliar;

SELECT 
    c.Nombre_Ciudad,
    (
        SELECT COUNT(*)
        FROM Envio e
        JOIN Sucursal s ON e.ID_Sucursal = s.ID_Sucursal
        WHERE s.ID_Ciudad = c.ID_Ciudad
        AND e.Estado = 'Pendiente'
    ) as Paquetes_Pendientes
FROM Ciudad c
HAVING Paquetes_Pendientes > 0
ORDER BY Paquetes_Pendientes DESC;

SELECT 
    p.Numero_Seguimiento,
    MIN(es.Fecha_Evento) as Fecha_Inicio,
    MAX(es.Fecha_Evento) as Fecha_Fin,
    DATEDIFF(MAX(es.Fecha_Evento), MIN(es.Fecha_Evento)) as Dias_Totales
FROM Paquete p
JOIN Evento_de_Seguimiento es ON p.ID_Paquete = es.ID_Paquete
GROUP BY p.ID_Paquete, p.Numero_Seguimiento
HAVING Dias_Totales > 0
ORDER BY Dias_Totales DESC;

```

Hecho por (Luis Alberto Talero Martinez)

> [!NOTE]
> complicaciones 

> [!TIP]
> 

> [!IMPORTANT]  
> se encuentra culminado 

> [!WARNING]  
> 

> [!CAUTION]
>
