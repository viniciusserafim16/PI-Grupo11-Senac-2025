# Diagrama de Classes – Sistema de Gestão Universitária

> **Escopo:** modelagem do domínio para cadastros de **Pessoa Física**, **Pessoa Jurídica**, **Aluno**, **Professor**, **Fornecedor** e **Responsável Legal**.

## 1) Visão Geral

- **Pessoa** é a superclasse que concentra atributos comuns (nome, e-mail, telefone).
- **PessoaFisica** e **PessoaJuridica** especializam **Pessoa**.
- **Aluno** e **Professor** especializam **PessoaFisica**.
- **Fornecedor** especializa **PessoaJuridica**.
- **ResponsavelLegal** se **associa** a **Aluno** (relação N:N por padrão, permitindo múltiplos responsáveis por aluno e um responsável para vários alunos).

## 2) Diagrama (Mermaid)

> GitHub renderiza automaticamente.

classDiagram
    direction TB

    class Pessoa {
      <<abstract>>
      - nome: String
      - email: String
      - telefone: String
    }

    class PessoaFisica {
      - cpf: String
      - dataNascimento: Date
    }

    class PessoaJuridica {
      - cnpj: String
      - razaoSocial: String
    }

    class Aluno {
      - matricula: String
      - curso: String
    }

    class Professor {
      - areaAtuacao: String
      - titulacao: String
    }

    class Fornecedor {
      - segmento: String
    }

    class ResponsavelLegal {
      - nome: String
      - telefone: String
      - parentesco: String
    }

    Pessoa <|-- PessoaFisica
    Pessoa <|-- PessoaJuridica
    PessoaFisica <|-- Aluno
    PessoaFisica <|-- Professor
    PessoaJuridica <|-- Fornecedor

    %% Associação N:N entre Aluno e ResponsavelLegal
    Aluno "0..*" -- "0..*" ResponsavelLegal : é assistido por / assiste
