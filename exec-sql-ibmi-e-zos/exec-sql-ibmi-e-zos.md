# 📄 Exemplos de EXEC SQL comparando IBM i e z/OS

## 📑 Índice

- [1. Introdução](#1-introdução)
- [2. Ambiente IBM i (AS/400)](#2-ambiente-ibm-i-as400)
- [3. Ambiente z/OS](#3-ambiente-zos)
- [4. Comparação direta](#4-comparação-direta)
- [5. Considerações práticas](#5-considerações-práticas)
- [6. Fontes Oficiais e Links Diretos](#6-fontes-oficiais-e-links-diretos)

---

## 1. Introdução

A integração entre COBOL e SQL é uma prática comum tanto no IBM i (AS/400) quanto no z/OS. Apesar das linguagens seguirem o padrão ANSI SQL, há diferenças notáveis na forma como cada ambiente implementa a interface entre COBOL e o banco de dados, seja DB2 for i ou DB2 for z/OS.

---

## 2. Ambiente IBM i (AS/400)

No IBM i, utiliza-se o compilador ILE COBOL e o banco de dados DB2 for i (integrado ao sistema operacional).

### ✅ Exemplo básico: SELECT

```cobol
EXEC SQL
   SELECT NOME, SALARIO
   INTO :WS-NOME, :WS-SALARIO
   FROM FUNCIONARIOS
   WHERE MATRICULA = :WS-MATRICULA
END-EXEC.
```

### Características:

- Variáveis host iniciam com `:` (ANSI SQL padrão).
- Declaração de cursores é feita no código COBOL.
- Binding dinâmico é possível via embedded SQL.
- É comum a utilização do **CRTSQLCBL** para compilar.

---

## 3. Ambiente z/OS

No z/OS, o compilador utilizado é o Enterprise COBOL, com interface para o DB2 for z/OS.

### ✅ Exemplo equivalente:

```cobol
EXEC SQL
   SELECT NOME, SALARIO
   INTO :WS-NOME, :WS-SALARIO
   FROM DB2DBA.FUNCIONARIOS
   WHERE MATRICULA = :WS-MATRICULA
END-EXEC.
```

### Características:

- Utiliza pré-compilador (DSNHPC).
- Nome qualificado com schema (ex: `DB2DBA.FUNCIONARIOS`) é exigido conforme convenções de catalogação.
- Uso obrigatório de **DCLGEN** para declaração de estruturas de dados compatíveis com o SQL.

---

## 4. Comparação direta

| Aspecto                          | IBM i (AS/400)                        | z/OS                                    |
|----------------------------------|----------------------------------------|------------------------------------------|
| Compilador COBOL                 | ILE COBOL                             | Enterprise COBOL                         |
| Banco de dados                   | DB2 for i                             | DB2 for z/OS                             |
| Pré-compilador necessário        | Não (embutido no CRTSQLCBL)           | Sim (DSNHPC)                             |
| Estruturas DCLGEN                | Opcional                              | Fortemente recomendado                   |
| Sintaxe SQL                      | Semelhante                            | Semelhante                               |
| Qualificação de nomes            | Tabelas locais geralmente não requerem| Exige schema.table                       |
| Binding                          | Dinâmico ou Estático                  | Estático com BIND PLAN                   |
| Ferramentas associadas           | CRTSQLCBL, STRSQL                     | DSNHPC, BIND, SPUFI, QMF                 |

---

## 5. Considerações práticas

- A escrita do código SQL dentro do COBOL é extremamente similar em ambos os ambientes.
- O processo de compilação e *bind* é mais complexo no z/OS, envolvendo geração de *DBRMs* e *Plans*.
- O IBM i oferece uma integração mais direta entre linguagem e banco de dados, com menos etapas.

---

## 6. Fontes Oficiais e Links Diretos

📄 [Using SQL in ILE COBOL Programs – IBM i 7.5](https://www.ibm.com/docs/en/i/7.5?topic=programs-using-sql-in-ile-cobol)

📄 [COBOL and DB2 for z/OS – EXEC SQL syntax](https://www.ibm.com/docs/en/db2-for-zos/12?topic=applications-embedded-sql)

📄 [DB2 for i vs DB2 for z/OS SQL Support – IBM Support](https://www.ibm.com/support/pages/differences-db2-i-and-db2-zos-sql-support)

📄 [Enterprise COBOL Programming Guide – DB2 usage](https://www.ibm.com/docs/en/cobol-zos/6.4?topic=db2-using)

📄 [CRTSQLCBL Command – IBM i SQL COBOL Compilation](https://www.ibm.com/docs/en/i/7.5?topic=ssw_ibm_i_75/cl/crtsqlcbl.htm)
