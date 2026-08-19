
O **.NET MAUI** simplifica o gerenciamento de ícones utilizando imagens vetoriais (**SVG**) e a ferramenta interna de build (**Resizetizer**). Em vez de exigir a criação manual de dezenas de resoluções para cada plataforma, o framework converte automaticamente um único arquivo SVG em todos os tamanhos e densidades de pixel necessários durante o processo de compilação.

### Estrutura e Atributos de Ícone (`.csproj`)

A configuração do ícone é declarada dentro do arquivo de projeto (`.csproj`) por meio da tag `<MauiIcon>`:

|**Atributo**|**Descrição**|**Exemplo de Valor**|
|---|---|---|
|**`Include`**|Define a camada de fundo (_background_) ou a imagem única.|`Resources\AppIcon\appicon.svg`|
|**`ForegroundFile`**|Define a camada de primeiro plano (_foreground_ / logo sobreposta).|`Resources\AppIcon\appiconfg.svg`|
|**`Color`**|Cor de preenchimento de fundo para áreas transparentes.|`#512BD4`|
|**`TintColor`**|Aplica uma máscara de cor sobre o vetor do primeiro plano.|`#FFFFFF`|

### 1. Modelos de Configuração do Ícone

**A. Ícone em Camadas (Adaptive Icons - Padrão Android/Desktop)**

Combina um fundo sólido/vetorial com uma camada de primeiro plano recortada, alterando a cor do ícone via software (`TintColor`):



```XML
<ItemGroup>
    <!-- Ícone com camada de fundo verde e primeiro plano pintado de branco -->
    <MauiIcon Include="Resources\AppIcon\appicon.svg" 
              ForegroundFile="Resources\AppIcon\appiconfg.svg" 
              TintColor="#FFFFFF" />
</ItemGroup>
```

**B. Ícone Único com Fundo Transparente (Estilo Windows tradicional)**

Remove a camada de fundo e desativa preenchimentos automáticos:



```XML
<ItemGroup>
    <!-- Apenas a logo sem sobreposição e sem cor de fundo forçada -->
    <MauiIcon Include="Resources\AppIcon\meu_icone_transparente.svg" />
</ItemGroup>
```

### 2. O Processo de Geração (Resizetizer)

Durante o build, o .NET MAUI gera os arquivos rasterizados (`.png`, `.ico`) na pasta intermediária de compilação:

$$\text{Caminho: } \texttt{obj/Debug/\{plataforma\}/resizetizer/r/}$$

- **Windows:** Gera escalas específicas (ex: `100%`, `125%`, `150%`, `200%`, `400%`) para a barra de tarefas, menu Iniciar e Microsoft Store (gerando mais de 30 variações).
    
- **Android:** Converte o par _Background/Foreground_ nas pastas de densidade nativas (`mipmap-mdpi`, `mipmap-hdpi`, `mipmap-xxxhdpi`).
    
- **iOS:** Gera as variações exigidas pelo catálogo de ativos (`Assets.xcassets`) para diferentes modelos de iPhone e iPad.
    

### 3. Passo a Passo para Substituição de Ícones

1. **Exportar os Vetores:** Salvar as artes em formato `.svg` (ex: `appicon.svg` para o fundo e `appiconfg.svg` para a arte central).
    
2. **Substituir Arquivos:** Copiar os novos arquivos para `Resources/AppIcon/` mantendo os nomes originais para preservar a ação de compilação (**Build Action = `MauiIcon`**).
    
3. **Ajustar `.csproj`:** Configurar `TintColor` ou remover `ForegroundFile` conforme o design desejado.
    
4. **Limpar a Compilação:** Executar **Limpar Solução** (_Clean Solution_) e desinstalar o app anterior do dispositivo/emulador para limpar o cache de ícones do sistema operacional.
    
5. **Recompilar:** Rodar a aplicação para disparar a geração dos novos ativos.