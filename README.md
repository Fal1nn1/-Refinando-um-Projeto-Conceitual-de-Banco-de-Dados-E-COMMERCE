# -Refinando-um-Projeto-Conceitual-de-Banco-de-Dados-E-COMMERCE

-- Tabela para armazenar informações do cliente
CREATE TABLE Usuarios (
    idUsuario INT PRIMARY KEY,
    nomeCompleto VARCHAR(100),
    tipoUsuario CHAR(2) CHECK(tipoUsuario IN ('PJ', 'PF'))
);

-- Tabela para armazenar informações específicas do cliente PJ
CREATE TABLE UsuariosPJ (
    idUsuario INT PRIMARY KEY,
    cnpj VARCHAR(14),
    nomeFantasia VARCHAR(100),
    FOREIGN KEY (idUsuario) REFERENCES Usuarios(idUsuario)
);

-- Tabela para armazenar informações específicas do cliente PF
CREATE TABLE UsuariosPF (
    idUsuario INT PRIMARY KEY,
    cpf VARCHAR(11),
    dataNasc DATE,
    FOREIGN KEY (idUsuario) REFERENCES Usuarios(idUsuario)
);

-- Tabela para armazenar diferentes formas de pagamento
CREATE TABLE OpcoesPagamento (
    idOpcaoPagamento INT PRIMARY KEY,
    tipoPagamento VARCHAR(50)
);

-- Tabela para armazenar os métodos de pagamento usados por cada cliente
CREATE TABLE PagamentosUsuarios (
    idUsuario INT,
    idOpcaoPagamento INT,
    PRIMARY KEY (idUsuario, idOpcaoPagamento),
    FOREIGN KEY (idUsuario) REFERENCES Usuarios(idUsuario),
    FOREIGN KEY (idOpcaoPagamento) REFERENCES OpcoesPagamento(idOpcaoPagamento)
);

-- Tabela para armazenar informações do pedido
CREATE TABLE Compras (
    idCompra INT PRIMARY KEY,
    idUsuario INT,
    dataCompra DATE,
    FOREIGN KEY (idUsuario) REFERENCES Usuarios(idUsuario)
);

-- Tabela para armazenar informações de entrega
CREATE TABLE Envios (
    idEnvio INT PRIMARY KEY,
    idCompra INT,
    statusEnvio VARCHAR(20),
    codigoRastreio VARCHAR(20),
    FOREIGN KEY (idCompra) REFERENCES Compras(idCompra)
);
