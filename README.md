# SafeBalance

SafeBalance é um sistema de gerenciamento de finanças pessoais focado em separar e organizar os valores de diferentes clientes, permitindo o registro e controle de movimentações financeiras de forma segura e centralizada.

## Visão Geral do Projeto

O objetivo do SafeBalance é oferecer uma ferramenta onde seja possível gerenciar o saldo de diversas contas pertencentes a diferentes clientes. A cada movimentação financeira, informações como valor, motivo e data serão registradas para manter um histórico detalhado e transparente.

### Tecnologias Utilizadas

- **Backend**: .NET (WebAPI)
- **Frontend**: Angular
- **Banco de Dados**: SQL Server ou outra base compatível com Entity Framework

## Estrutura do Sistema

SafeBalance é baseado em três entidades principais:
1. **Cliente**: Representa o usuário do sistema, que possui uma ou mais contas.
2. **Conta**: Representa a conta financeira de cada cliente, contendo o saldo e o vínculo com o cliente.
3. **Movimentação**: Representa cada operação financeira, com detalhes sobre valor, tipo (depósito ou saque), motivo e data.

## Diagrama de Classes

Abaixo está o diagrama de classes que representa as entidades do sistema e suas relações:

```mermaid
classDiagram
    class Cliente {
        +int Id
        +string Nome
        +string Email
        +List~Conta~ Contas
    }
    
    class Conta {
        +int Id
        +decimal Saldo
        +int ClienteId
        +List~Movimentacao~ Movimentacoes
        +AtualizarSaldo(decimal valor)
    }
    
    class Movimentacao {
        +int Id
        +decimal Valor
        +string Tipo // "Depósito" ou "Saque"
        +string Motivo
        +DateTime Data
    }
    
    Cliente "1" --> "0..*" Conta : possui
    Conta "1" --> "0..*" Movimentacao : realiza
