# 👨‍💻 COBOL Developer em AS/400 (IBM i) vs z/OS (Mainframe)

## 📑 Índice

- [Introdução](#introdução)
- [Quem atua como COBOL Developer no AS/400](#quem-atua-como-cobol-developer-no-as400)
- [Similaridades entre COBOL + DB2 z/OS e COBOL no AS/400](#similaridades-entre-cobol--db2-zos-e-cobol-no-as400)
- [Diferenças entre COBOL no z/OS e no AS/400](#diferenças-entre-cobol-no-zos-e-no-as400)
- [Considerações Técnicas](#considerações-técnicas)
  - [Sobre o COBOL em AS/400](#sobre-o-cobol-em-as400)
  - [Sobre o DB2 no AS/400](#sobre-o-db2-no-as400)
- [Transição entre ambientes](#transição-entre-ambientes)
- [Conclusão](#conclusão)
- [Fontes e Documentação Oficial](#fontes-e-documentação-oficial)

---

## 📌 Introdução

Este documento apresenta um comparativo detalhado entre o papel do desenvolvedor COBOL que atua no ambiente **AS/400 (IBM i)** e aquele que atua no **z/OS (Mainframe)**, abordando **semelhanças, diferenças, tecnologias associadas** e pontos de interseção entre os dois universos.

---

## 👨‍💻 Quem atua como COBOL Developer no AS/400

### 🎯 Perfil profissional:
- Desenvolve, mantém e moderniza sistemas legados em **ILE COBOL** no sistema **IBM i (antigo AS/400)**.
- Presente em **varejo, indústria, serviços de saúde, manufatura e empresas de médio porte**.
- Pode atuar com **RPG**, linguagem nativa e amplamente usada no AS/400.
- Utiliza banco de dados **DB2 for i** e comandos nativos como `STRSQL`, `WRKJOB`, etc.

---

## 🧩 Similaridades entre COBOL + DB2 z/OS e COBOL no AS/400

| Aspecto                       | z/OS (Mainframe)                            | AS/400 (IBM i)                               | Similaridade                                                                 |
|------------------------------|---------------------------------------------|----------------------------------------------|------------------------------------------------------------------------------|
| **Linguagem**                | COBOL (Enterprise COBOL)                   | ILE COBOL                                     | Sintaxe COBOL parecida, com dialetos específicos                             |
| **Banco de Dados**           | DB2 for z/OS                               | DB2 for i (ou apenas "DB2")                   | Ambos usam DB2 relacional com SQL ANSI, porém com nuances                    |
| **Execução batch**           | JCL e programas COBOL                      | CLP (Control Language Programs) + COBOL       | Ambos usam scripts para orquestrar jobs                                     |
| **Uso de arquivos**          | VSAM, Sequential, Indexed                 | Arquivos físicos e lógicos (PF, LF)           | Manipulação de arquivos é muito comum em ambos                              |
| **SQL embutido (Embedded)**  | COBOL + SQL embutido (EXEC SQL)           | COBOL + SQL embutido (EXEC SQL)               | Mesma abordagem, mesmo padrão ANSI                                           |
| **Ambiente fechado (host)**  | z/OS                                       | IBM i (AS/400)                                | São sistemas proprietários da IBM, estáveis e seguros                        |
| **Modernização em pauta**    | APIs, MQ, CICS, Web Services               | APIs REST, DB2 Services, RPG Web Services     | Ambos buscam expor sistemas legados como serviços modernos                   |

---

## ❌ Diferenças entre COBOL no z/OS e no AS/400

| Aspecto                    | z/OS (Mainframe)                                        | AS/400 (IBM i)                                         |
|---------------------------|----------------------------------------------------------|--------------------------------------------------------|
| **Sistema Operacional**   | z/OS                                                     | IBM i (anteriormente OS/400)                          |
| **Compilador**            | Enterprise COBOL (IBM)                                   | ILE COBOL (Integrated Language Environment)           |
| **Job Control**           | JCL (Job Control Language)                               | CLP (Control Language Programs)                       |
| **Banco de Dados**        | DB2 for z/OS                                             | DB2 for i                                              |
| **Gerenciamento de arquivos** | VSAM, Datasets, GDG                                     | Arquivos PF (Physical File), LF (Logical File)        |
| **Transacional**          | CICS                                                    | Menos comum; uso de APIs, menus interativos e CLP     |
| **Ferramentas de monitoramento** | SDSF, RMF, OMEGAMON                                 | WRKACTJOB, WRKSPLF, STRSQL                            |
| **Mercado**               | Mais utilizado em bancos, grandes corporações globais    | Mais comum em indústrias, pequenas e médias empresas  |

---

## 🧠 Considerações Técnicas

### 📌 Sobre o COBOL em AS/400:
- **ILE COBOL** é modular e orientado à execução em *procedures*, aproveitando o modelo do ILE (Integrated Language Environment).
- Pode ser chamado a partir de **menus interativos**, **CLP**, **RPG**, **programas externos**.
- Permite integração com programas escritos em outras linguagens do ILE (RPG, C, CL).

### 📌 Sobre o DB2 no AS/400:
- Versão integrada ao sistema operacional IBM i.
- **Case-insensitive** por padrão.
- Tabelas e arquivos físicos (PF) são armazenados como objetos no sistema.
- SQL padrão ANSI é suportado (SELECT, INSERT, MERGE, etc).
- Pode ser acessado via comandos como `STRSQL`, `RUNSQLSTM` ou via embutido no COBOL (`EXEC SQL`).

---

## 🔄 Transição entre ambientes

| Item a estudar para quem vem do z/OS e vai ao AS/400 |
|-------------------------------------------------------|
| 📘 Comandos CLP (Control Language Programs) — similar ao JCL |
| 📁 Conceito de arquivos PF e LF — em vez de VSAM / GDG |
| 🖥️ Ambiente de execução: menus interativos, comandos WRK* |
| 📦 Criação de objetos: `CRTBNDCBL`, `CRTPGM`, `DLTPGM`, etc |
| 🧰 Utilização de comandos como `WRKJOB`, `DSPMSG`, `WRKACTJOB` |
| 🔄 Ferramentas para debug interativo, logs e mensagens do sistema |

---

## ✅ Conclusão

| Pontos-chave para lembrar |
|---------------------------|
| 🧠 Ambos usam COBOL e DB2, mas com variações técnicas importantes |
| 🏛️ z/OS é mais tradicional em bancos; AS/400 é mais comum em empresas de menor porte |
| 📚 O conhecimento em um ambiente ajuda na curva de aprendizado do outro |
| 💡 Há grande demanda por quem conhece os dois mundos, especialmente para **modernização de legados** |

---

## 📚 Fontes e Documentação Oficial

- 🔗 IBM Documentation – **IBM i 7.5 ILE COBOL Programmer's Guide**  
  https://www.ibm.com/docs/en/i/7.5?topic=languages-ile-cobol

- 🔗 IBM Documentation – **Enterprise COBOL for z/OS Documentation**  
  https://www.ibm.com/docs/en/cobol-zos/latest

- 🔗 IBM Documentation – **Db2 for i SQL Reference**  
  https://www.ibm.com/docs/en/i/7.5?topic=db2-sql-reference

- 🔗 IBM Documentation – **Db2 for z/OS Concepts**  
  https://www.ibm.com/docs/en/db2-for-zos/12?topic=overview-db2-zos-concepts

---

## 📚 Fontes e Documentação Oficial

- 🔗 [IBM i 7.5 – ILE COBOL Programmer's Guide (introdução e estrutura de programa)](https://www.ibm.com/docs/en/i/7.5?topic=guide-program-structure-in-ile-cobol)
  
- 🔗 [IBM i 7.5 – DB2 for i: Comandos SQL suportados no STRSQL](https://www.ibm.com/docs/en/i/7.5?topic=functions-sql-statements-supported-by-strsql)

- 🔗 [IBM i 7.5 – Conceito de arquivos físicos (PF) e lógicos (LF)](https://www.ibm.com/docs/en/i/7.5?topic=ssw_ibm_i_75/rzarl/rzarlpdf.htm)

- 🔗 [Enterprise COBOL for z/OS – Visão geral e comparação com versões anteriores](https://www.ibm.com/docs/en/cobol-zos/6.4?topic=overview)

- 🔗 [DB2 for z/OS – Introdução ao SQL embutido (Embedded SQL)](https://www.ibm.com/docs/en/db2-for-zos/12?topic=programs-using-embedded-sql)

- 🔗 [DB2 for z/OS – Tipos de tabelas, índices e partições](https://www.ibm.com/docs/en/db2-for-zos/12?topic=structures-types-tables-indexes)

- 🔗 [JCL – IBM z/OS MVS JCL Reference (Introdução e comandos básicos)](https://www.ibm.com/docs/en/zos/2.5.0?topic=overview-job-control-language)

- 🔗 [IBM i – Comandos CL (CLP): referência completa](https://www.ibm.com/docs/en/i/7.5?topic=reference-cl-command)

- 🔗 [IBM i – WRKACTJOB (Work with Active Jobs)](https://www.ibm.com/docs/en/i/7.5?topic=ssw_ibm_i_75/cl/wrkactjob.htm)

---

📎 **Próximos tópicos sugeridos para aprofundamento:**
- Diferenças práticas entre ILE COBOL e Enterprise COBOL
- Manipulação de arquivos PF/LF no COBOL do AS/400
- Exemplos de `EXEC SQL` comparando IBM i e z/OS
- Processo de compilação e deploy em cada ambiente
- Como migrar programas de um ambiente para outro

---
