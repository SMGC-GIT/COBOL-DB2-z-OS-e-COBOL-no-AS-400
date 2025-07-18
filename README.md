# COBOL + DB2 (z/OS | AS/400)

🗂️ **Manual Básico das diferenças e similaridades COBOL + DB2 (z/OS | AS/400)**

Esclarecer o papel do desenvolvedor COBOL em ambiente AS/400 (IBM i), suas diferenças e similaridades com o COBOL e DB2 no z/OS (Mainframe). Isso é especialmente útil para quem vem de um mundo z/OS e quer entender o universo AS/400 — ou vice-versa.

---

## 📚 Índice de Tópicos

| Módulo | Descrição |
|--------|-----------|
| [📁 Entendendo Diferenças e Similaridades](diferencas-similaridades/diferencas-similaridades.md) | Entender diferenças e similaridades COBOL + DB2 (z/OS | AS/400) |
| [📁 ILE COBOL e Enterprise COBOL](ile-cobol-enterprise-cobol/ile-cobol-enterprise-cobol.md) | Diferenças práticas entre ILE COBOL e Enterprise COBOL |
| [📁 Manipulação de Arquivos PF/LF no COBOL do AS/400](pf-lf-no-cobol-do-as400/pf-lf-no-cobol-do-as400.md) | Manipulação de Arquivos PF/LF no COBOL do AS/400 |
| [📁 Exemplos de EXEC SQL comparando IBM i e z/OS](exec-sql-ibmi-e-zos/exec-sql-ibmi-e-zos.md) | Exemplos de EXEC SQL comparando IBM i e z/OS |
| [📁 Processo de compilação e deploy em cada ambiente](compilacao-e-deploy/compilacao-e-deploy.md) | Processo de compilação e deploy em cada ambiente |
| [📁 Como migrar programas de um ambiente para outro](como-migrar-programas/como-migrar-programas.md) | Como migrar programas de um ambiente para outro |
| [📁 Comandos CLP vs JCL](comandos-clp-vs-jcl/comandos-clp-vs-jcl.md) | Comandos CLP vs JCL |
| [📁 Banco de Dados Integrado no IBM i (AS/400)](banco-de-dados-integrado/banco-de-dados-integrado/.md) | Banco de Dados Integrado no IBM i (AS/400)|
| [📁 Papel do DBA no z/OS x IBM i](papel-do-dba/papel-do-dba.md) | Papel do DBA no z/OS x IBM i: Similaridades, diferenças e quando cada perfil é necessário |

 
---

## 🔍 Objetivo

> Este manual foi criado para ser um **repositório vivo de conhecimento**, organizado por temas, de modo que possa ser consultado, atualizado e ampliado com o tempo por profissionais que atuam com COBOL | DB2 ( z/OS e AS/400 ).

---

## 📌 Licença

Este projeto é de uso pessoal/profissional aberto. Utilize, adapte e compartilhe com responsabilidade.

---

## 📌 Créditos e Contato

> Criado por **SILVIA GUIMARÃES** como parte de portfólio de projetos.

Para dúvidas ou sugestões, entre em contato comigo:
- **E-mail:** (sguimaraes1004@gmail.com)
- **Redes Sociais: [LinkedIn](https://www.linkedin.com/in/silvia-maria-guimar%C3%A3es-costa-3a01b423b)**
  
---



🔧 Módulos Sugeridos para Complemento
Módulo	Descrição
📁 Tratamento de Erros e Mensagens	Como tratar mensagens e códigos de erro no COBOL em ambos os ambientes. Inclui MONMSG (AS/400) e ABEND/RETURN-CODE (z/OS), além de SQLCODE/SQLSTATE.
📁 Uso de Subprogramas e Chamadas Externas	Diferenças entre CALL 'externa' e CALL integrada (ILE), uso de service programs (IBM i), DLLs e opções de bind no z/OS.
📁 Interação com Batch e Online (CICS/BSC)	Como o COBOL atua em ambientes batch e online em cada plataforma. Destaque para uso de CICS no z/OS vs. menus e display files no IBM i.
📁 Debugging e Ferramentas de Análise	Ferramentas disponíveis para debug no IBM i (STRDBG, debug view) e z/OS (Expeditor, Intertest, SDSF, SYSOUT), e melhores práticas.
📁 Acesso a Arquivos Externos (VSAM vs. PF/LF)	Comparação entre uso de VSAM (KSDS, ESDS) no z/OS e Physical/Logical Files no IBM i, com exemplos de SELECT/READ/WRITE/REWRITE.
📁 Conceitos de Journaling, Locks e Controle de Concorrência	Como garantir consistência de dados nos dois ambientes: journaling no IBM i e LOCK/ISOLATION LEVEL no DB2/z.
📁 Segurança e Controle de Acesso (RACF vs. OS/400 Security)	Como perfis, authorities e roles funcionam em cada ambiente e como isso impacta o desenvolvimento e o acesso a objetos.
📁 Comparativo de Utilitários e Comandos do Sistema	Ex: STRSQL vs. SPUFI/DSNTEP2, WRKOBJ vs. ISPF, WRKACTJOB vs. SDSF, WRKSRCPF vs. Edit Dataset. Tabela comparativa seria muito útil.
📁 Modernização e Integração com Web Services/REST	Como integrar programas COBOL com APIs ou serviços modernos (XML, JSON, HTTP calls), usando opções nativas ou wrappers.
📁 Gerenciamento de Versões e DevOps para COBOL	Ferramentas como RDi, Git com IBM i, Endevor, ChangeMan, Jenkins com z/OS, e práticas ágeis adaptadas ao mundo legado.

✨ Extras
✅ Anexar Apêndice com Glossário Técnico: siglas comuns (RPG, DSPFFD, DCLGEN, STRSRVJOB, BIND PLAN, etc.).

✅ Checklist de Portabilidade entre Ambientes

✅ FAQ com dúvidas frequentes de quem vem de um dos mundos (IBM i ou z/OS)

---

🧭 Continuação Sugerida do Manual – Foco na Transição z/OS ➡️ IBM i
Módulo 📁	Descrição
📁 Comandos CLP vs JCL	Comparar comandos CLP do IBM i com JCL do z/OS (inclusive com equivalentes práticos)
📁 Navegação e Utilitários	Navegação no IBM i: menus, comandos, SEU, PDM, VS código fonte no z/OS (ISPF)
📁 Compiladores, Bind e Liberações	Diferença no uso de compiladores, Bind e controle de versão entre os ambientes
📁 Conceito de Bibliotecas (LIB) no IBM i	Equivalente de Bibliotecas (LIB, QSYS, QGPL) com visão para quem vem de datasets no z/OS
📁 Debug e Rastreamento	Como depurar programas COBOL/SQL no IBM i: STRDBG, versus ferramentas de debug no z/OS
📁 Segurança e Acesso a Objetos	Segurança no IBM i (perfis, autorizações) comparando com RACF no z/OS
📁 DB2 for i: Particularidades	Quais recursos do DB2 for i diferem do DB2 z/OS – journaling, triggers, etc
📁 Criação e Manutenção de Tabelas	Como criar e manter tabelas e índices no IBM i – via DDS, SQL, Navigator
📁 Agendamento e Batch	Comparar o uso de JOBS/Job Schedule Entries no IBM i com JES no z/OS
📁 Mensagens e Logs	DSPMSG, WRKMSGQ e logs do sistema versus SDSF no z/OS
📁 Migração assistida de código	Boas práticas e ferramentas para migração de código COBOL + DB2 z/OS para IBM i


