# Desenvolvimento Salesforce: Do Setup ao Primeiro Objeto Customizado

Este guia prático foi criado para quem está iniciando a jornada de desenvolvimento no ecossistema Salesforce. Aqui você aprenderá a configurar seu ambiente de testes, entenderá a arquitetura de dados básica e criará seu primeiro objeto personalizado.

---

## 1. Iniciando no Salesforce: Primeiros passos com o Developer Edition

Para começar a desenvolver no Salesforce sem custos, você precisa de uma organização de testes chamada **Developer Edition (DE)**. Ela é um ambiente completo, gratuito e que não expira.

### Passo 1: Criar sua conta Trailhead (Opcional, mas recomendado)
O Trailhead é a plataforma de aprendizado oficial do Salesforce.
1. Acesse o [Trailhead](https://trailhead.salesforce.com/).
2. Clique em **Sign Up** (Inscrever-se).
3. Escolha uma forma de login (Google, LinkedIn ou Email) e preencha seu perfil.

### Passo 2: Inscrever-se em uma Organização Developer Edition (DE)
1. Acesse o site oficial de inscrição: [://salesforce.com](https://://salesforce.com).
2. Preencha o formulário com seus dados:
   - **Email:** Use um endereço real (você precisará dele para ativar a conta).
   - **Role:** Selecione *Developer*.
   - **Username:** Deve ser em formato de email (ex: `seu_nome@dev2026.com`), mas não precisa ser um email real. Ele deve ser exclusivo em todo o ecossistema Salesforce.
3. Clique em **Sign me up**.
4. Abra o seu email, procure a mensagem de confirmação do Salesforce e clique em **Verify Account**.
5. Redefina sua senha e configure sua pergunta de segurança.

### Passo 3: Acessar a Org e Conhecer o Menu Setup
Sempre que quiser trabalhar no seu código ou configuração:
1. Acesse [login.salesforce.com](https://login.salesforce.com/).
2. Insira o seu *Username* e senha criados no Passo 2.
3. Você cairá na página inicial. No canto superior direito, clique no ícone de **Engrenagem** e selecione **Setup** (Configuração). O Setup é o painel de controle do administrador e desenvolvedor.

### Passo 4: Abrir o Developer Console
O Developer Console é a IDE interna do Salesforce usada para escrever código Apex, executar consultas SOQL e debugar.
1. Certifique-se de que está na página de **Setup**.
2. Clique novamente no ícone de **Engrenagem** no canto superior direito.
3. Clique em **Developer Console**. Uma nova janela pop-up será aberta com o seu ambiente de desenvolvimento.

### Fontes Recomendadas
* [Projeto Trailhead: Prepare-se para desenvolver no Salesforce](https://trailhead.salesforce.com/pt-BR/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop?trail_id=force_com_dev_beginner)
* [Trilha Trailhead: Comece a desenvolver com o Salesforce](https://trailhead.salesforce.com/pt-BR/content/learn/projects/get-started-with-salesforce-development?trail_id=build-your-salesforce-developer-career)

---

## 2. Standard Objects x Custom Objects

No Salesforce, tabelas de banco de dados são chamadas de **Objetos**. Eles contêm campos (colunas) e registros (linhas). Entender a diferença entre os tipos de objetos é fundamental para a modelagem de dados.

Para quem vem do .NET, a melhor forma de entender **Objects** no Salesforce é enxergá-los como a camada de persistência (o equivalente às suas *Entities* ou *Domain Models* no Entity Framework), mas com a peculiaridade de que a infraestrutura, o banco de dados e a camada de segurança já vêm "embutidos" no objeto.

### Standard Objects (Objetos Padrão)
São os objetos que já vêm pré-construídos e inclusos na plataforma Salesforce por padrão. Eles cobrem os processos de negócios mais comuns (Vendas e Atendimento).
* **Exemplos clássicos:** `Account` (Contas/Empresas), `Contact` (Contatos/Pessoas), `Lead` (Potenciais Clientes) e `Opportunity` (Oportunidades de Vendas).
* **Nome de API:** O nome do objeto no banco de dados coincide exatamente com o seu nome padrão (ex: `Account`).
* **Limitação:** Você pode customizá-los (adicionar campos, mudar layouts), mas não pode deletá-los.

> **Ponto de Atenção para Devs C#:** No .NET, você define seu `DbContext`. No Salesforce, a "tabela" já existe no banco de dados assim que você cria o objeto via interface. O seu trabalho como desenvolvedor é manipular esses objetos via Apex ou configurar automações declarativas (Flows).

---

#### A Comparação Técnica

| Característica | .NET (EF / SQL Server) | Salesforce |
| --- | --- | --- |
| **Identificador** | `Id` (Guid/Int) | `Id` (18 caracteres - String) |
| **Schema** | `Migrations` / `Fluent API` | Configurado via Metadados (UI) |
| **Nomeação** | `PascalCase` | `Nome_Do_Objeto__c` |
| **Campos do Sistema** | Você cria manualmente (`CreatedAt`) | Já incluídos (`CreatedDate`, `LastModifiedDate`, etc.) |

---

#### Exemplo Prático: Acessando Objetos em Apex

Em C#, você faria um `context.Accounts.Where(...)`. No Salesforce, o acesso é direto através da linguagem **SOQL** integrada ao Apex:

```apex
// Exemplo de busca de um Account (Standard) e um objeto customizado
// Note o sufixo __c nos campos e objetos customizados

public void processarDados() {
    // SOQL é como um SELECT nativo no código
    List<Account> contas = [SELECT Id, Name FROM Account WHERE Industry = 'Technology' LIMIT 10];
    
    // Custom Object
    List<Veiculo__c> carros = [SELECT Id, Placa__c, Modelo__c FROM Veiculo__c WHERE Ativo__c = true];
    
    for(Veiculo__c v : carros) {
        System.debug('Modelo encontrado: ' + v.Modelo__c);
    }
}

```

### Custom Objects (Objetos Customizados)
São os objetos que você cria do zero para atender a necessidades específicas e exclusivas do seu modelo de negócio que não são cobertas pelos objetos padrão.
* **Exemplos hipotéticos:** `Imovel__c` (para uma imobiliária), `Pet__c` (para um petshop), `Agendamento__c` (para uma clínica).
* **Nome de API:** O Salesforce adiciona automaticamente o sufixo **`__c`** (custom) ao final do nome do objeto e de seus campos no banco de dados (ex: `Imovel__c`).
* **Flexibilidade:** Você tem controle total. Pode criá-los, alterá-los e deletá-los quando necessário.

---

## 3. Criando um Objeto Customizado do Salesforce no Developer Edition

Siga este passo a passo para criar o seu primeiro contêiner de dados personalizado no ecossistema.

### Passo 1: Navegar até o Gerenciador de Objetos
1. No menu principal do **Setup**, olhe para a barra de navegação superior.
2. Clique na aba **Object Manager** (Gerenciador de Objetos) ao lado de *Home*.

### Passo 2: Iniciar a Criação do Objeto
1. No canto superior direito da tela do Gerenciador de Objetos, clique no botão **Create** (Criar).
2. No menu suspenso, selecione **Custom Object** (Objeto personalizado).

### Passo 3: Preencher as Definições Básicas
Insira as seguintes informações essenciais:
* **Label (Rótulo):** O nome de exibição no singular. Digite `Carro`.
* **Plural Label (Rótulo no Plural):** Como aparecerá nas abas e menus. Digite `Carros`.
* **Object Name (Nome do Objeto):** Preenchido automaticamente como `Carro` (Este será o nome usado por desenvolvedores).
* **Record Name (Nome do Registro):** O campo identificador principal do registro. Mantenha como `Carro Name` e tipo **Text** (ou altere para *Auto-Number* se quiser códigos sequenciais como `CAR-{0000}`).

### Passo 4: Configurar Recursos Opcionais e Status
1. Role a página até **Optional Features** (Recursos opcionais) e marque as caixas:
   * **Allow Reports** (Permitir relatórios) - *Para conseguir extrair métricas depois.*
   * **Allow Activities** (Permitir atividades) - *Para vincular tarefas e eventos ao carro.*
2. Em **Deployment Status** (Status de implantação), certifique-se de que a opção **Deployed** (Implantado) está selecionada. Se ficar em *In Development*, apenas administradores verão o objeto.

### Passo 5: Ativar o Assistente de Guia (Muito Importante)
1. No final da página de configuração, marque a caixa **Launch New Custom Tab Wizard after saving this custom object** (Iniciar o assistente de nova guia personalizada após salvar este objeto personalizado).
2. Clique em **Save** (Salvar).

### Passo 6: Configurar a Guia Visual (Tab)
Como você marcou a caixa anterior, a tela de criação de Guia abrirá automaticamente:
1. **Object:** Já estará selecionado como `Carro`.
2. **Tab Style (Estilo da guia):** Clique no ícone de lupa e escolha qualquer cor ou ícone (ex: *Car* ou *Block*). Isso define a identidade visual do objeto.
3. Clique em **Next** (Avançar).
4. **Visibility:** Mantenha o padrão (*Default On* para todos os perfis) e clique em **Next**.
5. **Custom Apps:** Mantenha marcado para incluir em todos os aplicativos e clique em **Save** (Salvar).

**Pronto!** Seu objeto customizado `Carro__c` foi criado com sucesso e já possui uma aba visível no menu do sistema para você criar e gerenciar registros.

### Fontes Recomendadas
* [Trilha Trailhead: Conceitos básicos do Salesforce para desenvolvedores .NET](https://trailhead.salesforce.com/pt-BR/content/learn/trails/microsoft_dotnet)
* [Módulo Trailhead: Criar um objeto personalizado (Quick Look)](https://trailhead.salesforce.com/pt-BR/content/learn/modules/create-a-custom-object-quick-look/create-a-custom-object)
* [Projeto Trailhead: Personalizar um objeto do Salesforce](https://trailhead.salesforce.com/pt-BR/content/learn/projects/customize-a-salesforce-object)

