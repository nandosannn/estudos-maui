# 📱 Aula — Construção e estilização da primeira tela do aplicativo .NET MAUI

Nesta aula, o professor passa da explicação conceitual para a construção prática da primeira tela do aplicativo.

O objetivo é reproduzir, no projeto .NET MAUI, a aparência de um protótipo criado anteriormente. Para isso, ele trabalha principalmente com:

- `Image`;
    
- `Label`;
    
- `Button`;
    
- `Source`;
    
- `WidthRequest`;
    
- `HeightRequest`;
    
- `TextColor`;
    
- `BackgroundColor`;
    
- estilos globais;
    
- `CornerRadius`;
    
- `HorizontalOptions`;
    
- `VerticalOptions`;
    
- `Margin`;
    
- centralização dos elementos.
    

A sequência da aula é essencialmente:

Plaintext

```
Protótipo
   ↓
Limpeza da tela
   ↓
Exportação da imagem
   ↓
Importação para o projeto
   ↓
Criação dos componentes
   ↓
Dimensionamento da imagem
   ↓
Configuração dos estilos
   ↓
Posicionamento
   ↓
Margens
   ↓
Centralização
   ↓
Primeira tela concluída
```

## 1. 🎯 Objetivo da aula

O professor começa dizendo que agora serão feitas as modificações necessárias para construir a primeira tela do aplicativo.

A ideia é observar o protótipo e reproduzir sua aparência no projeto.

Portanto, diferentemente da aula anterior, em que os conceitos de página, layout, componentes, `Margin` e `Padding` foram apresentados, aqui o professor começa efetivamente a montar a interface.

## 2. 🧹 Primeiro passo — limpar a tela

O primeiro trabalho é deixar o projeto preparado para receber a nova interface.

O professor identifica que o protótipo possui um fundo totalmente branco.

Por isso, ele remove as cores que estavam sendo utilizadas anteriormente apenas para visualizar os componentes.

A ideia é:

**Antes:**

- Página → colorida
    
- Layout → colorido
    
- Componentes → cores de teste
    

**Depois:**

- Página → branco
    
- Layout → branco
    

> [!WARNING] Importante
> 
> As cores utilizadas anteriormente tinham finalidade didática: ajudavam a enxergar os limites dos componentes.
> 
> Agora elas deixam de ser necessárias porque a tela real deverá reproduzir o protótipo.

## 3. 🖼️ Remoção da imagem antiga

O professor também remove uma imagem que não será utilizada na nova tela.

O objetivo é começar a construção apenas com os elementos necessários.

A tela será composta basicamente por:

Plaintext

```
Logo
  ↓
Número da sorte
  ↓
Botão
```

## 4. 🖌️ Exportando a logo do protótipo

O próximo passo acontece no protótipo.

O professor precisa pegar a imagem da logo e levá-la para o projeto.

Ele orienta que a imagem seja exportada no formato:

- **SVG**
    

A justificativa dada na aula é que o formato é adequado para preservar a resolução da imagem.

A imagem é exportada e colocada em uma pasta de materiais:

Plaintext

```
Materiais
└── Seção 3
    └── Imagens
        └── Logo Green
```

## 5. 📂 Copiando a imagem para o projeto

Depois de exportar a logo, o professor volta para o projeto e copia a imagem para os arquivos do aplicativo.

Ele interrompe a execução do projeto antes de fazer alterações nos arquivos.

A sequência demonstrada é:

Plaintext

```
Parar execução
     ↓
Excluir arquivo antigo
     ↓
Copiar nova logo
     ↓
Colar no projeto
     ↓
Executar novamente
```

Ele destaca que é interessante fazer uma exportação completa do protótipo quando o design estiver pronto e, depois, copiar os recursos para o projeto.

Isso evita ficar reiniciando e alterando recursos repetidamente durante o desenvolvimento.

## 6. 🖥️ Organização da área de trabalho

O professor reorganiza as janelas para conseguir acompanhar simultaneamente:

- o código;
    
- o protótipo;
    
- a tela do aplicativo.
    

A intenção é comparar visualmente:

Plaintext

```
Protótipo
    ↕
Aplicativo
```

Essa comparação será utilizada durante toda a construção.

## 7. 🏗️ Criando a estrutura da tela

Agora começa efetivamente a implementação.

O professor lembra que está utilizando:

XML

```
<VerticalStackLayout>
```

O `VerticalStackLayout` organiza os elementos um abaixo do outro.

Portanto, a estrutura geral será:

Plaintext

```
VerticalStackLayout
│
├── Logo
│
├── Número da sorte
│
└── Botão
```

Essa estrutura corresponde diretamente à disposição visual do protótipo.

## 8. 🖼️ Adicionando a imagem

O professor cria um componente de imagem.

A ideia é utilizar a propriedade:

XML

```
Source
```

para indicar qual arquivo deverá ser apresentado.

Conceitualmente:

XML

```
<Image
    Source="logo_green.png" />
```

O `Source` informa qual imagem será carregada pelo componente.

## 9. ⚠️ Problema: a imagem ficou gigante

Assim que a imagem é adicionada, o professor observa um problema:

> A logo ficou esticada/ocupando uma área muito grande.

Isso acontece porque o componente de imagem está utilizando o espaço disponível.

Visualmente:

Plaintext

```
┌──────────────────────┐
│                      │
│       IMAGEM         │
│       GRANDE         │
│                      │
└──────────────────────┘
```

Mas o protótipo possui uma logo pequena.

Portanto, será necessário definir suas dimensões.

## 10. 📏 Definindo largura e altura

O professor consulta o tamanho da imagem no protótipo.

Ele identifica aproximadamente:

- **Largura:** 74
    
- **Altura:** 115
    

Então utiliza propriedades para definir essas dimensões.

A ideia é:



```XML
<Image
    Source="logo_green.png"
    WidthRequest="74"
    HeightRequest="115" />
```

### O que cada propriedade significa?

|**Propriedade**|**Função**|
|---|---|
|`WidthRequest`|Define a largura desejada|
|`HeightRequest`|Define a altura desejada|

O professor observa que, ao definir a largura, a imagem consegue manter sua proporção, mas ele mantém os valores definidos para obter o tamanho desejado.

## 11. 📝 Criando o número da sorte

Depois da imagem, o próximo elemento é o texto:

- **Número da sorte**
    

O professor utiliza uma `Label` para representar esse texto.

A estrutura passa a ser:

Plaintext

```
VerticalStackLayout
│
├── Image
│
└── Label
```

## 12. 🔘 Criando o botão

Depois do número da sorte, é criado um botão.

O texto do botão será:

- **Gerar o número da sorte**
    

Portanto:



```
VerticalStackLayout
│
├── Image
│
├── Label
│
└── Button
```

Essa é a estrutura básica da primeira tela.

## 13. 🎨 Agora começa a estilização

Depois de criar os componentes, o professor explica que ainda falta:

- posicionamento;
    
- espaçamento;
    
- cores;
    
- estilos;
    
- aparência do botão.
    

Ele então apresenta o arquivo de estilos do projeto.

## 14. 🎨 Arquivo de estilos

O professor mostra que o projeto possui uma estrutura de recursos onde estão definidos:

- cores;
    
- estilos;
    
- configurações dos componentes.
    

A ideia é centralizar determinadas configurações.

Por exemplo:

Plaintext

```
Resources
└── Styles
    ├── Cores
    └── Estilos
```

Isso permite definir uma aparência padrão para determinados componentes.

## 15. 🌈 Cores globais × cores específicas

Aqui aparece uma distinção muito importante.

O professor percebe que o número da sorte deve ser verde.

Mas os outros textos da aplicação continuarão pretos.

Por isso, ele decide não alterar o estilo global da `Label`.

Em vez disso, modifica somente aquela `Label`.

### Comparação

|**Situação**|**Onde configurar?**|
|---|---|
|Todas as `Label` devem ser verdes|Estilo global|
|Somente uma `Label` deve ser verde|Na própria `Label`|
|Todos os botões devem seguir o mesmo padrão|Estilo global do botão|
|Apenas um botão deve ser diferente|No próprio `Button`|

Essa distinção é fundamental para entender quando utilizar estilos globais e quando utilizar propriedades diretamente no componente.

## 16. 🟢 Alterando o TextColor

O professor utiliza a propriedade:

XML

```
TextColor
```

para modificar a cor do texto do número da sorte.

A cor utilizada é:

- `#00AB37`
    

Conceitualmente:

XML

```
<Label
    Text="Número da sorte"
    TextColor="#00AB37" />
```

Assim, somente aquele texto fica verde.

## 17. 🤔 Por que não alterar todas as Labels?

O professor explica a razão:

- As demais `Label` deverão permanecer com a aparência padrão.
    
- Além disso, existe a possibilidade de haver outras telas no aplicativo.
    
- Portanto, alterar o estilo global poderia provocar uma mudança indesejada em vários elementos.
    

> [!TIP] Regra importante
> 
> Se a alteração é específica de um componente, pode ser melhor configurar diretamente nele.
> 
> Se a alteração deve ser compartilhada por vários componentes, faz sentido colocá-la em um estilo.

## 18. 🔘 Estilizando o botão

Agora o professor passa para o botão.

Ele observa que o botão precisa:

- ser verde;
    
- possuir cantos arredondados;
    
- ter aparência semelhante ao protótipo.
    

Aqui surge uma decisão importante.

Como os botões são componentes utilizados frequentemente no aplicativo, o professor considera mais interessante modificar o estilo global do botão, em vez de configurar cada botão individualmente.

## 19. 🎨 Cor primária

O professor encontra no arquivo de estilos a configuração da cor primária.

Ela estava utilizando uma cor roxa.

Ele substitui pela cor verde:

- `#00AB37`
    

Como o estilo do botão já utiliza a cor primária, a alteração é automaticamente refletida no botão.

A cadeia é:

Plaintext

```
Cor primária
      ↓
Estilo do botão
      ↓
Button
      ↓
Botão fica verde
```

Essa é uma das vantagens de utilizar estilos centralizados.

## 20. 🌙 Tema claro e tema escuro

O professor observa que o estilo do botão já possui configurações relacionadas ao tema do sistema operacional.

A ideia apresentada é que determinadas cores podem mudar conforme o sistema esteja utilizando:

- `Light Mode`
    
- `Dark Mode`
    

O professor não aprofunda esse mecanismo nesta aula; ele apenas mostra que o estilo já possui essa configuração.

## 21. 🔵 CornerRadius

O botão possui cantos arredondados.

O professor modifica a propriedade:

XML

```
CornerRadius
```

Essa propriedade representa o raio utilizado para arredondar os cantos.

Ele começa utilizando:

- `20`
    

Conceitualmente:

XML

```
<Button
    CornerRadius="20" />
```

Quanto maior o valor, mais arredondados ficam os cantos.

## 22. 📐 Testando valores diferentes

O professor faz testes com valores maiores: `23`, `25`, `50`, `100`.

Quando o valor fica muito grande, o botão começa a ficar excessivamente arredondado.

Visualmente:

**CornerRadius pequeno:**

Plaintext

```
┌──────────────┐
│              │
└──────────────┘
```

**CornerRadius grande:**

Plaintext

```
╭──────────────╮
│              │
╰──────────────╯
```

**CornerRadius muito grande:**

Plaintext

```
╭──────────────╮
│              │
╰──────────────╯
```

O professor conclui que aproximadamente **23** produz uma aparência mais próxima do protótipo.

## 23. ↔️ Botão ocupando toda a largura

Depois da aparência, vem o posicionamento.

O professor percebe que o botão está ocupando toda a largura disponível:

Plaintext

```
┌─────────────────────────┐
│                         │
│ ┌─────────────────────┐ │
│ │ GERAR NÚMERO        │ │
│ └─────────────────────┘ │
│                         │
└─────────────────────────┘
```

Mas o protótipo possui um botão menor e centralizado.

Então ele altera a configuração de alinhamento horizontal.

## 24. 🎯 HorizontalOptions

O professor utiliza `HorizontalOptions` para modificar o comportamento horizontal do componente.

A intenção é fazer com que o botão não ocupe toda a largura disponível e fique centralizado.

Conceitualmente:

XML

```
<Button
    HorizontalOptions="Center" />
```

Resultado:

Plaintext

```
┌─────────────────────────┐
│                         │
│      ┌───────────┐      │
│      │   BOTÃO   │      │
│      └───────────┘      │
│                         │
└─────────────────────────┘
```

## 25. 📦 Margin no botão

Depois do alinhamento, o professor trabalha com `Margin`.

A margem é utilizada para criar os espaços entre os componentes.

Ele ajusta os valores até encontrar uma aparência próxima do protótipo.

Na demonstração, ele testa valores como `30`, `15` e `12`, até chegar a uma configuração visual considerada adequada.

## 26. 🖼️ Espaçamento da logo

Agora é necessário separar visualmente os componentes.

O professor aplica margem na imagem.

A ideia é colocar a logo mais afastada da parte superior.

Ele inicialmente experimenta `Margin = 50`.

Mas lembra de uma regra importante da aula anterior:

> Quando são utilizados dois valores, eles representam os valores horizontal e vertical.

Portanto, `50,50` produziria:

- Horizontal = 50
    
- Vertical = 50
    

Mas ele não deseja criar margem horizontal.

Então ajusta para algo equivalente a `0,50`:

- **Horizontal** = 0
    
- **Vertical** = 50
    

## 27. 📊 Relembrando Margin com dois valores

Essa parte conecta diretamente com a aula anterior.

|**Sintaxe**|**Horizontal**|**Vertical**|
|---|---|---|
|`50`|50|50|
|`0,50`|0|50|
|`20,120`|20|120|

A aula utiliza esse conceito para posicionar os elementos da tela.

## 28. 📝 Margem da Label

Depois da imagem, o professor trabalha o espaçamento do número da sorte.

Ele adiciona uma margem à `Label`.

A ideia é criar:

Plaintext

```
Logo
  ↓
espaço
  ↓
Número da sorte
  ↓
espaço
  ↓
Botão
```

Ele experimenta valores até chegar a uma distância visualmente adequada.

Na demonstração, chega a utilizar uma margem com valor vertical bastante maior na região abaixo do texto, chegando a aproximadamente **120**.

O objetivo não é decorar esse número, mas perceber como a margem controla a distância entre os elementos.

## 29. 🧩 Quem deve receber a Margin?

O professor faz uma observação importante.

A distância entre dois componentes pode ser obtida configurando a margem de um ou de outro componente.

Por exemplo:

Plaintext

```
Imagem
   ↓
Label
```

Pode-se pensar na margem:

- `Imagem → Margin`
    
- ou: `Label → Margin`
    

O professor opta por deixar a imagem mais simples e utilizar a margem na `Label`.

A ideia é que existem diferentes maneiras de organizar o espaçamento, e você precisa escolher uma estratégia consistente.

## 30. 📱 Problema: diferentes tamanhos de tela

Depois de posicionar os componentes, o professor aumenta e diminui a tela.

Ele percebe que as distâncias permanecem.

Isso significa que os elementos não estão simplesmente sendo posicionados por coordenadas fixas.

A estrutura está trabalhando com o sistema de layout do MAUI.

## 31. 🎯 Centralizando o conteúdo

O professor então apresenta uma solução melhor:

> Centralizar o conteúdo dentro do layout.

Primeiro ele coloca novamente uma cor no layout para conseguir visualizar sua área.

Como explicado anteriormente:

> O layout ocupa todo o espaço disponível.

Então:

Plaintext

```
┌──────────────────────────────┐
│                              │
│           LAYOUT             │
│                              │
│                              │
└──────────────────────────────┘
```

Os componentes ficam dentro dessa área.

## 32. ↔️ Centralização horizontal

O professor configura `HorizontalOptions` para centralizar os elementos:

XML

```
HorizontalOptions="Center"
```

Assim, os componentes deixam de ficar presos a uma extremidade.

## 33. ↕️ Centralização vertical

Depois ele faz o mesmo para a direção vertical.

Utiliza `VerticalOptions` para centralizar o conteúdo verticalmente.

Conceitualmente:

XML

```
<VerticalStackLayout
    HorizontalOptions="Center"
    VerticalOptions="Center">
```

A intenção é:

Plaintext

```
       ┌───────────────────────┐
       │                       │
       │       ┌───────┐       │
       │       │ LOGO  │       │
       │       └───────┘       │
       │          ↓            │
       │       LABEL           │
       │          ↓            │
       │       BOTÃO           │
       │                       │
       └───────────────────────┘
```

Agora a estrutura inteira fica centralizada.

## 34. 🔄 Testando diferentes tamanhos

O professor reduz e aumenta a tela novamente.

O resultado desejado é que o conteúdo continue centralizado:

**Tela grande:**

Plaintext

```
┌───────────────────────────┐
│                           │
│       LOGO                │
│       LABEL               │
│       BOTÃO               │
│                           │
└───────────────────────────┘
```

**Tela menor:**

Plaintext

```
┌───────────────────┐
│                   │
│      LOGO         │
│      LABEL        │
│      BOTÃO        │
│                   │
└───────────────────┘
```

A posição se adapta ao espaço disponível.

## 35. 🧹 Removendo as cores de teste

Depois de confirmar que o posicionamento está funcionando, o professor remove novamente a cor utilizada no layout.

Essa cor havia sido utilizada apenas para visualizar a área ocupada pelo layout.

A tela volta a ficar limpa.

## 36. 🔧 Ajuste final da margem da logo

Como o layout agora está sendo centralizado, algumas margens utilizadas anteriormente deixam de ser necessárias.

O professor então zera as margens da logo:

- `Margin = 0`
    

Isso permite que a centralização do layout determine melhor a posição do conteúdo.

## 37. 🧠 Estrutura final da tela

Ao final da aula, temos conceitualmente:

Plaintext

```
ContentPage
│
└── VerticalStackLayout
    │
    ├── Image
    │    └── Logo Green
    │
    ├── Label
    │    └── Número da sorte
    │
    └── Button
         └── Gerar o número da sorte
```

E o layout é centralizado:

- `HorizontalOptions → Center`
    
- `VerticalOptions → Center`
    

## 38. 📋 Tabela dos principais componentes utilizados

|**Elemento**|**Função na tela**|**Configuração trabalhada**|
|---|---|---|
|`VerticalStackLayout`|Organizar elementos verticalmente|Centralização|
|`Image`|Exibir a logo|`Source`, largura, altura, margem|
|`Label`|Exibir o número da sorte|`TextColor`, margem|
|`Button`|Gerar o número da sorte|Cor, margem, `CornerRadius`, alinhamento|
|**Estilo**|Definir aparência reutilizável|Cores e propriedades|
|**Cor primária**|Cor compartilhada pelo projeto|`#00AB37`|

## 39. 🎨 Tabela de propriedades trabalhadas

|**Propriedade**|**O que controla**|**Utilização na aula**|
|---|---|---|
|`Source`|Arquivo exibido pela imagem|Logo|
|`WidthRequest`|Largura desejada|Dimensão da logo|
|`HeightRequest`|Altura desejada|Dimensão da logo|
|`TextColor`|Cor do texto|Número da sorte|
|`BackgroundColor`|Fundo do componente|Utilizado para testes|
|`CornerRadius`|Arredondamento dos cantos|Botão|
|`HorizontalOptions`|Alinhamento horizontal|Centralizar|
|`VerticalOptions`|Alinhamento vertical|Centralizar|
|`Margin`|Espaçamento externo|Separação dos elementos|

## 40. 🆚 Estilo global × propriedade local

Essa é uma das ideias mais importantes da aula.

|**Necessidade**|**Melhor abordagem apresentada**|
|---|---|
|Alterar apenas o número da sorte|`TextColor` diretamente na `Label`|
|Alterar todos os botões|Estilo do `Button`|
|Alterar a cor primária do aplicativo|Recurso de cores|
|Alterar o arredondamento padrão dos botões|Estilo do botão|
|Criar uma distância específica|`Margin` do componente|

### Regra prática

Plaintext

```
Mudança específica
        ↓
Componente

Mudança reutilizável
        ↓
Estilo
```

## 41. ⚠️ Pegadinhas importantes da aula

1. **`BackgroundColor` não serve para posicionar:** Ele apenas altera a cor de fundo. Na aula, as cores são utilizadas principalmente para visualizar os limites dos componentes.
    
2. **`Source` não define o tamanho da imagem:** `Source="logo_green.png"` indica qual imagem carregar. O tamanho é tratado por propriedades como `WidthRequest` e `HeightRequest`.
    
3. **A imagem pode ocupar muito espaço:** Adicionar uma imagem não significa que ela automaticamente terá o tamanho do protótipo. É necessário ajustar suas dimensões.
    
4. **`Margin="50"` não significa "50 para cima":** Um único valor é aplicado a todos os lados. Para controlar horizontal e vertical separadamente, utiliza-se a estrutura com dois valores.
    
5. **Dois valores não significam "esquerda e cima":** Na lógica apresentada, `30,20` representa `30` (horizontal) e `20` (vertical).
    
6. **`CornerRadius` muito alto pode deixar o botão excessivamente arredondado:** O professor testa valores como `50` e `100` para demonstrar esse efeito.
    
7. **Centralizar o botão não é o mesmo que centralizar o layout inteiro:** São configurações aplicadas em níveis diferentes:
    

Plaintext

```
Button
└── HorizontalOptions

VerticalStackLayout
├── HorizontalOptions
└── VerticalOptions
```

## 42. 👨‍🏫 Passo a passo completo do professor

A sequência prática da aula pode ser memorizada assim:

1. **Preparou o projeto:** abriu o protótipo, comparou a tela e identificou as modificações necessárias.
    
2. **Limpou a interface:** removeu cores de teste, removeu imagem desnecessária e deixou a base branca.
    
3. **Exportou a logo:** selecionou a logo no protótipo, exportou no formato SVG e colocou na pasta de imagens.
    
4. **Copiou a logo para o projeto:** `Materiais` → `Seção 3` → `Imagens` → `Logo` → `Projeto`.
    
5. **Executou novamente o projeto:** confirmou que o recurso estava disponível.
    
6. **Criou a imagem:** `<Image Source="..."/>`.
    
7. **Corrigiu o tamanho:** utilizou largura e altura para aproximar a logo do protótipo.
    
8. **Criou o número da sorte:** utilizou uma `<Label>`.
    
9. **Criou o botão:** "Gerar o número da sorte".
    
10. **Configurou a cor da Label:** aplicou `#00AB37` somente ao número da sorte.
    
11. **Alterou a cor primária:** modificou o recurso global para verde.
    
12. **Estilizou o botão:** configurou cor, arredondamento e aparência.
    
13. **Configurou CornerRadius:** testou valores até encontrar aproximadamente `23`.
    
14. **Centralizou o botão:** utilizou `HorizontalOptions`.
    
15. **Ajustou as margens:** utilizou `Margin` para criar as distâncias entre `Logo` → `Label` → `Button`.
    
16. **Centralizou o layout:** configurou `HorizontalOptions` e `VerticalOptions`.
    
17. **Testou diferentes tamanhos:** reduziu e aumentou a tela para verificar o comportamento.
    
18. **Removeu as cores de teste:** deixou a interface com a aparência final.
    
19. **Zerou margens desnecessárias:** ajustou a logo depois da centralização.
    
20. **Finalizou a primeira tela:** o resultado é uma interface organizada, centralizada e visualmente próxima do protótipo.
    

## 🧠 Resumo de revisão

A aula representa a passagem de:

Plaintext

```
PROTÓTIPO
   ↓
IMPLEMENTAÇÃO
```

A tela final possui:

Plaintext

```
        LOGO
          ↓
   NÚMERO DA SORTE
          ↓
      [ BOTÃO ]
```

### Conceitos mais importantes

| **Para lembrar**             | **Conceito**                     |
| ---------------------------- | -------------------------------- |
| 🖼️ Imagem                   | `Source`                         |
| 📏 Tamanho                   | `WidthRequest` / `HeightRequest` |
| 🟢 Cor do texto              | `TextColor`                      |
| 🟩 Cor de fundo              | `BackgroundColor`                |
| 🔘 Cantos arredondados       | `CornerRadius`                   |
| ↔️ Alinhamento horizontal    | `HorizontalOptions`              |
| ↕️ Alinhamento vertical      | `VerticalOptions`                |
| 📐 Espaçamento               | `Margin`                         |
| 🎨 Configuração reutilizável | Estilo                           |
| 🎯 Um único componente       | Propriedade local                |
| 🎯 Vários componentes        | Estilo global                    |

### A ideia central

Primeiro criamos a estrutura da tela; depois configuramos aparência; depois ajustamos espaçamentos e, finalmente, usamos as opções de alinhamento para tornar a interface adaptável ao espaço disponível.

Isso encerra a construção da primeira tela do aplicativo, deixando a base pronta para a continuação do desenvolvimento na próxima aula.

## Notas
- #### [[exemplo de código tela inicial]]
