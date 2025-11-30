# 🏖️ Sistema de Gerenciamento de Barraca (Juca)

Este projeto consiste na modelagem de banco de dados para um sistema de gestão de Barraca de Praia/Quiosque. O objetivo é controlar o fluxo de caixa, estoque de produtos e, principalmente, o **aluguel de equipamentos por hora** (como cadeiras e guarda-sóis).

## 🛠️ Tecnologias Utilizadas

* **MySQL Workbench:** Ferramenta visual para modelagem e criação do Diagrama ER.
* **MySQL / MariaDB:** Sistema Gerenciador de Banco de Dados (SGBD).
* **SQL:** Linguagem utilizada para estruturação do banco (`.sql`).

## 📊 Diagrama Entidade-Relacionamento (DER)

O diagrama abaixo representa a estrutura lógica do banco de dados:

```mermaid
erDiagram
    CLIENTES ||--o{ COMANDAS : "abre"
    COMANDAS ||--o{ ITENS_COMANDA : "possui"
    PRODUTOS ||--o{ ITENS_COMANDA : "é vendido/alugado"
    FUNCIONARIOS ||--o{ ITENS_COMANDA : "atende"
    COMANDAS ||--|| PREMIACOES : "gera"
    COMANDAS ||--|| FATURAMENTOS : "compõe"

    CLIENTES {
        int idClientes PK
        string nomeCliente
    }
    COMANDAS {
        int idComandas PK
        int idClientes FK
        decimal valorTotal
        date data
    }
    ITENS_COMANDA {
        int idItensComanda PK
        int idComanda FK
        int idProdutos FK
        int idFuncionarios FK
        time horaRetirada
        time horaDevolvida
        decimal precoHora
        decimal total
    }
    PRODUTOS {
        int idProdutos PK
        string nomeProduto
        int quantidadesProdutos
    }
    FUNCIONARIOS {
        int idFuncionarios PK
        string nomeFuncionario
    }