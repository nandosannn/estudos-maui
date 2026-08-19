
No **.NET MAUI**, o gerenciamento de ícones adaptativos para o Android passou por mudanças importantes entre as versões **.NET 7** e **.NET 8**.

No Android, o sistema aplica uma máscara circular/quadrada com cantos arredondados sobre o ícone adaptativo. Se a arte de primeiro plano (_Foreground_) for desenhada até as bordas, ela é cortada. Para solucionar isso, o desenvolvedor precisa reduzir a escala da arte central.

### Comparativo: Abordagens entre .NET 7 e .NET 8+

|**Cenário**|**Comportamento no .NET 7**|**Comportamento no .NET 8 em diante**|
|---|---|---|
|**Duplicação de Tags sem Filtro**|Permitia sobrescrever arquivos de ícones já gerados na pasta intermediária.|**Gera erro de compilação**: o MSBuild/Resizetizer não permite gerar o mesmo ativo para a mesma plataforma duas vezes.|
|**Filtro de Plataforma no `.csproj`**|Podia declarar um genérico e outro com `Condition=" '$(TargetFramework)' == '...android...' "` por cima.|**Exige condições estritas de exclusão** (`!= '...android...'` e `== '...android...'`).|
|**Suporte ao `ForegroundScale`**|Tinha falhas de renderização/cálculo no build; exigia exportar uma segunda imagem menor manualmente no Figma.|**Funciona nativamente**: reduz a escala da imagem vetorial diretamente via MSBuild (`ForegroundScale="0.4"`).|

### 1. Solução A: Abordagem Moderna com `ForegroundScale` (Recomendada no .NET 8+)

Com o `ForegroundScale` corrigido no .NET 8+, **não é necessário criar duas imagens SVG diferentes** no Figma ou aplicar condicionais complexas para o ícone padrão se você quiser apenas reduzir a arte para caber na zona segura (_safe zone_):



```XML
<ItemGroup>
    <!-- 
      ForegroundScale="0.65" reduz o primeiro plano para 65% do tamanho,
      garantindo que o Android não corte as bordas do ícone adaptativo.
    -->
    <MauiIcon Include="Resources\AppIcon\appicon.svg"
              ForegroundFile="Resources\AppIcon\appiconfg.svg"
              TintColor="#FFFFFF"
              ForegroundScale="0.65" />
</ItemGroup>
```

### 2. Solução B: Condicionais de Plataforma no `.csproj`

Caso utilize dois arquivos vetoriais separados (por exemplo, `appiconfg.svg` para Desktop/iOS e `appiconfg_android.svg` menor para Android), a configuração precisa de condições mutuamente exclusivas para evitar erros no .NET 8+:



```XML
<ItemGroup>
    <!-- 1. Para TODAS as plataformas, EXCETO Android (iOS, MacCatalyst, Windows) -->
    <MauiIcon Condition="!$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)').Equals('android'))"
              Include="Resources\AppIcon\appicon.svg"
              ForegroundFile="Resources\AppIcon\appiconfg.svg"
              TintColor="#FFFFFF" />

    <!-- 2. APENAS para Android -->
    <MauiIcon Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)').Equals('android'))"
              Include="Resources\AppIcon\appicon.svg"
              ForegroundFile="Resources\AppIcon\appiconfg_android.svg"
              TintColor="#FFFFFF" />
</ItemGroup>
```

> **Por que isso é necessário?** Se remover o `Condition="!..."` da primeira tag, o .NET MAUI tentará compilar o ícone padrão para o Android e, em seguida, tentará compilar o ícone específico do Android, quebrando o processo de build do Resizetizer.

### 3. Propriedades do `<MauiIcon>` Atualizadas

|**Propriedade / Atributo**|**Tipo / Formato**|**Descrição**|
|---|---|---|
|**`ForegroundScale`**|Decimal (ex: `0.4` a `1.0`)|Reduz ou amplia a proporção do vetor de primeiro plano em relação ao fundo.|
|**`Condition`**|Expressão MSBuild|Controla em quais plataformas de destino (_TargetFramework_) aquele ativo será processado.|
|**`TintColor`**|Hexadecimal (`#FFFFFF`)|Substitui a cor original dos traços/preenchimentos do vetor de primeiro plano.|
|**`Color`**|Hexadecimal (`#512BD4`)|Preenche áreas transparentes do fundo.|