# Splash Screen no .NET MAUI

## 1. Introdução

Nesta aula foi apresentada a configuração da **Splash Screen** de um aplicativo .NET MAUI.

A Splash Screen é a tela exibida **durante o carregamento inicial do aplicativo**, enquanto o sistema operacional prepara a aplicação para ser executada.

No exemplo da aula, a Splash Screen padrão do .NET MAUI, que apresenta a identidade visual do framework, será substituída pela identidade visual do aplicativo **Número da Sorte**.

A ideia geral é:

```text
Aplicativo iniciado
       │
       ↓
Splash Screen
       │
       ↓
Carregamento do aplicativo
       │
       ↓
Tela principal
```

---

# 2. O que é uma Splash Screen?

A **Splash Screen** é uma tela temporária exibida enquanto o aplicativo está sendo inicializado.

Ela normalmente apresenta:

- Logo do aplicativo;
    
- Nome ou identidade visual;
    
- Cor de fundo;
    
- Elementos visuais relacionados à marca.
    

Ela aparece por um período muito curto.

No exemplo da aula, o aplicativo inicialmente apresenta a Splash Screen e, depois de carregado, exibe a tela principal.

```text
┌─────────────────────────┐
│                         │
│       🍀                │
│                         │
│    Número da Sorte      │
│                         │
└─────────────────────────┘
             ↓
┌─────────────────────────┐
│                         │
│   Tela principal        │
│                         │
└─────────────────────────┘
```

---

# 3. Splash Screen x Ícone do aplicativo

É importante não confundir esses dois recursos.

|Recurso|Função|
|---|---|
|**App Icon**|Identifica o aplicativo no sistema operacional|
|**Splash Screen**|É exibida enquanto o aplicativo está sendo carregado|

Por exemplo:

### Ícone

É o elemento que aparece na lista de aplicativos, menu iniciar, área de trabalho etc.

```text
┌───────┐
│  🍀   │
└───────┘
Número da Sorte
```

### Splash Screen

É apresentada durante a inicialização:

```text
┌──────────────────────┐
│                      │
│        🍀            │
│                      │
└──────────────────────┘
```

Portanto:

> **Ícone identifica o aplicativo; Splash Screen aparece durante o carregamento.**

---

# 4. Problema encontrado com a imagem da Splash Screen

Durante a aula foi identificado um comportamento problemático do gerenciador de recursos do .NET MAUI.

Quando uma imagem retangular é utilizada como Splash Screen, pode ocorrer um comportamento em que a imagem é tratada como se fosse quadrada.

Isso pode provocar:

- Distorção;
    
- Redimensionamento inadequado;
    
- Alteração da proporção da imagem;
    
- Resultado visual diferente do esperado.
    

Por isso, no exemplo da aula, foi utilizada uma **imagem quadrada**.

---

# 5. Preparando a imagem

Para evitar problemas com a Splash Screen, a imagem foi preparada em um editor gráfico.

A ideia foi criar uma área quadrada:

```text
┌────────────────────┐
│                    │
│                    │
│       🍀           │
│                    │
│                    │
└────────────────────┘
```

A logo foi posicionada no centro dessa área.

Depois, o fundo foi configurado com a cor utilizada pelo aplicativo.

No exemplo:

```text
#00AB37
```

Essa é a cor verde utilizada no projeto.

---

# 6. Exportando a imagem

Depois de preparar a imagem, ela foi exportada no formato:

```text
SVG
```

O arquivo foi chamado de:

```text
Splash.svg
```

E colocado na pasta de recursos do projeto.

Por exemplo:

```text
Resources/
└── Splash/
    └── Splash.svg
```

A localização exata pode variar de acordo com a estrutura do projeto, mas o importante é que o arquivo seja tratado pelo .NET MAUI como um recurso de Splash Screen.

---

# 7. Por que substituir o arquivo existente?

Na aula foi recomendado **substituir o arquivo de Splash Screen existente**, mantendo o mesmo nome, em vez de criar outro arquivo com nome diferente.

Por exemplo:

```text
Splash.svg
```

é substituído pela nova imagem.

Isso facilita porque a configuração do projeto já possui uma referência para esse arquivo.

Assim, não é necessário alterar várias configurações.

A ideia é:

```text
Splash.svg antigo
       ↓
Substituir
       ↓
Splash.svg novo
       ↓
Projeto continua referenciando o mesmo arquivo
```

---

# 8. Configuração no arquivo `.csproj`

As configurações dos recursos do .NET MAUI podem ser encontradas no arquivo de projeto:

```text
.csproj
```

Esse arquivo possui configurações relacionadas à compilação e aos recursos utilizados pelo aplicativo.

Um exemplo de configuração de Splash Screen pode ser semelhante a:

```xml
<MauiSplashScreen
    Include="Resources\Splash\splash.svg"
    Color="#00AB37"
    BaseSize="178,178" />
```

A configuração pode variar de acordo com a versão do .NET MAUI e com a estrutura do projeto.

---

# 9. Build Action

Um conceito importante apresentado na aula é a **Build Action**.

A Build Action determina como um determinado arquivo será tratado durante o processo de compilação.

Para recursos do .NET MAUI, encontramos configurações específicas.

Por exemplo:

```text
MauiSplashScreen
```

indica que o arquivo deve ser tratado como um recurso de Splash Screen.

Para o ícone, temos algo semelhante:

```text
MauiIcon
```

Podemos pensar:

```text
Arquivo
   │
   ↓
Build Action
   │
   ├── MauiIcon
   │
   └── MauiSplashScreen
```

Isso informa ao processo de compilação qual é a finalidade daquele recurso.

---

# 10. MauiSplashScreen

Quando encontramos:

```xml
<MauiSplashScreen>
```

estamos informando ao .NET MAUI que determinado arquivo deve ser utilizado como **Splash Screen**.

Por exemplo:

```xml
<MauiSplashScreen
    Include="Resources\Splash\splash.svg"
    Color="#00AB37" />
```

Nesse caso:

```text
Include
   ↓
Define qual arquivo será utilizado

Color
   ↓
Define a cor de fundo
```

---

# 11. Propriedade `Include`

A propriedade:

```xml
Include
```

indica o arquivo que será utilizado.

Exemplo:

```xml
Include="Resources\Splash\splash.svg"
```

Isso significa:

> Utilize o arquivo `splash.svg` localizado dentro da pasta de recursos de Splash Screen.

Podemos representar:

```text
Resources
   │
   └── Splash
         │
         └── splash.svg
                ↑
                │
             Include
```

---

# 12. Propriedade `Color`

A propriedade:

```xml
Color
```

define a cor de fundo da Splash Screen.

Exemplo:

```xml
Color="#00AB37"
```

Nesse projeto, o fundo será verde.

```text
Splash Screen

┌─────────────────────────┐
│                         │
│          🍀             │
│                         │
└─────────────────────────┘

Fundo:
#00AB37
```

Essa configuração é importante porque a imagem pode não ocupar toda a tela.

O sistema pode utilizar a cor configurada como fundo ao redor da imagem.

---

# 13. Propriedade `BaseSize`

Outra propriedade importante é:

```text
BaseSize
```

Ela representa o **tamanho base/original utilizado como referência para o processamento do recurso**.

Exemplo:

```xml
BaseSize="178,178"
```

Isso indica:

```text
Largura: 178
Altura: 178
```

Podemos visualizar:

```text
        178
   ┌────────────┐
   │            │
   │     🍀     │ 178
   │            │
   └────────────┘
```

O .NET MAUI utiliza esse tamanho como referência para gerar os diferentes tamanhos necessários para cada plataforma e densidade.

---

# 14. Por que utilizar uma imagem quadrada?

No exemplo da aula, a imagem foi propositalmente criada como quadrada.

Por exemplo:

```text
178 × 178
```

em vez de:

```text
300 × 178
```

A razão é evitar problemas de redimensionamento e distorção.

Uma imagem retangular poderia acabar sendo adaptada pelo processo de geração da Splash Screen de maneira inadequada.

Por isso:

```text
Imagem quadrada
      ↓
Mais previsível
      ↓
Melhor adaptação
```

---

# 15. Propriedade `Resize`

Também existe a possibilidade de controlar o redimensionamento do recurso.

A propriedade é:

```text
Resize
```

Por exemplo:

```xml
Resize="true"
```

Quando configurada como `true`, o recurso pode ser redimensionado conforme necessário.

De maneira simplificada:

```text
Resize = true
      ↓
Permite redimensionamento
```

Quando determinados valores não são especificados, o .NET MAUI pode utilizar valores padrão para realizar o processamento do recurso.

---

# 16. Valores padrão

Caso algumas propriedades não sejam informadas, o .NET MAUI pode utilizar valores padrão.

Por exemplo, se o `BaseSize` não for especificado, o sistema pode utilizar o tamanho da própria imagem como referência.

Da mesma maneira, determinadas propriedades possuem comportamentos padrão definidos pelo framework.

Isso significa que não é obrigatório configurar absolutamente todas as propriedades.

Porém, quando precisamos de um resultado visual específico, podemos definir explicitamente os valores.

---

# 17. Exemplo de configuração

Uma configuração simplificada pode ser:

```xml
<MauiSplashScreen
    Include="Resources\Splash\splash.svg"
    Color="#00AB37"
    BaseSize="178,178" />
```

Podemos interpretar cada parte:

```text
<MauiSplashScreen
       │
       ├── Include
       │      └── Arquivo da Splash Screen
       │
       ├── Color
       │      └── Cor de fundo
       │
       └── BaseSize
              └── Tamanho base da imagem
/>
```

---

# 18. Splash Screen em cada plataforma

Um ponto importante da aula é que o comportamento da Splash Screen **não é exatamente igual em todas as plataformas**.

## Android

No Android, a Splash Screen pode ser apresentada durante a inicialização do aplicativo.

```text
Android
   │
   ↓
Splash Screen
   │
   ↓
Aplicativo
```

---

## iOS

No iOS também existe uma tela de inicialização.

```text
iOS
 │
 ↓
Splash Screen
 │
 ↓
Aplicativo
```

O resultado visual é semelhante à ideia apresentada no Android.

---

## Mac Catalyst

No Mac Catalyst, o comportamento é diferente.

Em vez de apresentar uma Splash Screen da mesma maneira que ocorre nos dispositivos móveis, o sistema apresenta outro mecanismo visual durante a inicialização.

Por exemplo, o ícone do aplicativo pode apresentar uma animação de carregamento no macOS.

A ideia é:

```text
Aplicativo aberto
       ↓
Ícone apresenta animação
       ↓
Aplicativo termina de carregar
       ↓
Tela principal
```

---

# 19. Windows

O comportamento também é diferente no Windows.

A versão utilizada na aula não apresenta a Splash Screen da mesma maneira que o Android e o iOS.

O aplicativo pode abrir diretamente a interface principal.

Assim:

```text
Windows

Abrir aplicativo
       ↓
Tela principal
```

Enquanto em dispositivos móveis:

```text
Android / iOS

Abrir aplicativo
       ↓
Splash Screen
       ↓
Tela principal
```

---

# 20. Por que o comportamento é diferente?

Isso acontece porque cada sistema operacional possui seus próprios mecanismos para inicialização de aplicativos.

O .NET MAUI tenta fornecer uma experiência multiplataforma, mas **não significa que todos os recursos terão exatamente o mesmo comportamento visual em todas as plataformas**.

Podemos pensar:

```text
                 .NET MAUI
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
     Android         iOS       Windows
        │            │            │
     Splash       Splash       Outro
        │            │         comportamento
        ↓            ↓            ↓
   Sistema        Sistema      Sistema
   Android          iOS        Windows
```

---

# 21. Problemas e bugs do gerenciador de recursos

Durante a aula também foi comentado que algumas funcionalidades relacionadas ao gerenciamento automático de ícones e Splash Screens ainda podem apresentar problemas dependendo da versão do .NET MAUI.

Alguns recursos podem não funcionar exatamente como esperado.

Por isso, pode ser necessário:

- Adaptar a imagem;
    
- Criar versões específicas para determinada plataforma;
    
- Alterar propriedades manualmente;
    
- Substituir arquivos existentes;
    
- Acompanhar correções do projeto;
    
- Atualizar a versão do .NET MAUI.
    

A ideia é que essas ferramentas continuem evoluindo com o tempo.

---

# 22. GitHub e acompanhamento de problemas

Quando existe um problema no framework, uma possibilidade é acompanhar as discussões e correções no repositório oficial do projeto.

Isso permite verificar:

- Bugs conhecidos;
    
- Issues abertas;
    
- Correções;
    
- Pull Requests;
    
- Novas versões;
    
- Mudanças futuras.
    

Assim, se determinada propriedade não estiver funcionando corretamente, pode existir uma issue relacionada ao problema.

---

# 23. Limpeza do projeto

Depois de modificar o ícone ou a Splash Screen, a aula recomenda realizar uma **limpeza do projeto**.

No Visual Studio, podemos utilizar:

```text
Build
   ↓
Clean Solution
```

A limpeza remove arquivos gerados anteriormente pela compilação.

Entre esses arquivos estão aqueles que ficam em diretórios como:

```text
bin/
obj/
```

---

# 24. Por que limpar o projeto?

Durante a compilação, o .NET MAUI gera diversos arquivos derivados dos recursos originais.

Por exemplo:

```text
splash.svg
    │
    ↓
Processamento
    │
    ↓
Arquivos gerados
```

Se modificarmos o arquivo original, podemos acabar observando um resultado antigo caso algum recurso gerado anteriormente ainda esteja sendo utilizado.

Ao limpar o projeto:

```text
Clean
  ↓
Remove arquivos gerados
  ↓
Build novamente
  ↓
Gera os recursos novamente
```

Isso ajuda a garantir que o aplicativo seja recompilado utilizando os arquivos atualizados.

---

# 25. Quando utilizar o Clean?

A limpeza não precisa ser realizada constantemente.

Durante o desenvolvimento normal das telas, geralmente não é necessário ficar executando:

```text
Clean Solution
```

a todo momento.

É especialmente útil quando estamos trabalhando com:

- Ícones;
    
- Splash Screens;
    
- Recursos;
    
- Arquivos gerados;
    
- Alterações que parecem não estar sendo refletidas.
    

Por exemplo:

```text
Alterei a imagem
       ↓
Executei o projeto
       ↓
Imagem antiga continua aparecendo
       ↓
Clean Solution
       ↓
Build novamente
       ↓
Verificar resultado
```

---

# 26. Processo completo realizado na aula

O processo apresentado pode ser resumido em algumas etapas.

### Etapa 1 — Criar/preparar a imagem

Foi criada uma imagem quadrada contendo a logo.

```text
Imagem quadrada
      +
Logo centralizada
      +
Fundo verde
```

---

### Etapa 2 — Exportar

A imagem foi exportada como:

```text
SVG
```

Com o nome:

```text
splash.svg
```

---

### Etapa 3 — Substituir o recurso

O arquivo existente foi substituído pelo novo arquivo.

```text
Splash.svg antigo
        ↓
Splash.svg novo
```

---

### Etapa 4 — Configurar o projeto

No `.csproj`, foram configuradas propriedades relacionadas à Splash Screen.

Exemplo:

```xml
<MauiSplashScreen
    Include="Resources\Splash\splash.svg"
    Color="#00AB37"
    BaseSize="178,178" />
```

---

### Etapa 5 — Limpar

Foi utilizado:

```text
Clean Solution
```

para remover arquivos gerados anteriormente.

---

### Etapa 6 — Compilar

O projeto foi compilado novamente.

```text
Clean
  ↓
Build
  ↓
Processamento dos recursos
  ↓
Aplicativo
```

---

### Etapa 7 — Executar

O aplicativo foi executado no Android.

Durante a inicialização, a nova Splash Screen apareceu.

```text
Abrir aplicativo
       ↓
Splash Screen
       ↓
Tela principal
```

---

# 27. Resultado obtido

O resultado foi uma Splash Screen personalizada com:

- Logo do aplicativo;
    
- Fundo verde;
    
- Formato quadrado;
    
- Identidade visual do projeto.
    

A Splash Screen aparece apenas durante um curto período, enquanto o aplicativo está carregando.

Depois disso, a aplicação apresenta sua tela principal.

---

# 28. Estrutura visual do resultado

```text
        INICIALIZAÇÃO
              │
              ↓
┌─────────────────────────────┐
│                             │
│                             │
│             🍀              │
│                             │
│                             │
└─────────────────────────────┘
         Splash Screen
              │
              ↓
       Carregamento
              │
              ↓
┌─────────────────────────────┐
│                             │
│       Número da Sorte       │
│                             │
│          Aplicativo         │
│                             │
└─────────────────────────────┘
         Tela principal
```

---

# 29. Conceitos importantes para memorizar

|Conceito|Explicação|
|---|---|
|**Splash Screen**|Tela apresentada durante a inicialização do aplicativo|
|**MauiSplashScreen**|Configuração que identifica um recurso como Splash Screen|
|**Include**|Define o arquivo utilizado|
|**Color**|Define a cor de fundo|
|**BaseSize**|Define o tamanho base usado como referência|
|**Resize**|Controla o comportamento de redimensionamento|
|**MauiIcon**|Configuração relacionada ao ícone do aplicativo|
|**SVG**|Formato utilizado para a imagem da Splash Screen|
|**Clean Solution**|Remove arquivos gerados para permitir uma nova compilação limpa|
|**Build**|Compila o projeto e gera novamente os recursos|

---

# 30. Resumo final

A aula mostrou como personalizar a **Splash Screen de um aplicativo .NET MAUI**.

O processo consiste basicamente em:

```text
Preparar imagem
      ↓
Exportar como SVG
      ↓
Colocar no projeto
      ↓
Configurar MauiSplashScreen
      ↓
Definir cor de fundo
      ↓
Definir BaseSize
      ↓
Limpar o projeto
      ↓
Compilar novamente
      ↓
Executar
      ↓
Verificar a Splash Screen
```

O arquivo de projeto pode conter uma configuração semelhante a:

```xml
<MauiSplashScreen
    Include="Resources\Splash\splash.svg"
    Color="#00AB37"
    BaseSize="178,178" />
```

O ponto mais importante é entender que o **.NET MAUI utiliza os recursos definidos no projeto para gerar os recursos necessários para cada plataforma**, mas cada sistema operacional pode apresentar esses recursos de maneira diferente.

No caso da Splash Screen:

```text
Android → Splash Screen
iOS     → Splash Screen
macOS   → Comportamento próprio do sistema
Windows → Comportamento próprio do sistema
```

Portanto, ao desenvolver uma aplicação multiplataforma, é importante **testar o resultado em cada plataforma**, pois o comportamento visual pode variar.