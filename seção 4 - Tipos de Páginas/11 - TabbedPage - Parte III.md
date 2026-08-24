## 1. Diferença entre Windows e Android

A mesma propriedade pode apresentar resultados diferentes em cada sistema operacional.

|Conceito|Windows|Android|
|---|---|---|
|`SelectedTabColor`|Pode alterar o fundo/indicador|Pode alterar elementos da aba|
|`UnselectedTabColor`|Pode alterar o fundo das abas|Pode ter comportamento diferente|
|`BarTextColor`|Pode funcionar normalmente|Pode deixar todos os textos da mesma cor|
|Aparência|Baseada no componente do Windows|Baseada no componente do Android|

**Exemplo:**

```
<TabbedPage
    SelectedTabColor="Purple"
    UnselectedTabColor="Gray">
```

O resultado visual pode ser diferente no Windows e no Android.

---

## 2. `SelectedTabColor` e `UnselectedTabColor`

Servem para diferenciar a aba selecionada das demais.

|Propriedade|Função|
|---|---|
|`SelectedTabColor`|Cor/aparência da aba selecionada|
|`UnselectedTabColor`|Cor/aparência das abas não selecionadas|

Exemplo:

```
<TabbedPage
    SelectedTabColor="Purple"
    UnselectedTabColor="Gray">
```

Visualmente:

```
Página 1 | Página 2 | Página 3
  Gray      Purple      Gray
```

---

## 3. `BarTextColor`

Define a cor dos textos das abas.

```
BarTextColor="White"
```

Porém, no Android, a aula recomenda **cuidado com essa propriedade**, porque ela pode deixar todos os textos das abas com a mesma cor.

```
Página 1 | Página 2 | Página 3
  Branco    Branco     Branco
```

Isso pode dificultar a identificação da aba selecionada.

---

## 4. Cores do Android

O Android possui recursos próprios para controlar cores.

|Recurso|Função|
|---|---|
|`ColorPrimary`|Cor principal do aplicativo|
|`ColorPrimaryDark`|Variação mais escura|
|`ColorAccent`|Cor de destaque|

Esses recursos são úteis quando precisamos adaptar a aparência especificamente ao Android.

---

## 5. Ícones nas abas

Podemos adicionar um ícone para cada página utilizando `IconImageSource`.

```
<ContentPage
    Title="Página 1"
    IconImageSource="1.png">
```

Exemplo:

```
 ① Página 1    ② Página 2    ③ Página 3
```

Os ícones ajudam o usuário a identificar rapidamente a função de cada aba.

---

## 6. SVG

A aula utiliza imagens no formato `.svg`.

```
Resources
└── Images
    ├── 1.svg
    ├── 2.svg
    └── 3.svg
```

O SVG é um formato vetorial, adequado para trabalhar com diferentes tamanhos e densidades de tela.

No `IconImageSource`, pode ser utilizado o recurso processado pelo MAUI, por exemplo:

```
IconImageSource="1.png"
```

---

## 7. Abas na parte inferior

No Android, podemos configurar as abas para ficarem na parte inferior.

### Padrão

```
┌──────────────────────┐
│ Página 1 | Página 2 │
├──────────────────────┤
│                      │
│       Conteúdo       │
│                      │
└──────────────────────┘
```

### Configurado para baixo

```
┌──────────────────────┐
│                      │
│       Conteúdo       │
│                      │
├──────────────────────┤
│ Página 1 | Página 2 │
└──────────────────────┘
```

Para isso, utilizamos uma configuração específica do Android relacionada ao `TabbedPage` e ao posicionamento da barra.

---

## 8. Recursos específicos de plataforma

O .NET MAUI permite acessar recursos específicos de cada sistema.

```
Código MAUI
     │
     ├── Windows
     ├── Android
     └── iOS
```

No XAML, podemos importar um namespace específico do Android e utilizar propriedades que não são necessariamente compartilhadas entre todas as plataformas.

Isso é importante quando precisamos de uma aparência específica para determinado sistema.

---

## 9. Hot Reload x Reinicialização

|Recurso|Utilização|
|---|---|
|**Hot Reload**|Atualiza alterações compatíveis rapidamente|
|**Reiniciar aplicativo**|Útil quando o Hot Reload não consegue aplicar a alteração|
|**Recompilar projeto**|Necessário em alterações mais estruturais|

Alterações nativas do Android podem exigir uma reinicialização completa do aplicativo.

---

## 10. Combinação das páginas

Um dos conceitos mais importantes no final da aula é que os diferentes tipos de páginas podem ser **combinados**.

|Página|Pode ser combinada?|
|---|---|
|`ContentPage`|Sim|
|`NavigationPage`|Sim|
|`FlyoutPage`|Sim|
|`TabbedPage`|Sim|

Por exemplo:

```
TabbedPage
│
├── NavigationPage
│      └── Página 1
│
├── NavigationPage
│      └── Página 2
│
└── FlyoutPage
       ├── Menu
       └── Detail
```

Isso permite criar aplicativos mais complexos, combinando **abas, navegação e menus laterais**.

---

## Resumo para memorizar

|Assunto|Ideia principal|
|---|---|
|`SelectedTabColor`|Personaliza a aba selecionada|
|`UnselectedTabColor`|Personaliza as abas não selecionadas|
|`BarTextColor`|Altera a cor do texto das abas|
|`IconImageSource`|Adiciona ícones às abas|
|SVG|Formato vetorial para imagens|
|Recursos Android|Permitem personalização específica do Android|
|Barra inferior|Permite adaptar a navegação ao padrão mobile|
|Hot Reload|Atualiza alterações sem recompilar tudo|
|Plataformas|Podem apresentar comportamentos visuais diferentes|
|Combinação de páginas|`TabbedPage`, `NavigationPage` e `FlyoutPage` podem trabalhar juntas|

**Em resumo:** a aula ensina que a `TabbedPage` não precisa ter a mesma aparência em todas as plataformas. Podemos **personalizar cores, textos, ícones e posição das abas**, além de utilizar recursos específicos do Android e combinar diferentes modelos de navegação.