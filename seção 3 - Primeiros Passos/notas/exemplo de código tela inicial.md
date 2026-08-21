Aqui está o código completo organizado exatamente como visto na aula, dividindo o que é **estilo global** (cores e botões) do que é a **tela em si (XAML)**, além do passo a passo prático para rodar no Visual Studio.

### 1. Código da Tela Principal (`MainPage.xaml`)

Substitua todo o conteúdo do seu arquivo `MainPage.xaml` por:


```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNumeroDaSorte.MainPage"
    Title="Número da Sorte">

    <!-- 
        VerticalStackLayout centralizado na tela inteira 
        (tanto na horizontal quanto na vertical)
    -->
    <VerticalStackLayout
        HorizontalOptions="Center"
        VerticalOptions="Center">

        <!-- 
            1. LOGO:
            - Source: nome do arquivo na pasta Resources/Images
            - WidthRequest / HeightRequest: travando o tamanho exato da logo
            - Margin: 0 pois o alinhamento é controlado pelo layout pai
        -->
        <Image
            Source="logo.jpg."
            WidthRequest="74"
            HeightRequest="115"
            Margin="0" />

        <!-- 
            2. NÚMERO DA SORTE:
            - TextColor: alterado localmente (#00AB37) para não afetar outras labels
            - Margin: '0, 40, 0, 80' -> (Esquerda, Cima, Direita, Baixo)
              Cria o espaçamento entre a Logo e o Botão
        -->
        <Label
            Text="Número da sorte"
            TextColor="#00AB37"
            FontSize="22"
            FontAttributes="Bold"
            HorizontalOptions="Center"
            Margin="0,30,0,60" />

        <!-- 
            3. BOTÃO:
            - Text: texto da ação
            - HorizontalOptions="Center": não estica 100% da tela, fica com largura proporcional
            - CornerRadius: cantos arredondados (23)
            - As cores de fundo e texto herdam do estilo global (Primary / White)
        -->
        <Button
            Text="Gerar o número da sorte"
            HorizontalOptions="Center"
            CornerRadius="23"
            Padding="20,12" />

    </VerticalStackLayout>

</ContentPage>
```

### 2. Configurações Globais de Estilo e Cores

#### A. Alterar a Cor Primária (`Resources/Styles/Colors.xaml`)

No arquivo `Colors.xaml`, localize a chave `Primary` e substitua a cor padrão (roxa) pelo verde:



```XML
<!-- Troque o valor da Primary para o verde da aplicação -->
<Color x:Key="Primary">#00AB37</Color>
```

#### B. (Opcional) Ajustar o Estilo Global do Botão (`Resources/Styles/Styles.xaml`)

Se você preferir definir o `CornerRadius` para todos os botões do app de forma global, localize `<Style TargetType="Button">` em `Styles.xaml` e adicione/ajuste a propriedade:



```XML
<Style TargetType="Button">
    <Setter Property="TextColor" Value="{AppThemeBinding Light={StaticResource White}, Dark={StaticResource PrimaryDarkText}}" />
    <Setter Property="BackgroundColor" Value="{AppThemeBinding Light={StaticResource Primary}, Dark={StaticResource PrimaryDark}}" />
    <Setter Property="CornerRadius" Value="23" />
</Style>
```

### 3. Passo a Passo para Adicionar e Executar

1. **Parar a execução:** Se o projeto estiver rodando, pare a depuração clicando no botão vermelho de _Stop_ (ou `Shift + F5`).
    
2. **Adicionar a imagem SVG/PNG:**
    
    - No Gerenciador de Soluções (_Solution Explorer_), abra a pasta `Resources` -> `Images`.
        
    - Arraste ou copie a imagem `logo_green.svg` (ou `.png`) para dentro dessa pasta.
        
    - Clique com o botão direito na imagem -> **Propriedades** -> verifique se a _Build Action_ (_Ação de Compilação_) está marcada como **MauiImage**.
        
3. **Atualizar o arquivo `Colors.xaml`:**
    
    - Abra `Resources/Styles/Colors.xaml`.
        
    - Atualize a cor `<Color x:Key="Primary">#00AB37</Color>`.
        
4. **Atualizar o `MainPage.xaml`:**
    
    - Abra `MainPage.xaml` e cole o código da seção 1.
        
    - Se o nome do arquivo da logo for diferente, ajuste a propriedade `Source="seu_arquivo.svg"`.
        
5. **Executar a aplicação:**
    
    - Pressione **F5** (ou o botão verde _Windows Machine_ / Emulador Android).
        
    - Redimensione a janela para testar como o `VerticalStackLayout` com `Center` se adapta a qualquer resolução mantendo o conteúdo centralizado.