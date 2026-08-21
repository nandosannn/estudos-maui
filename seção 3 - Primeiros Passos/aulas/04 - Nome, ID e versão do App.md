# Configurações Iniciais de um Projeto .NET MAUI

## 1. Visão geral

Nesta aula são apresentadas as **primeiras configurações de um projeto .NET MAUI**, principalmente aquelas relacionadas a:

- Nome do aplicativo;
    
- Identificação do aplicativo;
    
- Versão de exibição;
    
- Versão interna do aplicativo;
    
- Plataformas suportadas;
    
- Configurações específicas de cada plataforma;
    
- Publicação do aplicativo nas lojas.
    

O .NET MAUI permite centralizar grande parte dessas configurações em um único projeto e, posteriormente, aplicar essas informações às diferentes plataformas suportadas.

---

# 2. Plataformas suportadas pelo .NET MAUI

Um dos primeiros pontos importantes do arquivo de configuração do projeto é observar quais plataformas podem ser utilizadas.

Um projeto .NET MAUI pode trabalhar com:

|Plataforma|Finalidade|
|---|---|
|**Android**|Aplicativos para dispositivos Android|
|**iOS**|Aplicativos para iPhone e iPad|
|**Mac Catalyst**|Aplicativos para computadores macOS|
|**Windows**|Aplicativos para computadores Windows|
|**Tizen**|Plataforma utilizada principalmente em dispositivos Samsung, como Smart TVs|

A grande vantagem é que podemos trabalhar com **um único projeto .NET MAUI** e gerar aplicações para diferentes ecossistemas.

### Estrutura conceitual

```text
                  .NET MAUI
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
     Android         iOS       Windows
        │            │            │
        └────────────┼────────────┘
                     ↓
                Mac Catalyst
```

Dependendo da configuração e das ferramentas utilizadas, outras plataformas também podem ser habilitadas.

---

# 3. Onde configurar o projeto?

Existem duas formas principais de acessar as configurações do projeto.

## 3.1. Arquivo do projeto

Podemos clicar no projeto dentro do Visual Studio para acessar o arquivo de configuração.

Esse arquivo contém diversas configurações importantes do projeto.

Entre elas estão informações relacionadas a:

- Plataformas;
    
- Nome do aplicativo;
    
- Identificação;
    
- Versão;
    
- Configurações de compilação;
    
- Configurações específicas das plataformas.
    

---

## 3.2. Propriedades do projeto

Outra maneira é clicar com o botão direito sobre o projeto e selecionar:

```text
Propriedades
```

A tela de propriedades apresenta diversas configurações organizadas por categorias.

Podemos encontrar configurações relacionadas a:

- .NET;
    
- Android;
    
- iOS;
    
- Windows;
    
- Mac Catalyst;
    
- Linguagem C#;
    
- Compilação;
    
- Pacotes de instalação;
    
- Publicação.
    

Como o objetivo da aula é trabalhar principalmente com a identificação e a versão do aplicativo, o foco está nas configurações compartilhadas.

---

# 4. Configurações compartilhadas

Dentro das propriedades do projeto, encontramos uma área relacionada ao **MAUI compartilhado**.

Nessa área podemos configurar informações que serão utilizadas como padrão pelas diferentes plataformas.

Entre as principais configurações estão:

|Configuração|Finalidade|
|---|---|
|**Application Title**|Nome de exibição do aplicativo|
|**Application ID**|Identificação do aplicativo|
|**Application Display Version**|Versão amigável exibida para o usuário|
|**Application Version**|Número interno da versão do aplicativo|

Essas configurações são importantes principalmente quando o aplicativo será distribuído ou publicado nas lojas.

---

# 5. Configuração do nome do aplicativo

A propriedade relacionada ao título define o **nome que será apresentado ao usuário**.

Por exemplo:

```text
Número da Sorte
```

Esse é o nome amigável do aplicativo.

Podemos pensar nessa configuração da seguinte maneira:

```text
Application Title
       │
       ↓
"Número da Sorte"
       │
       ↓
Nome apresentado ao usuário
```

Uma das vantagens do .NET MAUI é que podemos definir esse valor de forma centralizada.

Assim, o nome pode ser utilizado nas diferentes plataformas.

---

# 6. Personalização por plataforma

Apesar de existir uma configuração central, o .NET MAUI também permite fazer configurações específicas para cada plataforma.

Por exemplo, podemos definir um nome geral:

```text
Número da Sorte
```

E, caso seja necessário, configurar um nome diferente especificamente para o Android.

Isso permite trabalhar com:

```text
Configuração compartilhada
          │
          ├── Android
          ├── iOS
          ├── Windows
          └── Mac Catalyst
```

Ou seja, existe uma **configuração padrão**, mas ela pode ser sobrescrita por configurações específicas de cada plataforma.

---

# 7. AndroidManifest

No Android existe um arquivo chamado:

```text
AndroidManifest.xml
```

Esse arquivo contém diversas informações importantes sobre o aplicativo Android.

Entre elas estão informações relacionadas a:

- Nome do aplicativo;
    
- Identificação;
    
- Permissões;
    
- Componentes;
    
- Configurações específicas do Android.
    

No .NET MAUI, muitas configurações podem ser definidas de maneira centralizada e o framework utiliza essas informações para gerar/configurar os arquivos específicos de cada plataforma.

Podemos visualizar a ideia assim:

```text
        Configuração central
                │
                ↓
             .NET MAUI
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
   Android     iOS    Windows
       │
       ↓
AndroidManifest.xml
```

Isso facilita bastante o desenvolvimento multiplataforma.

---

# 8. Application ID

O **Application ID** é diferente do nome que aparece para o usuário.

Enquanto:

```text
Application Title
```

representa o nome amigável do aplicativo, o:

```text
Application ID
```

serve para **identificar o aplicativo**.

Uma prática comum é utilizar o formato de **domínio reverso**.

## Exemplo

Imagine que uma empresa possui o domínio:

```text
empresa.com.br
```

O domínio pode ser invertido para:

```text
br.com.empresa
```

Depois acrescentamos o nome do aplicativo:

```text
br.com.empresa.numerodasorte
```

Esse formato ajuda a criar identificadores únicos.

### Estrutura

```text
br
 │
 └── com
      │
      └── empresa
            │
            └── numerodasorte
```

No exemplo apresentado na aula, o professor utiliza uma empresa fictícia chamada **Space Bidu**, criando um identificador seguindo essa ideia.

---

# 9. GUID

O projeto também possui um identificador baseado em **GUID (Globally Unique Identifier)**.

GUID significa:

> Globally Unique Identifier

Ou seja:

> Identificador Globalmente Único.

Um GUID possui uma estrutura semelhante a:

```text
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Exemplo:

```text
550e8400-e29b-41d4-a716-446655440000
```

A ideia é gerar um identificador com uma probabilidade extremamente baixa de colisão.

### Importante

O GUID não deve ser confundido com o **Application ID**.

São identificadores diferentes e possuem finalidades diferentes dentro do projeto.

---

# 10. Application Display Version

A **Application Display Version** representa a versão que normalmente será apresentada de forma amigável.

Um exemplo seria:

```text
1.0.0
```

ou:

```text
1.0
```

Essa versão é voltada principalmente para comunicação da versão do aplicativo.

Podemos pensar nela como:

```text
Versão exibida
      │
      ↓
   1.0.0
      │
      ↓
Usuário consegue identificar
a versão do aplicativo
```

---

# 11. Versionamento do aplicativo

O versionamento permite indicar a evolução do aplicativo.

Um formato bastante utilizado é:

```text
MAJOR.MINOR.PATCH
```

Por exemplo:

```text
1.0.0
```

Cada parte possui um significado.

|Parte|Nome|Significado|
|---|---|---|
|**1**|MAJOR|Mudança grande ou incompatível|
|**0**|MINOR|Nova funcionalidade|
|**0**|PATCH|Correção de problemas|

---

# 12. PATCH — correções pequenas

O último número geralmente é utilizado para indicar **correções ou pequenas alterações**.

Imagine que o aplicativo esteja na versão:

```text
1.0.0
```

Foi encontrado um bug no cadastro.

O aplicativo continua sendo essencialmente o mesmo, mas o problema foi corrigido.

A versão pode passar para:

```text
1.0.1
```

Podemos visualizar:

```text
1.0.0
  │
  └── Correção de bug
          ↓
       1.0.1
```

Também pode ser utilizado para pequenas alterações que não modificam significativamente o aplicativo.

### Exemplo

Versão inicial:

```text
1.0.0
```

Correção de um problema:

```text
1.0.1
```

Outra correção:

```text
1.0.2
```

Mais uma correção:

```text
1.0.3
```

---

# 13. MINOR — novas funcionalidades

O número do meio pode ser utilizado quando adicionamos **novas funcionalidades** sem realizar uma grande mudança estrutural no aplicativo.

Imagine que o aplicativo inicialmente gere números para a Mega-Sena:

```text
1.0.0
```

Posteriormente, adicionamos uma nova funcionalidade para gerar números de outra modalidade.

Podemos alterar para:

```text
1.1.0
```

Depois adicionamos outra funcionalidade:

```text
1.2.0
```

Visualmente:

```text
1.0.0
 │
 └── Nova funcionalidade
          ↓
       1.1.0
          │
          └── Outra funcionalidade
                    ↓
                 1.2.0
```

A ideia é indicar que o aplicativo continua sendo da mesma geração principal, mas ganhou funcionalidades.

---

# 14. MAJOR — grandes mudanças

O primeiro número representa uma mudança mais significativa.

Imagine que o aplicativo esteja na versão:

```text
1.5.3
```

Depois de algum tempo, ele passa por uma grande reformulação:

- Novo design;
    
- Nova arquitetura;
    
- Novas funcionalidades;
    
- Alterações importantes;
    
- Mudanças que podem tornar a nova versão incompatível com a anterior.
    

Nesse caso, podemos passar para:

```text
2.0.0
```

Visualmente:

```text
1.5.3
  │
  │
  └── Grande reestruturação
             ↓
          2.0.0
```

---

# 15. Resumo do versionamento

Uma forma simples de memorizar:

```text
        1 . 2 . 3
        │   │   │
        │   │   └── PATCH
        │   │       Correções
        │   │
        │   └────── MINOR
        │           Novas funcionalidades
        │
        └────────── MAJOR
                    Grandes mudanças
```

### Exemplos

|Versão|Interpretação|
|---|---|
|`1.0.0`|Primeira versão|
|`1.0.1`|Correção de bug|
|`1.0.2`|Outra correção|
|`1.1.0`|Nova funcionalidade|
|`1.2.0`|Outra funcionalidade|
|`2.0.0`|Grande reformulação|

> **Observação:** isso é uma convenção de versionamento. O significado exato de cada segmento pode variar conforme a política adotada pelo projeto.

---

# 16. Application Version

A propriedade **Application Version** possui uma função diferente da versão de exibição.

Ela representa um **número de versão utilizado internamente pelas plataformas e pelos processos de publicação**.

De forma simplificada:

```text
Application Display Version
        ↓
Versão amigável
Exemplo: 1.2.0

Application Version
        ↓
Versão interna
Exemplo: 3
```

A versão interna possui regras mais restritas e, dependendo da plataforma, existem requisitos específicos para o formato e para a progressão desse valor.

---

# 17. Diferença entre Display Version e Application Version

Essa é uma das partes mais importantes da aula.

|Propriedade|Exemplo|Objetivo|
|---|---|---|
|**Application Title**|Número da Sorte|Nome do aplicativo|
|**Application ID**|br.com.empresa.numerodasorte|Identificar o aplicativo|
|**Application Display Version**|1.2.0|Versão amigável|
|**Application Version**|3|Versão interna|

Podemos representar:

```text
                 APLICATIVO
                     │
        ┌────────────┼─────────────┐
        ↓            ↓             ↓
      Nome           ID          Versões
        │            │             │
        ↓            ↓       ┌─────┴─────┐
Número da Sorte   br.com...  ↓           ↓
                         Display      Application
                         Version        Version
                           1.2.0           3
```

---

# 18. Exemplo completo

Imagine que estamos desenvolvendo o aplicativo:

```text
Número da Sorte
```

Podemos ter:

```text
Application Title:
Número da Sorte

Application ID:
br.com.spacebidu.numerodasorte

Application Display Version:
1.0.0

Application Version:
1
```

Depois corrigimos um problema:

```text
Application Display Version:
1.0.1

Application Version:
2
```

Depois adicionamos uma nova funcionalidade:

```text
Application Display Version:
1.1.0

Application Version:
3
```

Depois fazemos uma grande reformulação:

```text
Application Display Version:
2.0.0

Application Version:
4
```

Perceba que a **versão exibida** e a **versão interna** não precisam necessariamente ter a mesma numeração.

---

# 19. Versionamento utilizando datas

A versão de exibição também pode seguir outras convenções.

Por exemplo:

```text
2026.08.21
```

Isso poderia representar:

```text
2026 → ano
08   → mês
21   → dia
```

Também é possível adotar formatos mais detalhados, dependendo da estratégia do projeto.

Porém, para aplicativos publicados em lojas, é importante respeitar as regras de versionamento exigidas pela plataforma.

---

# 20. Configuração centralizada x configuração específica

Uma das principais vantagens apresentadas na aula é a possibilidade de configurar informações de maneira centralizada.

### Configuração centralizada

```text
               Projeto .NET MAUI
                      │
                      ↓
             Configurações comuns
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
    Android          iOS          Windows
```

Isso evita ter que configurar manualmente a mesma informação em diversos arquivos.

### Configuração específica

Quando necessário, podemos sobrescrever uma configuração para uma plataforma específica.

Por exemplo:

```text
Nome padrão:
Número da Sorte
```

Mas:

```text
Android:
Número da Sorte Android
```

Assim, temos flexibilidade para trabalhar tanto com configurações compartilhadas quanto específicas.

---

# 21. O que acontece durante a publicação?

Essas configurações são especialmente importantes quando queremos gerar versões do aplicativo para distribuição.

O .NET MAUI utiliza as informações do projeto para preparar a aplicação para cada plataforma.

Podemos imaginar o processo:

```text
                Projeto MAUI
                     │
                     ↓
          Configurações do projeto
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    Android         iOS         Windows
       │             │             │
       ↓             ↓             ↓
   Pacote Android  App iOS    Aplicação Windows
       │             │             │
       ↓             ↓             ↓
 Google Play      App Store    Distribuição
```

Por isso, informações como **identificação e versionamento** precisam ser configuradas corretamente.

---

# 22. Principais conceitos da aula

## Application Title

É o **nome amigável** do aplicativo.

Exemplo:

```text
Número da Sorte
```

---

## Application ID

É o identificador do aplicativo.

É comum utilizar o formato de domínio reverso:

```text
br.com.empresa.aplicativo
```

Exemplo:

```text
br.com.spacebidu.numerodasorte
```

---

## GUID

É um identificador globalmente único utilizado pelo projeto.

Exemplo:

```text
550e8400-e29b-41d4-a716-446655440000
```

---

## Application Display Version

É a versão apresentada de forma amigável.

Exemplo:

```text
1.0.0
```

Pode seguir uma estratégia como:

```text
MAJOR.MINOR.PATCH
```

---

## Application Version

É o identificador numérico interno da versão utilizado no processo de publicação.

Exemplo:

```text
1
2
3
4
```

A cada nova versão distribuída, normalmente esse valor precisa avançar conforme as regras da plataforma.

---

# 23. Resumo para revisão

> **.NET MAUI permite criar aplicativos multiplataforma a partir de um único projeto.**

As configurações principais estudadas foram:

```text
Application Title
        ↓
Nome apresentado ao usuário

Application ID
        ↓
Identificação única do aplicativo

GUID
        ↓
Identificador globalmente único

Application Display Version
        ↓
Versão amigável
Exemplo: 1.2.0

Application Version
        ↓
Versão interna
Exemplo: 3
```

### Versionamento

```text
MAJOR.MINOR.PATCH
   │      │     │
   │      │     └── Correções
   │      │
   │      └──────── Novas funcionalidades
   │
   └─────────────── Grandes mudanças
```

### Exemplo:

```text
1.0.0 → Primeira versão
1.0.1 → Correção de bug
1.1.0 → Nova funcionalidade
2.0.0 → Grande reformulação
```

### Ideia central

O ponto mais importante da aula é entender que o **.NET MAUI centraliza diversas configurações do aplicativo**, permitindo que informações como nome, identificação e versão sejam definidas no projeto e utilizadas nas diferentes plataformas.

Ao mesmo tempo, o desenvolvedor mantém a possibilidade de **personalizar determinadas configurações individualmente para Android, iOS, Windows ou Mac Catalyst**.