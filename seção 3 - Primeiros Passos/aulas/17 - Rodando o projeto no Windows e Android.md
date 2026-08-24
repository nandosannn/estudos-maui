# Aula — Ajustes do aplicativo .NET MAUI para Android

## 1. Objetivo da aula

Nesta aula, o aplicativo **Número da Sorte** é executado para verificar seu comportamento em diferentes sistemas operacionais.

O professor demonstra primeiro a execução no **Windows** e depois no **Android**, mostrando que, apesar de o .NET MAUI permitir reutilizar grande parte do código entre plataformas, alguns ajustes específicos precisam ser realizados em cada sistema operacional.

Os principais pontos trabalhados foram:

- Execução do aplicativo no Windows;
    
- Verificação do ícone do aplicativo;
    
- Ausência de Splash Screen inicialmente;
    
- Execução no Android;
    
- Personalização da barra de status do Android;
    
- Utilização do arquivo `Colors`;
    
- Diferença entre configurações gerais do MAUI e configurações específicas do Android;
    
- Identificação de um problema de corte na interface;
    
- Correção do problema causado pelo `HorizontalOptions`.
    

---

# 2. Testando o aplicativo no Windows

Primeiramente, o professor executa o aplicativo **Número da Sorte** no Windows.

Ao acessar o menu de aplicativos, é possível visualizar a logomarca do projeto.

### Observação sobre o ícone

O sistema operacional pode demorar um pouco para apresentar o ícone do aplicativo.

Isso pode acontecer principalmente na primeira execução, pois o sistema ainda pode estar realizando processos de indexação ou atualização das informações do aplicativo.

Portanto, caso o ícone não apareça imediatamente, isso não significa necessariamente que existe um problema no projeto.

---

# 3. Execução do aplicativo

Ao abrir o aplicativo, a tela inicial é apresentada.

Inicialmente, o projeto não possuía uma **Splash Screen** configurada.

A Splash Screen é a tela exibida temporariamente enquanto o aplicativo está sendo inicializado.

Como o aplicativo é simples e inicia rapidamente, a ausência dessa tela faz com que a transição para a tela principal seja praticamente imediata.

---

# 4. Funcionamento do Número da Sorte

Na tela principal existe o botão:

```text
Gerar número da sorte
```

Ao clicar nesse botão, o aplicativo gera os números da sorte.

O funcionamento básico é:

```text
Usuário clica no botão
        ↓
A lógica do aplicativo é executada
        ↓
Novos números são gerados
        ↓
Os números são apresentados na interface
```

Esse teste confirma que a lógica implementada anteriormente continua funcionando corretamente.

---

# 5. Por que utilizar o .NET MAUI?

O professor destaca que o .NET MAUI foi escolhido por permitir desenvolver aplicativos para diferentes plataformas utilizando uma mesma tecnologia.

Entre as plataformas mencionadas estão:

- Windows;
    
- Android;
    
- iOS;
    
- macOS.
    

Uma das vantagens é poder desenvolver e testar o aplicativo diretamente no Windows, tornando o processo mais prático durante o desenvolvimento.

Porém, isso não significa que o aplicativo ficará automaticamente perfeito em todas as plataformas.

Cada sistema operacional possui características próprias e pode exigir ajustes específicos.

---

# 6. Executando o aplicativo no Android

Depois de testar o aplicativo no Windows, o professor executa o projeto no Android.

Nesse momento aparecem dois problemas principais:

### Problema 1 — Barra de status

A barra de status do Android continua roxa.

Porém, o projeto utiliza uma identidade visual verde.

### Problema 2 — Interface cortada

Alguns elementos da interface aparecem parcialmente cortados.

Por exemplo:

- o trevo;
    
- o texto "Gerar número da sorte".
    

Isso demonstra uma característica importante do desenvolvimento multiplataforma:

> Uma interface que funciona corretamente em uma plataforma pode precisar de ajustes quando executada em outra.

---

# 7. Arquivo `Colors.xaml`

O .NET MAUI possui um arquivo chamado:

```text
Colors.xaml
```

Esse arquivo é utilizado para centralizar as cores utilizadas pelo aplicativo.

Nele podem existir cores como:

```text
Primary
Secondary
Tertiary
PrimaryDark
```

Essas cores podem ser utilizadas pelos componentes visuais do projeto.

Por exemplo:

```text
Primary   → cor principal
Secondary → cor secundária
Tertiary  → cor terciária
```

Alterar essas cores pode modificar a aparência de diversos elementos da interface.

---

# 8. Por que a barra de status não mudou?

Mesmo alterando a cor principal do projeto, a barra de status do Android continuou roxa.

Isso acontece porque a barra de status possui uma **configuração específica do Android**.

Portanto, alterar somente as cores utilizadas pelos componentes do MAUI não é suficiente para alterar determinados elementos nativos do sistema operacional.

Essa é uma característica importante do .NET MAUI:

```text
Configurações gerais do MAUI
             ↓
       Componentes da aplicação

Configurações específicas da plataforma
             ↓
Elementos próprios do Android/iOS/Windows/macOS
```

---

# 9. Configurações específicas do Android

Para modificar configurações específicas do Android, é necessário acessar a estrutura:

```text
Platforms
   └── Android
       └── Resources
           └── values
```

Dentro dessa estrutura existem arquivos relacionados às configurações visuais do Android.

Entre eles está o arquivo responsável pelas cores utilizadas pelo sistema Android.

Nesse arquivo existem definições específicas para as cores da interface.

---

# 10. `ColorPrimaryDark`

Um dos conceitos apresentados na aula é o:

```text
ColorPrimaryDark
```

A barra de status do Android normalmente utiliza uma versão mais escura da cor principal do aplicativo.

Por exemplo:

```text
Cor principal:
#00AB37

Cor da barra de status:
#00892C
```

A ideia é utilizar uma variação mais escura da cor principal.

Visualmente:

```text
Cor principal
████████████████

Cor mais escura
████████████████
```

Isso cria uma aparência de continuidade entre a interface do aplicativo e a barra de status.

---

# 11. Escolhendo a nova cor

Para manter a identidade visual do aplicativo, o professor utiliza uma tonalidade verde.

A cor utilizada como referência para a barra de status foi:

```text
#00892C
```

Enquanto o projeto utiliza uma tonalidade de verde mais clara como cor principal.

Essa combinação cria uma relação de:

```text
Verde claro → interface principal
Verde escuro → barra de status
```

---

# 12. Cores do projeto

A aula também reforça que, em projetos maiores, é interessante configurar todas as cores da identidade visual.

Por exemplo:

```text
Primary
Secondary
Tertiary
PrimaryDark
```

Isso facilita a manutenção do projeto.

Em vez de espalhar códigos de cores diretamente pelos arquivos XAML, podemos centralizar essas informações.

Por exemplo:

```xml
<Color x:Key="Primary">#00AB37</Color>
```

Assim, quando for necessário alterar a identidade visual, basta modificar a definição da cor.

---

# 13. Problema do corte da interface

Além da barra de status, havia outro problema no Android.

Parte da interface estava sendo cortada.

O professor investigou o problema e identificou que ele estava relacionado à propriedade:

```xml
HorizontalOptions
```

O projeto possuía uma configuração que fazia o `VerticalStackLayout` ser centralizado horizontalmente.

Porém, esse comportamento já era realizado por padrão naquele contexto.

Ou seja, havia uma configuração explícita fazendo algo que o componente já fazia naturalmente.

---

# 14. Removendo `HorizontalOptions`

A solução foi simplesmente remover a propriedade:

```xml
HorizontalOptions
```

Por exemplo, se existia:

```xml
<VerticalStackLayout
    HorizontalOptions="Center">
```

a propriedade poderia ser removida:

```xml
<VerticalStackLayout>
```

O motivo é que, naquele caso, o `VerticalStackLayout` já apresentava o comportamento esperado sem precisar dessa configuração adicional.

---

# 15. O que aconteceu com o problema?

Depois de remover o:

```xml
HorizontalOptions
```

o problema de corte desapareceu.

O layout continuou centralizado horizontalmente, mas agora sem apresentar o comportamento incorreto no Android.

Isso demonstra uma ideia importante:

> Nem sempre é necessário adicionar propriedades para obter determinado comportamento. Algumas propriedades possuem valores padrão que já atendem à necessidade do projeto.

---

# 16. Resultado final

Depois das alterações, o aplicativo foi executado novamente no Android.

O resultado apresentou:

- Barra de status com a cor correta;
    
- Interface sem elementos cortados;
    
- Splash Screen funcionando;
    
- Layout centralizado;
    
- Botão funcionando;
    
- Geração dos números funcionando normalmente.
    

O resultado final ficou semelhante ao comportamento apresentado no Windows, respeitando as particularidades do Android.

---

# 17. Conceitos importantes aprendidos

| Conceito            | Explicação                                                                         |
| ------------------- | ---------------------------------------------------------------------------------- |
| .NET MAUI           | Framework para desenvolvimento multiplataforma                                     |
| `Colors.xaml`       | Arquivo utilizado para centralizar cores do projeto                                |
| `Primary`           | Cor principal da aplicação                                                         |
| `Secondary`         | Cor secundária                                                                     |
| `Tertiary`          | Cor terciária                                                                      |
| `ColorPrimaryDark`  | Cor escura utilizada pelo Android, especialmente na barra de status                |
| `Platforms/Android` | Local onde ficam configurações específicas do Android                              |
| `Resources/values`  | Diretório de recursos utilizados pelo Android                                      |
| Status Bar          | Barra superior do Android que apresenta informações do sistema                     |
| Splash Screen       | Tela exibida durante a inicialização do aplicativo                                 |
| `HorizontalOptions` | Propriedade utilizada para definir o posicionamento horizontal de elementos        |
| Valor padrão        | Comportamento que um componente já possui quando uma propriedade não é configurada |

---

# 18. Estrutura conceitual do projeto

A aula demonstra uma separação importante entre o código compartilhado e as configurações específicas de cada plataforma:

```text
Projeto .NET MAUI
│
├── Código compartilhado
│   ├── XAML
│   ├── C#
│   └── Recursos gerais
│
└── Platforms
    │
    ├── Android
    │   └── Configurações específicas do Android
    │
    ├── iOS
    │   └── Configurações específicas do iOS
    │
    ├── Windows
    │   └── Configurações específicas do Windows
    │
    └── MacCatalyst
        └── Configurações específicas do macOS
```

Isso permite que grande parte da aplicação seja compartilhada entre plataformas, enquanto cada sistema pode possuir suas próprias configurações.

---

# 19. Principais aprendizados da aula

### 1. O aplicativo deve ser testado em diferentes plataformas

Não basta verificar se o projeto funciona no Windows.

É necessário testar também no Android, iOS, macOS etc., porque podem surgir diferenças de comportamento.

### 2. Nem tudo é controlado pelo MAUI

Alguns elementos pertencem diretamente ao sistema operacional.

Por isso, determinadas configurações precisam ser feitas dentro das pastas específicas da plataforma.

### 3. As cores podem ser centralizadas

O arquivo `Colors.xaml` facilita a organização e manutenção da identidade visual.

### 4. O Android possui configurações próprias

A barra de status é um exemplo de elemento que pode exigir configuração específica.

### 5. Propriedades desnecessárias podem causar problemas

A propriedade `HorizontalOptions` estava sendo utilizada para um comportamento que já acontecia naturalmente.

A remoção da propriedade resolveu o problema de corte da interface.

### 6. O comportamento padrão dos componentes deve ser conhecido

Antes de adicionar propriedades, é importante entender o comportamento padrão do componente.

Isso evita configurações redundantes e possíveis conflitos de layout.

---

# 20. Resumo da aula

Nesta aula foi realizada a validação do aplicativo **Número da Sorte** em diferentes plataformas. Primeiro, o aplicativo foi executado no Windows e seu funcionamento foi verificado.

Em seguida, o aplicativo foi executado no Android, onde foram identificados dois problemas: a barra de status permanecia roxa e alguns elementos da interface estavam sendo cortados.

Para corrigir a barra de status, foram analisadas as configurações de cores do projeto e as configurações específicas do Android em `Platforms/Android/Resources/values`.

Também foi utilizada uma tonalidade verde mais escura para a barra de status, mantendo a identidade visual do aplicativo.

O problema de corte da interface foi investigado e estava relacionado ao uso da propriedade `HorizontalOptions`. Como o `VerticalStackLayout` já apresentava o comportamento esperado por padrão, a propriedade foi removida.

Após as alterações, o aplicativo passou a funcionar corretamente no Android, com a barra de status adequada, interface sem cortes e geração dos números funcionando normalmente.

A principal conclusão da aula é que o **.NET MAUI permite compartilhar grande parte do desenvolvimento entre plataformas, mas algumas características precisam ser configuradas individualmente para cada sistema operacional**.