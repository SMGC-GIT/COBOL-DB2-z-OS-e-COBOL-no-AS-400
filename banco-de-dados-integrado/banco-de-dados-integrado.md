## 🧠 Banco de Dados Integrado no IBM i (AS/400)

No IBM i, o **DB2 for i** é **totalmente integrado ao sistema operacional**, o que representa uma diferença conceitual e prática muito grande em relação ao DB2 no z/OS.

---

### 📌 O que significa "banco de dados integrado"?

- O DB2 for i **não é um produto separado** do sistema operacional. Ele é parte **nativa e inseparável** do IBM i.
- Isso significa que as funções de banco de dados fazem parte do **kernel do sistema**, com gerenciamento de memória, segurança, logs e backups totalmente integrados.
- Ao contrário do z/OS, **não é necessário iniciar o DB2** separadamente nem gerenciar instâncias de forma isolada.

---

### ⚙️ Estrutura de Objetos no IBM i

O IBM i **organiza tudo como objetos**, e isso vale também para os arquivos de dados. Ou seja:

| Tipo de Objeto | Finalidade                                              |
|----------------|----------------------------------------------------------|
| `*FILE`        | Arquivos físicos (PF) e lógicos (LF), equivalentes a tabelas e views |
| `*PGM`         | Programas compilados                                     |
| `*SRVPGM`      | Service Programs (módulos reutilizáveis)                 |
| `*LIB`         | Bibliotecas (organizam todos os objetos do sistema)     |

Esse modelo simplifica o controle de segurança, auditoria, deploy e versionamento — tudo usando comandos nativos do sistema (`WRKOBJ`, `DSPOBJD`, etc).

---

### 🧑‍💻 Precisa de DBA no IBM i?

#### Sim, **mas com perfil diferente** do DBA tradicional do z/OS.

| Aspecto                   | z/OS (DB2 for z/OS)                                | IBM i (DB2 for i)                                  |
|---------------------------|---------------------------------------------------|----------------------------------------------------|
| DBA é essencial?          | Sim, altamente especializado                      | Sim, mas pode ser mais "generalista"               |
| Administração separada?   | Sim. DB2 é um subsistema separado                 | Não. DB2 está dentro do SO                         |
| Start/Stop de instância?  | Sim                                               | Não (o DB já está sempre "ligado")                |
| Necessita tuning intenso? | Sim, com controle granular                        | Menor carga de tuning manual                      |
| Funções comuns do DBA     | Performance, segurança, catalog, utilities        | Também, mas muitas automatizadas ou integradas     |
| SQL Assistente?           | Sim (por exemplo, Data Studio)                   | Sim (Access Client Solutions, Navigator for i)     |

---

### 💡 Observação importante

No IBM i, **muitas tarefas de administração são feitas diretamente pelos desenvolvedores ou analistas de produção**, devido à simplicidade de comandos como `WRKDBF`, `DSPFD`, `RUNSQLSTM`, `STRSQL`, etc.

Entretanto, ambientes maiores ainda têm **DBAs especializados**, especialmente quando há:

- Alta carga de dados
- Ambientes com replicação (Journaling, Remote Journals)
- Processos críticos com muitos acessos concorrentes
- Necessidade de auditoria e segurança avançadas

---

### 🔗 Fontes para aprofundar

- [IBM Documentation - Introduction to DB2 for i](https://www.ibm.com/docs/en/i/7.5?topic=db2-introduction)
- [IBM Documentation - Object Types](https://www.ibm.com/docs/en/i/7.5?topic=overview-object-types)
- [IBM Support - DB2 for i vs DB2 for z/OS](https://www.ibm.com/support/pages/understanding-db2-i-vs-db2-zos)
