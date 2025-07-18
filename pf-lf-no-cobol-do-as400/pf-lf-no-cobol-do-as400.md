# Manipulação de arquivos PF/LF no COBOL do AS/400

## Índice

- [1. Introdução](#1-introdução)
- [2. Conceitos: PF e LF no IBM i](#2-conceitos-pf-e-lf-no-ibm-i)
- [3. Tipos de Acesso em COBOL](#3-tipos-de-acesso-em-cobol)
- [4. Exemplo Prático de Uso de PF e LF](#4-exemplo-prático-de-uso-de-pf-e-lf)
- [5. Declaração no COBOL: SELECT e FD](#5-declaração-no-cobol-select-e-fd)
- [6. Comandos COBOL para Arquivos PF/LF](#6-comandos-cobol-para-arquivos-pflf)
- [7. Considerações de Performance](#7-considerações-de-performance)
- [8. Considerações sobre Locking, Buffer e Concurrency](#8-consideracoes-sobre-locking-buffe-e-concurrency)
- [9. Diferenças para o ambiente z/OS](#9-diferencas-para-o-ambiente-z-os)
- [10. Boas Práticas e Cuidados](#10-boas-praticas-e-cuidados)
- [11. Fontes Oficiais e Links Diretos](#11-fontes-oficiais-e-links-diretos)

---

## 1. Introdução

No ambiente IBM i (AS/400), os arquivos físicos (PF) e arquivos lógicos (LF) representam a forma como os dados são armazenados e acessados. O COBOL pode manipular diretamente esses arquivos com comandos nativos da linguagem.

---

## 2. Conceitos: PF e LF no IBM i

- **PF (Physical File)**: armazena os dados propriamente ditos.
- **LF (Logical File)**: é uma "visão lógica" sobre o PF, podendo aplicar ordenações, filtros e chaves alternativas.

Um LF pode ter:
- uma chave diferente da do PF
- uma seleção ou omissão de registros
- ordenação distinta

---

## 3. Tipos de Acesso em COBOL

O COBOL permite diferentes modos de acesso:

- **Sequential**: leitura linha a linha (NEXT RECORD)
- **Random**: leitura direta via chave (READ KEY)
- **Dynamic**: combina os dois acima

Dependendo do tipo de acesso definido na cláusula `ORGANIZATION` e `ACCESS MODE`, o COBOL definirá a forma como o arquivo será manipulado.

---

## 4. Exemplo Prático de Uso de PF e LF

Suponha que temos:

- Um **PF chamado CLIENTESPF**
- Um **LF chamado CLIENTESLF** com chave composta por NOME + UF

```cobol
SELECT CLIENTE-ARQ
    ASSIGN TO DATABASE-CLIENTESLF
    ORGANIZATION IS INDEXED
    ACCESS MODE IS DYNAMIC
    RECORD KEY IS CLIENTE-CHAVE.
```

Essa definição permite acessar os dados fisicamente contidos no PF, porém através do índice lógico do LF.

---

## 5. Declaração no COBOL: SELECT e FD

A cláusula `SELECT` define o nome lógico para o arquivo.

```cobol
SELECT ARQUIVO-CLIENTE
    ASSIGN TO DATABASE-CLIENTESPF
    ORGANIZATION IS INDEXED
    ACCESS MODE IS RANDOM
    RECORD KEY IS CODIGO-CLIENTE.
```

Na `FILE SECTION`:

```cobol
FD ARQUIVO-CLIENTE
   LABEL RECORDS ARE STANDARD
   RECORD CONTAINS 80 CHARACTERS
   BLOCK CONTAINS 0 RECORDS
   DATA RECORD IS REG-CLIENTE.

01 REG-CLIENTE.
   05 CODIGO-CLIENTE     PIC X(05).
   05 NOME-CLIENTE       PIC X(40).
   05 UF-CLIENTE         PIC X(02).
   05 TELEFONE           PIC X(10).
```

---

## 6. Comandos COBOL para Arquivos PF/LF

- **OPEN INPUT / OUTPUT / I-O / EXTEND**
- **READ**, **READ NEXT**, **READ KEY IS**
- **WRITE**
- **REWRITE**
- **DELETE**
- **CLOSE**

Exemplo:

```cobol
OPEN INPUT ARQUIVO-CLIENTE.
READ ARQUIVO-CLIENTE NEXT RECORD
    AT END
        DISPLAY "FIM DE ARQUIVO".
CLOSE ARQUIVO-CLIENTE.
```

---


## 7. Considerações de Performance

- LF bem desenhados com chaves otimizadas melhoram muito a performance de busca via READ KEY.
- Evite acessos FULL SCAN se possível — prefira usar índices com filtros em LFs.
- O compilador COBOL no IBM i é altamente integrado com o DDS dos arquivos, garantindo performance elevada quando bem configurado.

---

## 8. Considerações sobre Locking, Buffer e Concurrency

- Ao abrir um arquivo em modo `I-O`, registros podem ser bloqueados automaticamente.
- Usar o parâmetro `USING LOCK MODE` (ou definir via DDS).
- O sistema IBM i pode usar buffering avançado, especialmente em acesso SEQUENCIAL.
- Recomenda-se atenção com simultaneidade em ambientes com múltiplos jobs.

---

## 9. Diferenças para o ambiente z/OS

| Característica        | AS/400 (IBM i)                  | z/OS                             |
|-----------------------|----------------------------------|----------------------------------|
| Sistema de Arquivos   | Integrado, nativo               | VSAM, datasets                   |
| Definição externa     | DDS (ou DDL com SQL moderno)    | JCL + Catalog/DCLGEN             |
| Interface com COBOL   | Direta com SELECT/ASSIGN        | COPY/INCLUDE de estruturas VSAM  |
| Locking/Sharing       | Controlado pelo sistema         | Necessário uso explícito         |

---

## 10. Boas Práticas e Cuidados

- Verifique sempre a existência do arquivo com comandos CL (e.g. `DSPFD`, `WRKOBJ`)
- Use nomes de arquivos consistentes entre DDS e SELECT no COBOL
- Prefira leitura SEQUENCIAL com CHAVE definida para grandes volumes
- Em programas com escrita e leitura, abra o arquivo em modo `I-O`
- Monitore o uso de `LOCK` em ambientes concorrentes para evitar deadlocks

---


## 11. Fontes Oficiais e Links Diretos

- [📄 Manipulating Database Files with COBOL on IBM i (IBM Documentation)](https://www.ibm.com/docs/en/i/7.5?topic=programs-manipulating-database-files-cobol)
- [📄 ILE COBOL Programmer's Guide – Working with Database Files](https://www.ibm.com/docs/en/i/7.5?topic=guide-working-database-files)
- [📄 Introduction to PF and LF – IBM i Database Files Concepts](https://www.ibm.com/docs/en/i/7.5?topic=overview-database-files)
- [📄 DDS Reference for LF/PF – IBM i Data Description Specifications](https://www.ibm.com/docs/en/i/7.5?topic=specifications-data-description-dds)
- [📄 Best Practices: Using Logical Files for Performance (IBM)](https://www.ibm.com/docs/en/i/7.5?topic=files-using-logical-performance)

