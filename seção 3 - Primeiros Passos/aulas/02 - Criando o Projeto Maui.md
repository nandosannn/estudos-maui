# .NET MAUI: Criação do Primeiro Projeto e Estrutura Arquitetural

A aula apresenta a criação do primeiro projeto .NET MAUI no Visual Studio e, principalmente, explica a estrutura de um projeto MAUI, suas diferenças em relação ao Xamarin e como o aplicativo consegue trabalhar com várias plataformas a partir de um único projeto.

## 1. Objetivo da Aula

O professor começa criando o projeto que será utilizado durante o curso. O aplicativo será um projeto simples chamado **App Número da Sorte**.

A ideia é posteriormente transformar esse projeto em um aplicativo capaz de gerar números da sorte, mas nesta aula o foco principal é:

- Criar o projeto;
    
- Configurar a solução;
    
- Entender a estrutura do .NET MAUI;
    
- Conhecer as pastas;
    
- Entender como o MAUI trabalha com Android, iOS, Mac Catalyst e Windows;
    
- Executar o projeto inicial.
    

## 2. Criando um Novo Projeto

**Passo 1 — Criar o projeto**

No Visual Studio, o professor seleciona a opção para criar um novo projeto e aguarda o carregamento dos templates disponíveis.

> [!INFO] **O que são templates?**
> 
> Um template é um modelo pronto de projeto que já fornece uma estrutura inicial com:
> 
> - Arquivos;
>     
> - Pastas;
>     
> - Configurações;
>     
> - Dependências;
>     
> - Código inicial.
>     
> 
> Isso evita a criação de toda a estrutura manualmente.

## 3. Procurando o Template .NET MAUI

Na tela de criação de projeto, pesquisa-se por: `MAUI`. Três opções principais são apresentadas:

|**Template**|**Finalidade**|
|---|---|
|**Aplicativo .NET MAUI**|Criar um aplicativo MAUI|
|**Aplicativo .NET MAUI Blazor**|Criar aplicativo MAUI utilizando Blazor|
|**Biblioteca de Classes .NET MAUI**|Criar uma biblioteca reutilizável|

Para o curso, a escolha é: **Aplicativo .NET MAUI**.

> [!WARNING] **Atenção**
> 
> O objetivo aqui é criar uma aplicação gráfica multiplataforma. Por isso, o template escolhido não é uma biblioteca e nem o template baseado em Blazor.

## 4. Definindo a Localização do Projeto

Depois de selecionar o template, define-se a pasta onde os projetos serão armazenados para manter uma estrutura organizada:

Plaintext

```
Projetos MAUI/
│
├── App Número da Sorte/
│
├── EP01/
│
├── EP02/
│
└── ...
```

## 5. Nome do Projeto

O nome definido para o primeiro projeto é: **App Número da Sorte**.

## 6. Projeto × Solução

- **Projeto:** É a aplicação ou biblioteca que será construída (`App Número da Sorte`).
    
- **Solução:** É um agrupador que pode conter vários projetos.
    

Plaintext

```
Projetos MAUI
│
├── App Número da Sorte
├── Projeto 02
├── Projeto 03
└── Projeto 04
```

## 7. Organização das Pastas do Curso

O professor cria a pasta **EP01** para isolar o primeiro aplicativo da solução:

Plaintext

```
Projetos MAUI
│
├── EP01
│   └── App Número da Sorte
│
├── EP02
│   └── Outro projeto
│
├── EP03
│   └── Outro projeto
│
└── ...
```

## 8. Escolhendo a Versão do .NET

Na aula, o professor escolhe o **.NET 6 (LTS)**.

> [!NOTE] **O que significa LTS?**
> 
> **LTS** significa _Long Term Support_ (versão que recebe suporte por um período estendido).
> 
> ⚠️ **Importante para estudos atuais:** Esta gravação utilizou .NET 6 com menção ao .NET 7. O conceito de LTS permanece central no ciclo do .NET.

## 9. Criando o Projeto

Após a configuração de template, nome, localização, solução e versão do .NET, o Visual Studio executa:

- Criação de arquivos;
    
- Carregamento de bibliotecas;
    
- Restauração de pacotes NuGet;
    
- Configuração de dependências;
    
- Preparação dos SDKs necessários.
    

## 10. A Grande Diferença do .NET MAUI

Diferente do Xamarin, onde cada plataforma exigia um projeto dedicado:

Plaintext

```
-- Modelo Xamarin Antigo --
Solução
│
├── Projeto principal
├── Projeto Android
├── Projeto iOS
└── Projeto Windows
```

No **.NET MAUI**, adota-se o modelo de **Single Project** (projeto único):

Plaintext

```
             .NET MAUI
                 │
        ┌────────┴────────┐
        │ Um único projeto│
        └────────┬────────┘
   ┌────────┬────┴───┬────────┐
   ↓        ↓        ↓        ↓
Android    iOS    Windows    Mac
```

## 11. Pasta Dependencies

Representa as dependências, bibliotecas e componentes necessários:

Plaintext

```
Dependencies
│
├── SDK
├── Pacotes
├── Analyzers
├── Frameworks
└── Referências
```

As dependências são segmentadas internamente para cada sistema operacional:

- **Android:** Bibliotecas MAUI + Bibliotecas .NET + Bibliotecas Android
    
- **iOS:** Bibliotecas MAUI + Bibliotecas .NET + Bibliotecas iOS
    

## 12. Pastas Properties e Platforms

### Properties

Contém arquivos de configuração de ambiente e perfis de inicialização (ex.: perfil de execução do Windows).

### Platforms

Concentra o código e as APIs que não podem ser completamente abstraídos:

Plaintext

```
Platforms
│
├── Android/        (MainActivity, MainApplication, Manifest)
├── iOS/            (AppDelegate, Info.plist)
├── MacCatalyst/    (Configurações específicas para macOS)
└── Windows/        (App, Package, Manifest)
```

## 13. Seleção da Plataforma de Execução

A plataforma de destino é selecionada diretamente na barra de ferramentas do Visual Studio:

Plaintext

```
▶ App Número da Sorte
        ↓
┌──────────────────────┐
│ Windows Machine      │
│ Android Emulator     │
│ Android Device       │
│ iPhone Simulator     │
│ Mac Catalyst         │
└──────────────────────┘
```

## 14. Pasta Resources

Centraliza os recursos visuais e estilos compartilhados para evitar duplicação entre sistemas operacionais:

Plaintext

```
             Resources
                 │
          ┌──────┴──────┐
       Ícones         Fontes
          │             │
     ┌────┼────┐        │
     ↓    ↓    ↓        ↓
 Android iOS Windows   Todas
```

## 15. Execução e Tela Inicial Padrão

Ao compilar e executar o template inicial (sem debug para maior agilidade), a interface renderiza:


```
┌─────────────────────────────┐
│        App Número da Sorte  │
├─────────────────────────────┤
│                             │
│          [ .NET ]           │
│                             │
│     Welcome to .NET MAUI    │
│                             │
│          [ CLICK ME ]       │
│                             │
└─────────────────────────────┘
```

### Comportamento do Botão

O evento de clique incrementa dinamicamente a contagem na tela:

$$\text{Clique do Usuário} \longrightarrow \text{Evento Click} \longrightarrow \text{C\# Code-Behind} \longrightarrow \text{Incrementa Contador} \longrightarrow \text{Atualiza Label}$$

- Clique 1 → `"You clicked me 1 time"`
    
- Clique 2 → `"You clicked me 2 times"`
    

## 16. Estrutura de Pastas e Comparativos

### Estrutura Geral

Plaintext

```
App Número da Sorte
│
├── Dependencies/
├── Properties/
├── Platforms/
│   ├── Android/
│   ├── iOS/
│   ├── MacCatalyst/
│   └── Windows/
├── Resources/
│   ├── AppIcon/
│   ├── Fonts/
│   ├── Images/
│   ├── Splash/
│   └── Styles/
└── Arquivos de Código / XAML
```

### Resumo dos Diretórios

|**Pasta / Elemento**|**Função**|
|---|---|
|`Dependencies`|Bibliotecas, SDKs, pacotes e referências do projeto|
|`Properties`|Configurações do projeto e perfis de depuração|
|`Platforms`|Código e configurações específicos de cada plataforma|
|`Platforms/Android`|Elementos e ciclo de vida específicos do Android|
|`Platforms/iOS`|Elementos e ciclo de vida específicos do iOS|
|`Platforms/MacCatalyst`|Elementos específicos do macOS via Mac Catalyst|
|`Platforms/Windows`|Elementos específicos do Windows|
|`Resources`|Recursos compartilhados da aplicação|
|`Resources/Fonts`|Fontes tipográficas do aplicativo|
|`Resources/Images`|Imagens da interface|
|`Resources/AppIcon`|Ícone do aplicativo adaptado automaticamente|
|`Resources/Splash`|Tela de carregamento (_Splash Screen_)|
|`Resources/Styles`|Estilos, cores e temas visuais da aplicação|

### Comparativo: Xamarin × .NET MAUI

|**Xamarin**|**.NET MAUI**|
|---|---|
|Estrutura com vários projetos|Um único projeto (_Single Project_)|
|Projeto Android separado|Pasta `Platforms/Android`|
|Projeto iOS separado|Pasta `Platforms/iOS`|
|Projeto Windows separado|Pasta `Platforms/Windows`|
|Maior duplicação estrutural|Maior compartilhamento de código|
|Recursos distribuídos entre projetos|Pasta `Resources` centralizada|
|Plataforma selecionada trocando o projeto padrão|Plataforma selecionada no seletor de execução|

## 17. Passo a Passo da Aula

|**#**|**Ação do Professor**|**Objetivo**|
|---|---|---|
|**1**|Abriu a criação de projeto|Iniciar a aplicação|
|**2**|Pesquisou por `MAUI`|Encontrar os templates disponíveis|
|**3**|Escolheu _Aplicativo .NET MAUI_|Criar a aplicação gráfica principal|
|**4**|Definiu a localização|Organizar a estrutura de pastas no disco|
|**5**|Nomeou o projeto|Definir `App Número da Sorte`|
|**6**|Organizou a solução|Preparar container para múltiplos projetos|
|**7**|Criou a pasta `EP01`|Organizar o código deste primeiro módulo|
|**8**|Escolheu `.NET 6`|Definir o framework alvo|
|**9**|Criou o projeto|Disparar a geração de arquivos|
|**10**|Abriu o projeto|Inspecionar a árvore de arquivos|
|**11**|Mostrou `Dependencies`|Explicar SDKs e pacotes por plataforma|
|**12**|Mostrou `Properties`|Explicar configurações de execução|
|**13**|Mostrou seleção de plataforma|Explicar o destino de build|
|**14**|Mostrou `Platforms`|Explicar código nativo/específico|
|**15**|Mostrou `Resources`|Explicar a unificação de assets|
|**16**|Executou o projeto|Testar a compilação e execução|
|**17**|Clicou no botão|Demonstrar o evento interativo básico|
|**18**|Explicou a organização geral|Preparar o conteúdo da próxima aula|

## 18. Pontos-Chave para Revisão

1. **Multiplataforma Unificada:** Desenvolvimento para Android, iOS, macOS e Windows em uma única base.
    
2. **Projeto Único:** Centralização de arquivos, configurações e compilação sem projetos separados por OS.
    
3. **Isolamento em `Platforms`:** Código que depende de APIs nativas reside na pasta correspondente do sistema operacional.
    
4. **Centralização em `Resources`:** Imagens, ícones, fontes e temas gerenciados em local único com processamento automático no build.
    
5. **Seleção de Destino:** Execução alternada diretamente pelo seletor de dispositivos/emuladores do Visual Studio.
    
6. **Template Funcional:** O template inicial já inclui pipeline de compilação, layout XAML e lógica em C#.
    

## 🧠 Mapa Mental


```
                    .NET MAUI
                        │
            ┌───────────┴───────────┐
            │                       │
       UM PROJETO              MULTIPLATAFORMA
            │                       │
            │          ┌────────────┼────────────┐
            │          ↓            ↓            ↓
            │       Android        iOS        Windows
            │
     ┌──────┼───────────┐
     ↓      ↓           ↓
Dependencies Properties Platforms
                            │
                ┌───────────┼───────────┐
                ↓           ↓           ↓
             Android       iOS       Windows
                            
                        +
                    Resources
                        │
             ┌──────────┼──────────┐
             ↓          ↓          ↓
          Imagens     Fontes     Ícones
```

> [!SUMMARY] **Síntese**
> 
> O professor cria o projeto **App Número da Sorte**, organiza a solução e apresenta a arquitetura do **.NET MAUI**, com foco no modelo de projeto único, suporte multiplataforma, pasta `Platforms` para particularidades de cada sistema e `Resources` para centralização de assets.
> 
> _Próximo passo: Análise detalhada do fluxo de execução do aplicativo (do bootstrap da plataforma até a renderização da interface)._