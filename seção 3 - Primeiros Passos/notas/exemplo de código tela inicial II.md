
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
                Source: nome do arquivo localizado em Resources/Images
            -->
            <Image
                Source="logo.jpg"
                WidthRequest="74"
                HeightRequest="115"
                HorizontalOptions="Center"
                Margin="0" />

            <!--
                2. NÚMERO DA SORTE
                Este elemento pertence à primeira tela.
                Posteriormente poderá ser controlado com IsVisible.
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
                HorizontalStackLayout coloca os números lado a lado.
            -->
            <HorizontalStackLayout
                HorizontalOptions="Center"
                Spacing="10"
                Margin="0,70,0,70">

                <Label
                    Text="01"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="05"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="12"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="18"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="32"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="47"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

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


```
ContentPage
│
└── ScrollView
    │
    └── VerticalStackLayout
        │
        ├── Image
        ├── Label
        ├── Button
        ├── Label
        ├── HorizontalStackLayout
        │   ├── Label
        │   ├── Label
        │   ├── Label
        │   ├── Label
        │   ├── Label
        │   └── Label
        ├── Label
        └── Button
```

