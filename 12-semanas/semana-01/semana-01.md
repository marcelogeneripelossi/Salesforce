## Semana 1: Do Setup ao Primeiro Objeto Customizado

Esta semana é dedicada a entender o "onde" antes de aprender o "como". Mas, por que não criarmos o nosso 1º Objeto Customizado.

### Dia 1: Navegação e o Setup

* **Onde fica o Setup e o Object Manager:** Ambos ficam na interface principal do Salesforce (Web), acessíveis pela engrenagem no canto superior direito. O *Developer Console* é uma ferramenta de edição de código que vive *dentro* dessa interface.
* **Conceito de Objetos:** Entender que *Accounts* (Contas) e *Contacts* (Contatos) são apenas "tabelas" com comportamentos especiais que já existem.
* **Link:** [Trailhead: Salesforce Platform Basics](https://www.google.com/search?q=https://trailhead.salesforce.com/content/learn/modules/platform_dev_basics)

### Dia 2: O Poder da Customização

* **O que é customizável:** Tudo. Desde campos, validações, até a própria UI e lógica de backend.
* **O que é desenvolvido via código:** Regras de negócio complexas, integrações via API, automações que não cabem em fluxos declarativos (Flows).
* **Link:** [Trailhead: Customizing the Salesforce Platform](https://trailhead.salesforce.com/content/learn/modules/lex_customization)

### Dia 3: Developer Console

* **Interface:** Entender como abrir o *Developer Console* (pela engrenagem). Aprender a usar o *Query Editor* (SOQL) e o *Log Panel*.
* **Link:** [Documentação: Navegando no Developer Console](https://help.salesforce.com/s/articleView?id=platform.code_dev_console_navigating.htm&type=5)

### Dia 4: Prática de Interface

* Explore o *Object Manager*. Abra um objeto *Account*, veja a lista de campos, *Page Layouts* e *Validation Rules*. Tente adicionar um campo customizado (ex: `Numero_De_Funcionarios__c`) em um objeto.

### Dia 5: Criando nosso 1º Objeto Customizado

* Criando um Objeto Customizado do Salesforce no Developer Edition.
---

## Dicas para o Desenvolvedor .NET

1. **O "Setup" é seu melhor amigo:** Diferente do .NET, onde você usa Visual Studio/VS Code para tudo, muito do "arquitetônico" no Salesforce é feito via interface de administração.
2. **Developer Console vs. VS Code:** Para iniciantes, o *Developer Console* é útil, mas à medida que avançarmos, migraremos para o **Salesforce Extensions for VS Code**, que é o padrão profissional.
3. **Não subestime a UI:** Entender onde as coisas estão na interface ajuda a debugar o código depois, pois você saberá exatamente em qual "objeto" o dado está sendo armazenado.
---
## O Primeiro Conceito Técnico: Governor Limits

No .NET, você raramente se preocupa se uma consulta `SELECT` vai travar o servidor (a menos que seja um loop absurdo). No Salesforce, **você está em um ambiente multitenant.** Se o seu código consumir muitos recursos, ele é interrompido pelo sistema para não afetar os outros clientes.

* **Regra de Ouro:** Nunca, sob hipótese alguma, coloque uma consulta SOQL ou uma operação DML dentro de um loop `for`. Isso causará um erro de tempo de execução imediato (Too many SOQL queries: 101).

---

## Fontes Recomendadas
* [Trilha Trailhead: Conceitos básicos do Salesforce para desenvolvedores .NET](https://trailhead.salesforce.com/pt-BR/content/learn/trails/microsoft_dotnet)
* [Módulo Trailhead: Criar um objeto personalizado (Quick Look)](https://trailhead.salesforce.com/pt-BR/content/learn/modules/create-a-custom-object-quick-look/create-a-custom-object)
* [Projeto Trailhead: Personalizar um objeto do Salesforce](https://trailhead.salesforce.com/pt-BR/content/learn/projects/customize-a-salesforce-object)
