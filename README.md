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

### Aplicação dos Princípios SOLID

O sistema segue os princípios SOLID:

- **Responsabilidade Única**: Cada classe e método tem uma função específica. Por exemplo, a `Conta` apenas gerencia o saldo e as movimentações, sem tratar de dados pessoais do cliente.
- **Aberto/Fechado**: Métodos para movimentações podem ser estendidos para novos tipos de operações sem alterar o código existente.
- **Substituição de Liskov e Segregação de Interfaces**: A interface `ISaldo` permite controlar o acesso ao saldo e às movimentações.
- **Inversão de Dependência**: `IContaRepository` permite implementar persistência de dados separadamente.

## Diagrama de Classes

Abaixo está o diagrama de classes atualizado, incluindo interfaces para encapsular e proteger dados sensíveis:

```mermaid
classDiagram
    class Cliente {
        +int Id
        +string Nome
        +string Email
        +List~Conta~ Contas
    }

    class Conta {
        -decimal Saldo
        +int ClienteId
        +List~Movimentacao~ Movimentacoes
        +Depositar(decimal valor)
        +Sacar(decimal valor)
        +ConsultarSaldo() decimal
    }

    class Movimentacao {
        +int Id
        +decimal Valor
        +string Tipo // "Depósito" ou "Saque"
        +string Motivo
        +DateTime Data
    }
    
    interface ISaldo {
        +Depositar(decimal valor)
        +Sacar(decimal valor)
        +ConsultarSaldo() decimal
    }

    interface IContaRepository {
        +SalvarConta(Conta conta)
        +BuscarContaPorId(int contaId) Conta
    }

    Cliente "1" --> "0..*" Conta : possui
    Conta "1" --> "0..*" Movimentacao : realiza
    Conta ..|> ISaldo
    Conta ..|> IContaRepository : "implementa"
