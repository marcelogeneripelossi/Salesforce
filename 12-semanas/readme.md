# Plano de Estudos: Transição .NET para Salesforce (Developer PD1)

Este é um roteiro estruturado de 12 semanas (dedicação de 2 horas/dia) para desenvolvedores .NET/C# que desejam migrar para o ecossistema Salesforce e obter a certificação **Platform Developer I (PD1)**.

## Estratégia de Treinamento (12 Semanas)

| Semanas | Foco Principal | Objetivo de Aprendizado |
| :--- | :--- | :--- |
| **1** | **Ambientação e UI** | Setup, Object Manager, Navegação e conceitos de Plataforma. |
| **2-3** | **Data Modeling & Schema** | Objetos, campos, tipos, e o crucial: a lógica de **Relacionamentos (Master-Detail vs Lookup)**. |
| **4-6** | **Lógica de Servidor (Apex)** | Sintaxe, DML, SOQL, e o domínio dos **Governor Limits**. |
| **7-8** | **Automação & Trigger Framework** | Triggers, o ciclo de vida de uma transação e padrões de projeto (Frameworks). |
| **9-10** | **Integração e Segurança** | OWD, Perfis, Permissões, API, e segurança em nível de campo. |
| **11-12** | **UI (LWC), Testes e Certificação** | Lightning Web Components (LWC) básico, Apex Tests e Revisão final. |

---

## Detalhamento do Plano

### Semana 1: Ambientação e UI
* **Setup:** O coração da administração do Salesforce.
* **Object Explorer:** Serve especificamente para gerenciar a estrutura de dados do Salesforce.
* **Objetos:** "tabelas" com comportamentos especiais.

### Semanas 2-3: Data Modeling & Schema
* **Conceitos:** Standard Objects vs. Custom Objects, tipos de campos, Schema Builder.
* **Foco PD1:** Diferença entre Lookup e Master-Detail (comportamento de segurança e deleção em cascata).
* **Ação:** Praticar a criação de objetos no seu *Developer Edition*.

### Semanas 4-6: Lógica de Servidor (Apex)
* **Conceitos:** Apex como linguagem orientada a objetos (similar a C#), DML, SOQL.
* **Foco PD1:** **Governor Limits**. Aprender por que nunca usar consultas/DML dentro de loops. Entender a importância da *Bulkification*.

### Semanas 7-8: Automação & Trigger Framework
* **Conceitos:** Ciclo de vida de uma Trigger, "Before" vs. "After" events.
* **Foco PD1:** Implementação de boas práticas. Entender que Trigger deve apenas delegar para classes de serviço (Trigger Handler Pattern).

### Semanas 9-10: Integração e Segurança
* **Conceitos:** Segurança declarativa (OWD, Profiles, Permission Sets).
* **Foco PD1:** Como o Salesforce garante que um usuário não acesse dados que não deveria (Sharing Rules, Role Hierarchy).

### Semanas 11-12: UI (LWC), Testes e Certificação
* **Conceitos:** Introdução ao LWC (o framework de UI moderno), Testes unitários (obrigatórios para deploy).
* **Foco PD1:** Cobertura de código (mínimo 75%), `Test.startTest()` e `Test.stopTest()`, Assertions.

---

## Dicas para o Desenvolvedor .NET
1.  **Esqueça o Entity Framework:** O Salesforce gerencia o banco de dados via metadados. Não há *Migrations* via código.
2.  **Bulkificação é Vida:** Em C#, `foreach(var i in list) { db.Save(i); }` pode ser aceitável. Em Apex, isso causará falha por *Governor Limits*. Sempre trabalhe com coleções.
3.  **Trailhead é sua principal fonte:** Siga as trilhas oficiais para consolidar o conhecimento teórico com prática no ambiente.

---
## O Primeiro Conceito Técnico: Governor Limits

No .NET, você raramente se preocupa se uma consulta `SELECT` vai travar o servidor (a menos que seja um loop absurdo). No Salesforce, **você está em um ambiente multitenant.** Se o seu código consumir muitos recursos, ele é interrompido pelo sistema para não afetar os outros clientes.

* **Regra de Ouro:** Nunca, sob hipótese alguma, coloque uma consulta SOQL ou uma operação DML dentro de um loop `for`. Isso causará um erro de tempo de execução imediato (Too many SOQL queries: 101).

