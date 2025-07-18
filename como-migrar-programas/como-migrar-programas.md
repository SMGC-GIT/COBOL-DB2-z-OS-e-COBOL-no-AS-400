# 🧩 Como migrar programas COBOL entre IBM i (AS/400) e z/OS

## 📌 Índice
- [Introdução](#introdução)
- [Desafios da Migração](#desafios-da-migração)
- [Comparativo de Recursos e Componentes](#comparativo-de-recursos-e-componentes)
- [Etapas da Migração](#etapas-da-migração)
- [Dicas de Compatibilidade](#dicas-de-compatibilidade)
- [Exemplo de Adaptação de Código](#exemplo-de-adaptação-de-código)
- [Fontes Oficiais e Links Diretos](#fontes-oficiais-e-links-diretos)

---

## Introdução

A migração de programas COBOL entre plataformas IBM i (AS/400) e z/OS requer entendimento profundo das particularidades de cada ambiente. Apesar de ambos suportarem COBOL e DB2, há diferenças significativas no uso de arquivos, chamadas de APIs, controle de compilação e execução.

---

## Desafios da Migração

- **Diferença nos formatos de arquivo**: PF/LF em IBM i vs datasets sequenciais/VSAM em z/OS.
- **Execução de comandos e chamadas ao sistema**.
- **Uso de SQL embutido (EXEC SQL)** com diferenças no suporte a funções, sintaxe e delimitadores.
- **Bibliotecas e estrutura de programas** (ex: *libraries* vs *datasets*).
- **Controle de compilação**: uso do CRTCBLMOD e CRTPGM no IBM i vs JCL e PROC no z/OS.

---

## Comparativo de Recursos e Componentes

| Recurso               | IBM i (AS/400)                        | z/OS (Mainframe)                         |
|-----------------------|----------------------------------------|------------------------------------------|
| Arquivos de Dados     | PF, LF                                 | VSAM, QSAM, ESDS                         |
| Comandos do sistema   | CL (Control Language)                  | JCL (Job Control Language)               |
| Compilador COBOL      | ILE COBOL                              | Enterprise COBOL                         |
| Execução SQL          | SQL embutido com suporte a DB2         | EXEC SQL com suporte a DB2               |
| Deployment            | Salvamento em *libraries*              | Cargas em datasets e deploy via JCL      |

---

## Etapas da Migração

1. **Levantamento e inventário** dos programas e arquivos envolvidos.
2. **Análise de compatibilidade** do código COBOL e comandos SQL.
3. **Conversão de arquivos** (ex: de PF/LF para VSAM se necessário).
4. **Adaptação de comandos de sistema** (CL para JCL).
5. **Reescrita ou parametrização de trechos específicos** por plataforma.
6. **Testes unitários e de integração** em ambiente de homologação.
7. **Automação de compilação e deploy no destino**.

---

## Dicas de Compatibilidade

- Verifique delimitadores de strings e nomes de campos SQL (ex: uso de *" ou '*).
- No z/OS, o uso de **DDNAME** em EXEC SQL é obrigatório para arquivos.
- No IBM i, comandos CL como `OVRDBF` não têm equivalente direto em z/OS.
- Se o código COBOL utiliza **APIs do sistema**, avalie reescrever ou encapsular em módulos adaptados.

---

## Exemplo de Adaptação de Código

**IBM i:**

```cobol
EXEC SQL
    SELECT CUSTNAME INTO :NAME
    FROM CUSTMAST
    WHERE CUSTID = :ID
END-EXEC.
```

**z/OS:**

```cobol
EXEC SQL DECLARE C1 CURSOR FOR
    SELECT CUSTNAME
    FROM CUSTMAST
    WHERE CUSTID = :ID
END-EXEC.

EXEC SQL OPEN C1 END-EXEC.
EXEC SQL FETCH C1 INTO :NAME END-EXEC.
EXEC SQL CLOSE C1 END-EXEC.
```

---

## Fontes Oficiais e Links Diretos

📄 [IBM Enterprise COBOL Migration Guide](https://www.ibm.com/docs/en/cobol-zos/6.4?topic=migration-enterprise-cobol)

📄 [ILE COBOL Programmer's Guide – Migrating from z/OS](https://www.ibm.com/docs/en/i/7.5?topic=programs-migrating-cobol-zos)

📄 [DB2 SQL Differences between IBM i and z/OS](https://www.ibm.com/support/pages/sql-differences-between-ibm-i-db2-zos)

📄 [Migrating Workloads to z/OS – IBM Redbooks](https://www.redbooks.ibm.com/redbooks/pdfs/sg248390.pdf)

---

