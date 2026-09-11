# Análise Arquitetural do Projeto: `e-sefaz-mobile`

O **e-SEFAZ Mobile** é o aplicativo móvel oficial da Secretaria da Fazenda do Estado do Rio Grande do Norte (SEFAZ/RN), voltado principalmente para a atuação dos **auditores fiscais** em campo e postos fiscais de fronteira.

---

## 1. Visão Geral da Arquitetura

O projeto é desenvolvido em **.NET MAUI (Multi-platform App UI)** com C# (.NET 8/9), visando compatibilidade com **Android** e **iOS**.

A solução passou por um processo de modernização arquitetural: foi migrada de um modelo legado com múltiplos projetos complexos e uso intensivo de MediatR/CQRS para uma **Clean Architecture (Arquitetura em Camadas Simplificada)** combinada com o padrão **MVVM (Model-View-ViewModel)**.

A solution principal (ESefaz.Mobile.sln) é composta por **3 projetos principais**:

ESefaz.Mobile/

├── Src/

│   ├── ESefaz.Mobile.Core             (Domínio, Contratos, DTOs e Lógica de Negócio)

│   ├── ESefaz.Mobile.Infrastructure   (Refit HTTP Clients, APIs, Storage, Serviços de Plataforma)

│   └── ESefaz.Mobile.Presentation     (UI, Páginas em C#, ViewModels MVVM, Inicialização MAUI)

### O Fluxo de Dependências:

Presentation ──► Infrastructure ──► Core

     │                               ▲

     └───────────────────────────────┘

1. **`ESefaz.Mobile.Core` (Camada Central / Domínio):**
    - **Independente de UI e de frameworks externos de persistência/rede**.
    - Contém as interfaces de serviços (`ILoginService`, `IConsultaContribuinteService`, etc.), modelos de domínio, DTOs, Requests/Responses, Enums, Commands e regras de validação.
2. **`ESefaz.Mobile.Infrastructure` (Camada de Integração e Infraestrutura):**
    - Implementa as interfaces definidas no Core.
    - Comunicação com os Web Services da SEFAZ via **Refit** (REST tipado) e HttpClient com pipelines de resiliência e autorização (`DelegatingHandlers`).
    - Persistência de dados locais e sessão do usuário (`Preferences`, `UserSessionStorage`).
    - Serviços dependentes de plataforma (identificador único de hardware no Android/iOS, biometria/FaceID).
3. **`ESefaz.Mobile.Presentation` (Camada de Apresentação):**
    - Ponto de entrada do aplicativo MAUI configurado no MauiProgram.cs.
    - Utiliza **C# Code-Behind / C# UI Markup** para construir boa parte das telas (`Pages/*.cs`), reduzindo o uso de XAML para arquivos estruturais como `App.xaml` e `AppShell.xaml`.
    - Implementa **MVVM** com suporte ao `CommunityToolkit.Mvvm` (usando `ObservableObject`, `[ObservableProperty]` e `[RelayCommand]`).

---

## 2. Lista Completa dos Módulos do Aplicativo

Com base no mapeamento de telas, rotas e serviços do aplicativo, o sistema é dividido nos seguintes módulos funcionais:

|#|Módulo|Descrição Funcional|
|---|---|---|
|**1**|**Acesso, Autenticação e Sessão**|Login tradicional (CPF/senha), SSO, Biometria/FaceID, registro do dispositivo móvel, refresh token, recuperação de senha e controle de sessão expirada.|
|**2**|**Home, Navegação e Perfil**|`AppShell`, tela inicial com atalhos dinâmicos, favoritos, menu funcional categorizado e fluxo de vínculo/desvínculo de empresa.|
|**3**|**Consulta de Contribuinte**|Busca de dados cadastrais de pessoas físicas e jurídicas por CPF, CNPJ ou Inscrição Estadual, com validação e detalhamento completo.|
|**4**|**Documentos Fiscais Eletrônicos (DF-e)**|Consulta de NF-e e NFC-e por chave de acesso, leitor de QR Code, scanner de código de barras pela câmera e visualizador do DANFE.|
|**5**|**MDF-e (Manifesto Eletrônico)**|Consulta de MDF-e por chave ou filtros, listagem por status (Autorizado, Cancelado, Encerrado) e tela de detalhes do manifesto.|
|**6**|**Consulta por Placa de Veículo**|Fiscalização de veículos em trânsito: carrega automaticamente as NF-es e MDF-es atrelados à placa e termos de apreensão associados.|
|**7**|**Fiscalização - TRM (Termo de Apreensão)**|Consulta e listagem de TRMs (Termos de Apreensão de Mercadoria), detalhamento do termo e visualização/download de PDF.|
|**8**|**Procedimentos TRM**|Ações operacionais sobre apreensões: registro de ciência, registro de recusa, nomeação de fiel depositário, cancelamento de atividade e liberação por liminar.|
|**9**|**Lavratura de TAM (Wizard)**|Fluxo guiado em etapas (Identificação, Momento, Ocorrências, Débitos Agrupados, Cálculo de Tributos, Rascunhos) para autuação fiscal.|
|**10**|**Arrecadação Vinculada**|Emissão de GRI (Guia de Recolhimento) e boletos vinculados a débitos e termos de apreensão.|
|**11**|**Liberação de Mercadorias (Fronteira)**|Consulta de mercadoria retida por chave NFe, conferência em posto fiscal, inclusão de justificativa e alteração de status de liberação.|
|**12**|**Parte de Serviço (PS)**|Abertura, registro e acompanhamento de Parte de Serviço dos auditores fiscais, com download de documentos anexos.|
|**13**|**SMART e Lotes**|Inclusão de lotes de notas fiscais via SMART e análise em lote para agilizar a fiscalização.|
|**14**|**Argos Chatbot**|Assistente virtual de inteligência/suporte integrado diretamente no app para apoio ao auditor.|
|**15**|**Infraestrutura Transversal (Cross-Cutting)**|Tratamento global de erros (`IGlobalExceptionHandler`), popups de loading (`ApiLoadingService`), notificações locais/push e feedback háptico.|

---

## 3. Módulo Indicado para Estudos: Módulo de Autenticação (`Auth`)

### Por que começar pelo módulo de Autenticação?

1. **É a porta de entrada da aplicação:** nada funciona sem entender como a sessão, o token e o dispositivo são registrados.
2. **É a referência de arquitetura do projeto:** este módulo já foi refatorado e serve como o modelo que a equipe está usando para modernizar os demais módulos.
3. **Fluxo ponta a ponta perfeito:** você consegue ver uma requisição saindo da UI, passando pela regra de negócio, consumindo o endpoint REST via Refit, salvando em cache seguro e navegando para a Home.

---

### Guia de Acesso aos Arquivos do Módulo `Auth`

Recomendamos estudar os arquivos na seguinte ordem de baixo para cima (da camada de dados/contratos até a tela):

```
1. Core (Contratos e DTOs) ──► 2. Infrastructure (Refit & Storage) ──► 3. Presentation (ViewModel & Page)
```

---

#### Passo 1: O Núcleo do Módulo (`ESefaz.Mobile.Core`)

1. **ILoginService.cs**
    - **O que é:** O contrato puro que define a operação de login (`SignInAsync`).
    - **O que observar:** Como o Core não conhece nem Refit, nem HTTP, nem MAUI; apenas inputs e outputs em C#.
2. **IAuthenticationService.cs**
    - **O que é:** Interface moderna que orquestra o ciclo completo de autenticação (login, logout, biometria e checagem de sessão).
3. **LoginCommand.cs**
    - **O que é:** DTO que encapsula as credenciais informadas pelo usuário (`Login` e `Password`).
4. **LoginRequest.cs** e **LoginResponse.cs**
    - **O que são:** Os modelos JSON enviados e recebidos da API REST do backend.

---

#### Passo 2: A Integração Externa (`ESefaz.Mobile.Infrastructure`)

1. **IAuthApiClient.cs**
    - **O que é:** Interface declarativa do **Refit**.
    - **O que observar:** A anotação `[Post("/api/Auth")]`. O Refit gera automaticamente em tempo de execução o código HttpClient que faz a chamada HTTP.
2. **LoginService.cs**
    - **O que é:** Implementação da interface `ILoginService`.
    - **O que observar:** O uso do `IMapper` para converter `LoginCommand` em `LoginRequest`, chamar o `IAuthApiClient` e retornar o `LoginDto`.
3. **AuthenticationService.cs**
    - **O que é:** Serviço de alto nível que orquestra a autenticação, registro do token e controle de biometria.
4. **UserSessionStorage.cs**
    - **O que é:** Gerenciador de persistência local da sessão.
    - **O que observar:** Salva dados da sessão do auditor, tokens e último usuário usando o `Microsoft.Maui.Storage.Preferences`.
5. **SetupClientApi.cs** e **ServiceCollectionExtensions.cs**
    - **O que são:** Os métodos de extensão de Injeção de Dependência (`AddInfrastructureServices` e `AddAuthenticationServices`) onde todos esses serviços são registrados no container do .NET.

---

#### Passo 3: A Interface e Interação (`ESefaz.Mobile.Presentation`)

1. **LoginViewModelRefactored.cs** _(Recomendado para entender o padrão ideal)_
    - **O que é:** O ViewModel simplificado e limpo.
    - **O que observar:** Veja como ele utiliza `[ObservableProperty]` do CommunityToolkit.Mvvm para `Login`, `Password`, `IsBusy`, e métodos assíncronos que chamam o `IAuthenticationService`.
2. **LoginViewModel.cs** _(Versão completa de produção)_
    - **O que é:** O ViewModel atualmente em produção, contendo tratamentos adicionais de SSO, usuário Apple Review para homologação na App Store, popups de erro e recuperação de senha.
3. **LoginPage.cs**
    - **O que é:** A tela de Login construída em C#.
    - **O que observar:** Veja como os campos `txtCodigoUsuario` e `txtSenha` fazem _Data Binding_ direto nas propriedades do ViewModel (`txtCodigoUsuario.SetBinding(Entry.TextProperty, nameof(LoginViewModel.Login))`).
4. **MauiProgram.cs**
    - **O que é:** O `Main` da aplicação MAUI onde o ciclo de vida e todas as dependências são amarradas.