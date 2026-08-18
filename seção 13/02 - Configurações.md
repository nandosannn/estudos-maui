
A aula foca nas **primeiras configurações fundamentais de um projeto .NET MAUI**, explicando como definir a identidade do aplicativo (título, identificador único e versionamento) de forma centralizada ou específica por plataforma.

### Modos de Configuração no .NET MAUI

Existem duas formas principais de acessar e editar as propriedades do projeto:

- **Direto no arquivo de projeto (`.csproj`):** Clicando diretamente sobre o projeto no _Solution Explorer_. O arquivo XML contém as diretivas de plataformas suportadas (`TargetFrameworks`) e propriedades globais.
    
- **Pela Interface Gráfica de Propriedades:** Clicando com o botão direito no projeto $\rightarrow$ **Propriedades** $\rightarrow$ aba **MAUI** (Compartilhado/Shared).
    

### Configurações de Identidade e Versionamento

O .NET MAUI centraliza os dados essenciais e os injeta automaticamente nos arquivos nativos (como o `AndroidManifest.xml` no Android ou `Info.plist` no iOS).

|**Configuração**|**Descrição**|**Regra / Boas Práticas**|**Exemplo Prático**|
|---|---|---|---|
|**Título do Aplicativo** (_Application Title_)|Nome amigável que aparece na tela inicial e gaveta de apps do usuário.|Nome legível e comercial.|`Número da Sorte`|
|**ID do Aplicativo** (_Application ID / Package Name_)|Identificador exclusivo global do app no sistema operacional e nas lojas.|Padrão de **Domínio Reverso** (`sufixo.dominio.empresa.projeto`).|`br.com.spacebidu.appnumerodasorte`|
|**GUID do Aplicativo** (_Application ID GUID_)|Identificador único global gerado automaticamente em formato hexadecimal.|**Não alterar**. Usado para garantir unicidade em ecossistemas específicos (ex.: empacotamento Windows/iOS).|`a1b2c3d4-e5f6-7890-abcd-ef1234567890`|
|**Versão de Exibição** (_Application Display Version_)|Versão visível ao usuário na loja e na tela "Sobre" (_Version Name_).|Formato semântico livre (`MAJOR.MINOR.PATCH`). Aceita números e pontos.|`1.0.0`|
|**Versão do Aplicativo** (_Application Version_)|Código interno de controle para sistemas operacionais e lojas (_Version Code / Build_).|**Apenas números inteiros sequenciais**. Deve sempre ser incrementado a cada novo build/deploy.|`1`, `2`, `3`...|

### Estrutura do Versionamento Semântico (Versão de Exibição)

A aula detalha a convenção comum de versionamento em três segmentos (`X.Y.Z`):

```
       1   .   0   .   0
       │       │       │
       │       │       └── PATCH (Correções de bugs / pequenas alterações)
       │       └────────── MINOR (Novas funcionalidades compatíveis)
       └────────────────── MAJOR (Reestruturação total / grandes mudanças)
```

- **PATCH (Último segmento - ex: `1.0.1`):** Usado para _hotfixes_, correções de bugs em produção ou ajustes mínimos (ex.: adição de um campo simples em formulário).
    
- **MINOR (Segmento central - ex: `1.1.0`):** Usado ao adicionar novas funcionalidades completas que mantêm compatibilidade (ex.: suporte a sorteios da Lotomania e Lotofácil).
    
- **MAJOR (Primeiro segmento - ex: `2.0.0`):** Usado em reestruturações completas de layout, quebra de compatibilidade ou mudanças drásticas na arquitetura.
    

### Exemplo de Configuração no `.csproj`

As opções preenchidas na interface gráfica refletem diretamente nas tags XML do arquivo `.csproj`:

XML

```
<PropertyGroup>
    <!-- Plataformas suportadas -->
    <TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks>
    <TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows'))">$(TargetFrameworks);net8.0-windows10.0.19041.0</TargetFrameworks>

    <!-- Propriedades globais do App -->
    <ApplicationTitle>Número da Sorte</ApplicationTitle>
    <ApplicationId>br.com.spacebidu.appnumerodasorte</ApplicationId>
    <ApplicationIdGuid>A1B2C3D4-E5F6-7890-ABCD-EF1234567890</ApplicationIdGuid>
    
    <!-- Versionamento -->
    <ApplicationDisplayVersion>1.0.0</ApplicationDisplayVersion>
    <ApplicationVersion>1</ApplicationVersion>
</PropertyGroup>
```

### Comportamento Centralizado vs. Personalizado

- **Propagação Automática:** Configurando os dados no painel compartilhado do MAUI, o compilador preenche automaticamente os manifestos nativos (`AndroidManifest.xml`, `Info.plist`, `Package.appxmanifest`).
    
- **Sobrescrita por Plataforma:** Se uma plataforma exigir configurações específicas (como um nome diferente no Android ou permissões exclusivas), a alteração pode ser feita diretamente na seção individual da plataforma ou no manifesto nativo dentro da pasta `Platforms/`.