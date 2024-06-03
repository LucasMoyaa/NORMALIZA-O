-- Criação das tabelas

CREATE TABLE Veículo (
    CodVeiculo INT PRIMARY KEY,
    Marca VARCHAR(50),
    Modelo VARCHAR(50),
    Ano INT
);

CREATE TABLE Cliente (
    CodCliente INT PRIMARY KEY,
    Nome VARCHAR(100),
    CPF VARCHAR(11),
    Endereço VARCHAR(200)
);

CREATE TABLE Locacao (
    CodLocacao INT PRIMARY KEY,
    DataInicio DATE,
    DataFim DATE,
    ValorTotal DECIMAL(10,2),
    CodVeiculo INT FOREIGN KEY REFERENCES Veículo(CodVeiculo),
    CodCliente INT FOREIGN KEY REFERENCES Cliente(CodCliente)
);

-- Criação da view

CREATE VIEW VW_LocacoesComVeiculosEClientes AS
SELECT
    L.CodLocacao,
    L.DataInicio,
    L.DataFim,
    L.ValorTotal,
    V.Marca,
    V.Modelo,
    V.Ano,
    C.Nome AS NomeCliente,
    C.CPF,
    C.Endereço
FROM
    Locacao L
    JOIN Veículo V ON L.CodVeiculo = V.CodVeiculo
    JOIN Cliente C ON L.CodCliente = C.CodCliente;
