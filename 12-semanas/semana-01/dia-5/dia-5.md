# Dia 5

---

## Criando um Objeto Customizado do Salesforce no Developer Edition

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

## Fontes Recomendadas
* [Módulo Trailhead: Criar um objeto personalizado (Quick Look)](https://trailhead.salesforce.com/pt-BR/content/learn/modules/create-a-custom-object-quick-look/create-a-custom-object)
* [Projeto Trailhead: Personalizar um objeto do Salesforce](https://trailhead.salesforce.com/pt-BR/content/learn/projects/customize-a-salesforce-object)
