--Descrição do MFD

O banco de dados é composto por quatro tabelas principais:

**Categorias

Armazena as categorias dos produtos, como "Bebidas" ou "Alimentos".
Cada categoria possui um identificador único (id) e um nome único (nome).

**Produtos

Armazena os produtos disponíveis no cardápio, com informações como nome, descrição, preço e a categoria a que pertencem.
Está relacionado à tabela categorias.

**Pedidos

Representa os pedidos realizados pelos clientes, com um status e o valor total.

**Itens_pedido

Detalha os itens individuais que compõem cada pedido, associando os produtos aos pedidos.


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Este projeto define um sistema básico para gerenciar categorias, produtos, pedidos e itens de pedidos em um banco de dados relacional. 
Ele utiliza tabelas SQL para organizar e armazenar dados relacionados a um cenário de comércio eletrônico ou controle de estoque.

--Estrutura do Banco de Dados

1. **Tabela de Categorias (categorias)

Esta tabela armazena as categorias de produtos.

Colunas:

id: Identificador único da categoria (chave primária).

nome: Nome da categoria, deve ser único.

SQL:

CREATE TABLE categorias (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL UNIQUE
);

------------------------------------------
2. **Tabela de Produtos (produtos)

Esta tabela armazena informações dos produtos.

Colunas:

id: Identificador único do produto (chave primária).

nome: Nome do produto.

descricao: Descrição detalhada do produto.

preco: Preço do produto.

categoria_id: Relaciona o produto a uma categoria específica (chave estrangeira).

SQL:

CREATE TABLE produtos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT,
    preco DECIMAL(10, 2) NOT NULL,
    categoria_id INT,
    FOREIGN KEY (categoria_id) REFERENCES categorias(id)
);

-------------------------------------------
3. **Tabela de Pedidos (pedidos)

Esta tabela armazena os pedidos realizados pelos clientes.

Colunas:

id: Identificador único do pedido (chave primária).

status: Status atual do pedido (valor padrão: em espera).

valor_total: Valor total do pedido.

SQL:

CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    status VARCHAR(20) NOT NULL DEFAULT 'em espera',
    valor_total DECIMAL(10, 2)
);

-----------------------------------------------
4. **Tabela de Itens do Pedido (itens_pedido)

Esta tabela armazena os itens de cada pedido, detalhando os produtos incluídos.

Colunas:

id: Identificador único do item do pedido (chave primária).

pedido_id: Identificador do pedido ao qual o item pertence (chave estrangeira).

produto_id: Identificador do produto incluído no pedido (chave estrangeira).

quantidade: Quantidade do produto.

subtotal: Subtotal do produto (preço multiplicado pela quantidade).

SQL:

CREATE TABLE itens_pedido (
    id INT AUTO_INCREMENT PRIMARY KEY,
    pedido_id INT NOT NULL,
    produto_id INT NOT NULL,
    quantidade INT NOT NULL,
    subtotal DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (pedido_id) REFERENCES pedidos(id),
    FOREIGN KEY (produto_id) REFERENCES produtos(id)
);

------------------------------------------------------------------------------------------
Relacionamentos entre as Tabelas

A tabela categorias está relacionada com a tabela produtos através de categoria_id.

A tabela pedidos está relacionada com a tabela itens_pedido através de pedido_id.

A tabela produtos está relacionada com a tabela itens_pedido através de produto_id.
