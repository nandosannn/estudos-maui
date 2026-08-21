
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNumeroDaSorte.MainPage"
    Title="Número da Sorte">

    <ScrollView>

        <VerticalStackLayout
            HorizontalOptions="Center"
            VerticalOptions="Center"
            Padding="30,0"
            Spacing="25">

            <!--
                1. LOGO
            -->
            <Image
                Source="logo.jpg"
                WidthRequest="74"
                HeightRequest="115"
                HorizontalOptions="Center"
                Margin="0" />

            <!--
                2. NÚMERO DA SORTE
            -->
            <Label
                Text="Número da sorte"
                TextColor="#00AB37"
                FontSize="22"
                FontAttributes="Bold"
                HorizontalOptions="Center"
                Margin="0,30,0,60" />

            <!--
                3. BOTÃO DA PRIMEIRA TELA
            -->
            <Button
                Text="Gerar o número da sorte"
                HorizontalOptions="Center"
                CornerRadius="23"
                Padding="20,12" />

            <!-- ================================================= -->
            <!-- SEGUNDA TELA                                      -->
            <!-- ================================================= -->

            <!--
                Título da segunda tela
            -->
            <Label
                Text="Número da Sorte:"
                HorizontalOptions="Center"
                Margin="0,20,0,0" />

            <!--
                Números sorteados
            -->
            <HorizontalStackLayout
                HorizontalOptions="Center"
                Spacing="10"
                Margin="0,70,0,70">

                <!-- Número 01 -->
                <Border
                    Stroke="#00AB37"
                    StrokeShape="RoundRectangle 8"
                    Padding="10,5">

                    <Label
                        Text="01"
                        FontSize="24"
                        FontFamily="OpenSansMedium"
                        TextColor="#00AB37" />

                </Border>

                <!-- Número 05 -->
                <Border
                    Stroke="#00AB37"
                    StrokeShape="RoundRectangle 8"
                    Padding="10,5">

                    <Label
                        Text="05"
                        FontSize="24"
                        FontFamily="OpenSansMedium"
                        TextColor="#00AB37" />

                </Border>

                <!-- Número 12 -->
                <Border
                    Stroke="#00AB37"
                    StrokeShape="RoundRectangle 8"
                    Padding="10,5">

                    <Label
                        Text="12"
                        FontSize="24"
                        FontFamily="OpenSansMedium"
                        TextColor="#00AB37" />

                </Border>

                <!-- Número 18 -->
                <Border
                    Stroke="#00AB37"
                    StrokeShape="RoundRectangle 8"
                    Padding="10,5">

                    <Label
                        Text="18"
                        FontSize="24"
                        FontFamily="OpenSansMedium"
                        TextColor="#00AB37" />

                </Border>

                <!-- Número 32 -->
                <Border
                    Stroke="#00AB37"
                    StrokeShape="RoundRectangle 8"
                    Padding="10,5">

                    <Label
                        Text="32"
                        FontSize="24"
                        FontFamily="OpenSansMedium"
                        TextColor="#00AB37" />

                </Border>

                <!-- Número 47 -->
                <Border
                    Stroke="#00AB37"
                    StrokeShape="RoundRectangle 8"
                    Padding="10,5">

                    <Label
                        Text="47"
                        FontSize="24"
                        FontFamily="OpenSansMedium"
                        TextColor="#00AB37" />

                </Border>

            </HorizontalStackLayout>

            <!--
                Mensagem da segunda tela
            -->
            <Label
                Text="Boa sorte!"
                HorizontalOptions="Center"
                Margin="0,0,0,50" />

            <!--
                Botão da segunda tela
            -->
            <Button
                Text="Gerar número da sorte"
                HorizontalOptions="Center"
                CornerRadius="23"
                Padding="20,12" />

        </VerticalStackLayout>

    </ScrollView>

</ContentPage>
```

### O que cada propriedade do `Border` está fazendo?

|Propriedade|Exemplo|Função|
|---|---|---|
|`Border`|`<Border>`|Cria um contêiner com borda|
|`Stroke`|`Stroke="#00AB37"`|Define a cor da borda|
|`StrokeShape`|`StrokeShape="RoundRectangle 8"`|Define a forma da borda como retângulo arredondado|
|`Padding`|`Padding="10,5"`|Cria espaço **dentro** do `Border`|
|`Label`|`<Label Text="01" />`|Exibe o número|

### Uma diferença importante

Agora você tem **dois tipos de espaçamento**:

```xml
<HorizontalStackLayout

    Spacing="10">
```

Esse `Spacing` controla o espaço **entre os Borders**:
```
┌────┐  ← 10 →  ┌────┐  ← 10 →  ┌────┐

│ 01 │          │ 05 │          │ 12 │

└────┘          └────┘          └────┘
```
Enquanto:

```xml
<Border

    Padding="10,5">
```

controla o espaço **dentro de cada Border**:

```
┌────────┐

│  01    │

└────────┘

  ↑    ↑

 Padding
```

Ou seja:

**`Spacing` → espaço entre os números**

**`Padding` → espaço entre o número e a borda**

**`Margin` → espaço externo de um elemento**