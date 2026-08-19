
No **Android**, os ícones seguem o padrão de **Adaptive Icons** (introduzido a partir do Android 8.0 / API 26). O sistema aplica máscaras automáticas (círculos, esquilos, cantos arredondados) sobre o ícone do aplicativo. Por conta disso, artes em tela cheia acabam sofrendo cortes laterais ou zoom indesejado, exigindo uma margem de segurança (_safe zone_).

### Organização e Estrutura de Pastas Geradas no Android

Diferente do Windows (onde todos os recursos ficam juntos), o compilador do .NET MAUI (**Resizetizer**) separa os recursos nativos nas seguintes pastas dentro de `obj/Debug/netX.0-android/resizetizer/r/`:

|**Pasta Nativa Android**|**Conteúdo Armazenado**|**Exemplo de Arquivo**|
|---|---|---|
|**`mipmap-{densidade}`**|Ícones do aplicativo divididos em camadas de background e foreground.|`appicon_background.png`, `appicon_foreground.png`|
|**`drawable-{densidade}`**|Imagens comuns da interface e ilustrações (como a logo do bot).|`dotnet_bot.png`|

_As densidades compiladas incluem:_ `mdpi`, `hdpi`, `xhdpi`, `xxhdpi` e `xxxhdpi`.

### Anatomia das Camadas do `<MauiIcon>`

Para atender aos requisitos nativos do Android sem perder compatibilidade com o Windows/iOS:

1. **`Include` (Camada de Fundo / Background):** Preenchimento sólido, gradiente ou SVG com dimensões totais (geralmente $108 \times 108\text{ dp}$).
    
2. **`ForegroundFile` (Camada Superior / Primeiro Plano):** O símbolo central com fundo transparente (ex: trevo de quatro folhas). Deve ocupar apenas os $66$ a $72\text{ dp}$ centrais para não ser cortado pela máscara do Android.
    

### Configuração com Condicional MSBuild no `.csproj`

Para fornecer um arquivo de primeiro plano menor exclusivo para o Android sem afetar as demais plataformas:



```XML
<ItemGroup>
    <!-- Configuração Exclusiva para Android: Usa SVG reduzido -->
    <MauiIcon Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)').Equals('android'))"
              Include="Resources\AppIcon\appicon.svg"
              ForegroundFile="Resources\AppIcon\appicon_android_fg.svg"
              TintColor="#FFFFFF" />

    <!-- Configuração para as Demais Plataformas (Windows, iOS, MacCatalyst) -->
    <MauiIcon Condition="!$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)').Equals('android'))"
              Include="Resources\AppIcon\appicon.svg"
              ForegroundFile="Resources\AppIcon\appiconfg.svg"
              TintColor="#FFFFFF" />
</ItemGroup>
```

### Resumo dos Atributos do `<MauiIcon>`

|**Atributo**|**Função**|**Comportamento no Android vs Windows**|
|---|---|---|
|**`Include`**|Define o background ou ícone base.|No Android vira a camada de fundo do adaptive icon; no Windows pode ser o ícone completo transparente.|
|**`ForegroundFile`**|Define a camada sobreposta.|Obrigatório para ícones adaptativos do Android; renderizado por cima do `Include`.|
|**`TintColor`**|Mascara a cor da arte do foreground.|Altera a cor de preenchimento dos vetores da logo (ex: muda o trevo verde para branco `#FFFFFF`).|
|**`Color`**|Cor de preenchimento de fundo.|Pinta áreas transparentes da imagem de fundo definida no `Include`.|
|**`ForegroundScale`**|Redimensiona a arte central.|Define a proporção (ex: `0.4` a `0.65`) sem precisar de um segundo arquivo SVG manual.|

### Procedimento de Validação no Dispositivo

1. **Substituição dos Arquivos:** Adicionar `appicon_android_fg.svg` à pasta `Resources/AppIcon/`.
    
2. **Limpeza do Cache:** Executar **Compilação > Limpar Solução** (_Clean Solution_).
    
3. **Desinstalação Manual:** Desinstalar a versão anterior do aplicativo no aparelho/emulador para forçar o Android Launcher a recarregar o cache de ícones adaptativos.
    
4. **Execução:** Compilar e implantar o projeto via Visual Studio (utilizando ferramentas como `scrcpy` para espelhar a tela do dispositivo USB).