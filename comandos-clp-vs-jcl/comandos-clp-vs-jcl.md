## 📁 Comandos CLP vs JCL – Comparativo prático para quem vem do z/OS

### 🎯 Objetivo
Apresentar um comparativo direto entre comandos CLP (Control Language Program) do IBM i e os JCLs (Job Control Language) do z/OS, com exemplos práticos e explicações para facilitar a transição.

---

### 🧠 Visão Geral

| Conceito                      | z/OS (JCL)                           | IBM i (CLP)                              |
|------------------------------|--------------------------------------|------------------------------------------|
| Submissão de job             | `SUBMIT JOB` (via SDSF ou batch)     | `SBMJOB`                                 |
| Execução de programa         | `PGM=xxx`                            | `CALL PGM(xxx)`                          |
| Passagem de parâmetros       | `PARM='abc'`                         | `CALL PGM(xxx) PARM('abc')`              |
| Impressão de mensagens       | `//SYSOUT=*`                         | `SNDPGMMSG MSG('texto')`                 |
| Variáveis                    | SET &VAR=VAL                         | `DCL VAR(&VAR) TYPE(*CHAR) LEN(n)` + `CHGVAR` |
| Encadeamento de comandos     | `EXEC` steps                         | comandos em sequência no CLP             |
| Testes de condição           | IF/THEN/ELSE                         | `IF COND(...) THEN(...)`                 |
| Esperar final de job         | N/A (gerenciado via JES)            | `DLYJOB` ou `MONMSG CPFxxxx`             |
| Atribuição de arquivos       | DD statements                        | `OVRDBF`, `DCLF`, `RCVF`                 |
| Redirecionamento de saída    | SYSOUT/OUTDD                         | `OVRPRTF`, `SNDNETSPLF`, `WRKSPLF`       |
| Fim do job                   | `//` EOF                             | `RETURN` ou `ENDPGM`                     |

---

### 🛠️ Exemplo Prático – z/OS (JCL)

```jcl
//MEUTESTE JOB (ACCT),'NOME',CLASS=A,MSGCLASS=X
//STEP01   EXEC PGM=PROGCOB
//STEPLIB  DD DSN=MEU.LOAD,DISP=SHR
//SYSOUT   DD SYSOUT=*
//SYSIN    DD *
DADOS ENTRADA
/*
```

---

### 🛠️ Exemplo Equivalente – IBM i (CLP)

```cl
PGM
    DCL VAR(&MSG) TYPE(*CHAR) LEN(40)
    CHGVAR VAR(&MSG) VALUE('DADOS ENTRADA')
    CALL PGM(PROGCOB) PARM(&MSG)
ENDPGM
```

📌 Para compilar e submeter:
```cl
CRTCLPGM PGM(MINHALIB/PROGCL) SRCFILE(MINHALIB/QCLSRC)
SBMJOB CMD(CALL PGM(MINHALIB/PROGCL))
```

---

### 📚 Referência Oficial IBM

- [SBMJOB Command – IBM Docs](https://www.ibm.com/docs/en/i/7.5?topic=ssw_ibm_i_75/cl/sbmjob.htm)
- [CL Programming Guide – IBM i](https://www.ibm.com/docs/en/i/7.5?topic=programs-control-language-cl)
- [z/OS JCL Reference](https://www.ibm.com/docs/en/zos/2.5.0?topic=jcl-zos-job-control-language)

---

### ⚠️ Observações Importantes

- No IBM i, os *jobs* são controlados por subsistemas (como QINTER, QBATCH), não por JES.
- Os *jobs* submetidos com `SBMJOB` rodam de forma assíncrona.
- É possível debugar jobs em batch com comandos como `STRSRVJOB` e `STRDBG`.

---

### ✅ Resumo da Adaptação

| Se você usava no z/OS... | No IBM i você usará...       |
|--------------------------|------------------------------|
| JCL (`//STEP EXEC`)      | CLP (`CALL`, `SBMJOB`)       |
| Dataset para programa    | Objeto (PGM) em biblioteca   |
| DD statements            | `OVRDBF`, `DCLF`, `RCVF`     |
| Variáveis JCL            | `DCL VAR`, `CHGVAR`          |
| SYSOUT                   | Spool via `WRKSPLF`          |

---

