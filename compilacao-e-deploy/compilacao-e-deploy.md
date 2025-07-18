# 🛠️ Processo de Compilação e Deploy em Cada Ambiente

## 📑 Índice
- [1. Introdução](#1-introdução)
- [2. Compilação no ambiente IBM i (AS/400)](#2-compilação-no-ambiente-ibm-i-as400)
- [3. Deploy no IBM i (AS/400)](#3-deploy-no-ibm-i-as400)
- [4. Compilação no ambiente z/OS](#4-compilação-no-ambiente-zos)
- [5. Deploy no z/OS](#5-deploy-no-zos)
- [6. Comparativo entre os ambientes](#6-comparativo-entre-os-ambientes)
- [7. Fontes Oficiais](#7-fontes-oficiais)

---

## 1. Introdução

Este tópico descreve e compara o processo de **compilação e deploy de programas COBOL** nos ambientes **IBM i (AS/400)** e **z/OS**, destacando as diferenças técnicas, ferramentas utilizadas e melhores práticas em cada plataforma.

---

## 2. Compilação no ambiente IBM i (AS/400)

- Utiliza o comando `CRTBNDCBL` (Create Bound COBOL Program) ou `CRTSQLCBL` para programas com SQL embutido.
- Fontes ficam em **membros de arquivos-fonte físicos (QSYS.LIB/QxxxSRC.FILE/MBR)**.
- Compilação pode ser feita via **SEU (Source Entry Utility)**, via comandos CL ou via ferramentas como **RDi**.
- Possui suporte a **debug embutido**, atributos de compilação como `DBGVIEW(*ALL)` e `ACTGRP()`.

Exemplo:
```cl
CRTSQLCBL PGM(MYLIB/MEUPGM) SRCFILE(MYLIB/QCBLSRC) DBGVIEW(*ALL)
```

---

## 3. Deploy no IBM i (AS/400)

- O "deploy" normalmente significa mover o objeto compilado para uma biblioteca de produção.
- Pode ser feito via comandos CL como `CPYOBJ`, `SAVOBJ`/`RSTOBJ`, ou por scripts automatizados com CLP.
- Pode haver **controle de versões por bibliotecas** (ex: DEVLIB, TESTLIB, PRODLIB).

---

## 4. Compilação no ambiente z/OS

- Utiliza JCL com passos específicos (`IGYCRCTL` para compilação, `IEWL` para linkage).
- Fontes estão em **datasets particionados (PDS)**.
- Para programas com SQL, utiliza o **pré-compilador do DB2** (`DSNHPC`), seguido da compilação e linkage.

Exemplo simplificado de JCL:
```jcl
//STEP1 EXEC PGM=DSNHPC,PARM='HOST(IBMCOB)'
//SYSIN DD DSN=MY.PDS.SOURCE(PROG1),DISP=SHR
...
//STEP2 EXEC PGM=IGYCRCTL
//SYSLIN DD DSN=&&OBJECT,UNIT=SYSDA,DISP=(MOD,PASS)
//SYSPRINT DD SYSOUT=*
//SYSUT1 DD UNIT=SYSDA,SPACE=(CYL,(1,1))

//STEP3 EXEC PGM=IEWL
//SYSLMOD DD DSN=MY.LOADLIB(PROG1),DISP=SHR
```

---

## 5. Deploy no z/OS

- Deploy significa movimentar o módulo compilado para a **LOADLIB de produção**.
- Pode ser feito via JCL (`IEBGENER`, `IEBCOPY`), ferramentas como **Endevor**, **Changeman**, ou manualmente via FTP/SDSF.
- Ambientes bem controlados utilizam **Change Management** formal.

---

## 6. Comparativo entre os ambientes

| Item                     | IBM i (AS/400)                        | z/OS                                |
|--------------------------|----------------------------------------|-------------------------------------|
| Armazenamento de fontes  | Membros em arquivos-fonte físicos      | Membros em datasets PDS             |
| Compilação COBOL         | CRTBNDCBL / CRTSQLCBL                 | JCL com IGYCRCTL e DSNHPC           |
| Deploy                   | Copiar objetos entre bibliotecas       | Copiar LOAD para LOADLIB            |
| Pré-processador SQL      | CRTSQLCBL (automático)                 | DSNHPC (pré-compilador DB2)         |
| Ferramentas              | RDi, PDM, SEU                          | ISPF, SDSF, Endevor, Changeman      |

---

## 7. Fontes Oficiais

- 📄 [IBM i CRTSQLCBL Reference](https://www.ibm.com/docs/en/i/7.5?topic=ssw_ibm_i_75/cl/crtsqlcbl.htm)
- 📄 [IBM i COBOL Compilation Overview](https://www.ibm.com/docs/en/i/7.5?topic=cobol-compiling-programs)
- 📄 [z/OS Enterprise COBOL Compilation JCL Example](https://www.ibm.com/docs/en/cobol-zos/6.4?topic=programs-compiling)
- 📄 [DB2 Precompiler (DSNHPC) - IBM z/OS](https://www.ibm.com/docs/en/db2-for-zos/12?topic=statements-using-db2-precompiler)
- 📄 [Link-edit with IEWL - IBM z/OS](https://www.ibm.com/docs/en/zos/2.5.0?topic=execution-link-editing-iewl)

