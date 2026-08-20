# Lógica da Mega-Sena em .NET MAUI

A aula conclui a lógica principal do aplicativo Mega-Sena em .NET MAUI, implementando o algoritmo responsável por gerar seis números aleatórios, sem repetição, em ordem crescente, e depois exibindo esses números nas `Labels` da interface.

## 1. Objetivo da aula

Implementar o botão **“Gerar Número da Sorte”**. Quando o usuário clicar nele, o programa deverá:

- Gerar números aleatórios entre 1 e 60.
    
- Gerar exatamente 6 números.
    
- Impedir números repetidos.
    
- Organizar os números em ordem crescente.
    
- Colocar cada número em uma `Label`.
    
- Exibir sempre dois dígitos:
    
    - $1 \rightarrow \text{01}$
        
    - $7 \rightarrow \text{07}$
        
    - $12 \rightarrow \text{12}$
        
- Fazer alterações sem reiniciar o aplicativo a cada mudança, utilizando o **Hot Reload / Recarga Dinâmica**.
    

## 2. Criando o método para gerar os números

No _Code Behind_ da página, cria-se o método responsável pela geração: `GenerateLuckyNumbers()`.

Inicialmente sem parâmetros, o método precisa retornar os números gerados (portanto, deixa de ser `void`).

C#

```
SortedSet<int> GenerateLuckyNumbers()
{
    // geração dos números
}
```

### Estrutura do método

|**Elemento**|**Função**|
|---|---|
|`SortedSet<int>`|Tipo de retorno|
|`GenerateLuckyNumbers`|Nome do método|
|`()`|Não recebe parâmetros|
|`return`|Devolve os números gerados|

## 3. Gerando números aleatórios com Random

Para gerar números aleatórios em C#, utilizamos a classe `Random`:

C#

```
Random random = new Random();
int luckyNumber = random.Next(1, 61); // Gera um número entre 1 e 60
```

> [!WARNING] Atenção ao `Next()`
> 
> O método `random.Next(1, 61)` **não** significa "de 1 até 61". O limite superior é **exclusivo**.
> 
> $\text{mínimo incluído} + \text{máximo excluído}$
> 
> |**Código**|**Possíveis valores**|
> |---|---|
> |`Next(1, 10)`|1 até 9|
> |`Next(1, 61)`|1 até 60|
> |`Next(0, 6)`|0 até 5|
> 
> Para a Mega-Sena, é necessário utilizar `61` como limite superior.

## 4. Primeiro problema: números repetidos

Se utilizarmos apenas um laço simples:

C#

```
for (int i = 0; i < 6; i++)
{
    int luckyNumber = random.Next(1, 61);
}
```

Poderemos obter repetições (ex.: `05, 12, 05, 34, 12, 59`), pois a classe `Random` apenas sorteia números isolados sem controle de contexto.

## 5. Segundo problema: números fora de ordem

Mesmo sem repetições, os números podem vir desordenados (ex.: `45, 03, 27, 12, 58, 19`).

O resultado desejado é a apresentação em ordem crescente: `03, 12, 19, 27, 45, 58`.

Portanto, precisamos de uma estrutura que:

1. Impeça duplicatas.
    
2. Mantenha os elementos ordenados.
    

## 6. Set: coleção sem duplicatas

Um `Set` é uma estrutura de dados voltada para armazenar elementos sem repetição.

C#

```
HashSet<int> numeros = new HashSet<int>();
```

Se tentarmos adicionar a sequência `10, 20, 10, 30, 20`, o conjunto armazenará apenas: `10, 20, 30`. Os repetidos são ignorados.

## 7. `SortedSet<T>`

A solução ideal combina duas propriedades:

1. **Não permite duplicatas**
    
2. **Mantém os elementos ordenados automaticamente**
    

C#

```
SortedSet<int> numeros = new SortedSet<int>();

numeros.Add(40);
numeros.Add(10);
numeros.Add(25);
numeros.Add(10); // Ignorado
numeros.Add(5);

// Resultado: 5, 10, 25, 40
```

## 8. Comparando as principais coleções

|**Estrutura**|**Permite repetição?**|**Mantém ordenação automática?**|
|---|---|---|
|`List<T>`|Sim|Não|
|`HashSet<T>`|Não|Não|
|`SortedSet<T>`|Não|Sim|

## 9. Por que o `for` não é suficiente?

C#

```
for (int i = 0; i < 6; i++)
{
    int luckyNumber = random.Next(1, 61);
    numeros.Add(luckyNumber);
}
```

Se houver duplicatas durante as 6 iterações (ex.: números sorteados `10, 20, 30, 20, 40, 50`), o `SortedSet` ficará com apenas 5 elementos.

> [!NOTE]
> 
> O laço `for` conta **sorteios realizados**, e não a quantidade final de números válidos inseridos.

## 10. Solução: `while`

Utiliza-se a condição baseada no tamanho da coleção:

C#

```
while (numeros.Count < 6)
```

> _"Enquanto eu ainda não tiver seis números diferentes, continue sorteando."_

## 11. Algoritmo completo de geração

C#

```
Random random = new Random();
SortedSet<int> luckyNumbers = new SortedSet<int>();

while (luckyNumbers.Count < 6)
{
    int luckyNumber = random.Next(1, 61);
    luckyNumbers.Add(luckyNumber);
}

return luckyNumbers;
```

## 12. Entendendo a execução do `while`

- Início: `Count = 0`
    
- Sorteia `37` $\rightarrow$ `Count = 1`
    
- Sorteia `12` $\rightarrow$ `Count = 2`
    
- Sorteia `37` (duplicado, não entra) $\rightarrow$ `Count = 2`
    
- Sorteia `51` $\rightarrow$ `Count = 3`
    
- Continua até `Count = 6`. A condição `6 < 6` resulta em `false` e o laço encerra.
    

## 13. Papel de cada recurso

Plaintext

```
Random ────► Gera número aleatório
                │
SortedSet ─► Remove duplicatas e ordena
                │
while ─────► Garante exatamente 6 números
```

|**Recurso**|**Responsabilidade**|
|---|---|
|`Random`|Gerar números aleatórios|
|`Next()`|Definir o intervalo do sorteio|
|`SortedSet<int>`|Evitar duplicatas e manter ordenado|
|`Count`|Informar quantidade de elementos|
|`while`|Continuar até obter 6 números|

## 14. Retornando os números

C#

```
private SortedSet<int> GenerateLuckyNumbers()
{
    Random random = new Random();
    SortedSet<int> luckyNumbers = new SortedSet<int>();

    while (luckyNumbers.Count < 6)
    {
        int luckyNumber = random.Next(1, 61);
        luckyNumbers.Add(luckyNumber);
    }

    return luckyNumbers;
}
```

## 15. Chamando o método

Ao clicar no botão:

C#

```
SortedSet<int> numbers = GenerateLuckyNumbers();
// Contém: 03, 17, 24, 35, 48, 59
```

## 16. Índices baseados em zero

|**Número exibido**|**Método de acesso**|**Índice**|
|---|---|---|
|1º Número|`numbers.ElementAt(0)`|0|
|2º Número|`numbers.ElementAt(1)`|1|
|3º Número|`numbers.ElementAt(2)`|2|
|4º Número|`numbers.ElementAt(3)`|3|
|5º Número|`numbers.ElementAt(4)`|4|
|6º Número|`numbers.ElementAt(5)`|5|

## 17. Exibindo nas Labels

C#

```
label1.Text = numbers.ElementAt(0).ToString();
label2.Text = numbers.ElementAt(1).ToString();
label3.Text = numbers.ElementAt(2).ToString();
label4.Text = numbers.ElementAt(3).ToString();
label5.Text = numbers.ElementAt(4).ToString();
label6.Text = numbers.ElementAt(5).ToString();
```

## 18. Diferença: `int` vs `string`

- `int numero = 15;` $\rightarrow$ Tipo numérico.
    
- `string texto = "15";` $\rightarrow$ Tipo textual.
    
- `label.Text` aceita apenas `string`, exigindo `.ToString()`.
    

## 19. Formatação com dois dígitos (`"D2"`)

Para exibir `01, 02...` em vez de `1, 2...`, utiliza-se o especificador de formato `"D2"`:

C#

```
int numero = 5;
string texto = numero.ToString("D2"); // "05"
```

## 20. O que significa `"D2"`?

- **D**: Decimal (número inteiro).
    
- **2**: Quantidade mínima de dígitos (preenche com zero à esquerda se necessário).
    

|**Número**|**ToString("D2")**|
|---|---|
|1|`"01"`|
|2|`"02"`|
|7|`"07"`|
|9|`"09"`|
|10|`"10"`|
|25|`"25"`|
|60|`"60"`|

Exemplo de uso: `numbers.ElementAt(0).ToString("D2")` $\rightarrow$ `"07"`.

## 21. Fluxo completo do aplicativo

Plaintext

```
Usuário clica em "Gerar Número da Sorte"
                 ↓
Transição da interface (Esconde antigos, mostra VerticalStackLayout)
                 ↓
GenerateLuckyNumbers()
                 ↓
Instancia Random e SortedSet<int>
                 ↓
while (Count < 6)
       ├──> Random.Next(1, 61)
       └──> SortedSet.Add(numero) -> (Ignora duplicados / Insere ordenado)
                 ↓
Retorna SortedSet<int> com 6 números
                 ↓
Preenche Labels com ElementAt(i).ToString("D2")
                 ↓
Números formatados exibidos na tela
```

## 22. Hot Reload / Recarga Dinâmica

Permite modificar o código C#/XAML e aplicar as alterações sem reiniciar a aplicação inteira:

$$\text{Alterar código} \longrightarrow \text{Compilar delta} \longrightarrow \text{Aplicar no app} \longrightarrow \text{Testar}$$

## 23. Limitações do Hot Reload

Determinadas alterações estruturais exigem reinicialização e recompilação completa do projeto. O Hot Reload não substitui o build tradicional, mas otimiza o ciclo de testes pontuais.

## 24. Recarga Dinâmica ao Salvar

Habilitar a opção de recarregar automaticamente ao salvar o arquivo agiliza o fluxo de desenvolvimento:

$$\text{Salvar} \longrightarrow \text{Recarga Dinâmica Automática} \longrightarrow \text{Testar}$$

## 25. Tabela de conceitos de C# aplicados

|**Conceito**|**Exemplo**|**O que representa**|
|---|---|---|
|**Método**|`GenerateLuckyNumbers()`|Encapsula uma funcionalidade|
|**Random**|`new Random()`|Geração de números pseudoaleatórios|
|**Next()**|`random.Next(1, 61)`|Sorteio dentro de intervalo delimitado|
|**SortedSet<T>**|`SortedSet<int>`|Conjunto sem duplicatas e ordenado|
|**while**|`while (Count < 6)`|Repetição baseada em condição lógica|
|**Count**|`numbers.Count`|Quantidade de elementos na coleção|
|**Add()**|`numbers.Add(numero)`|Adiciona elemento ao conjunto|
|**return**|`return numbers;`|Devolve o resultado da função|
|**Índice**|`ElementAt(0)`|Acessa elemento por posição sequencial|
|**int**|`int numero`|Tipo de dado para número inteiro|
|**string**|`Label.Text`|Tipo de dado para texto|
|**ToString()**|`numero.ToString()`|Conversão de tipos para texto|
|**"D2"**|`ToString("D2")`|Formatação numérica para dois dígitos|
|**Hot Reload**|Recarga Dinâmica|Atualização do app em tempo de execução|

## 26. `for` vs `while`

- **`for`**: Utilizado quando a quantidade exata de repetições é conhecida previamente.
    
- **`while`**: Utilizado quando a repetição depende do atendimento de uma condição (pois não sabemos de antemão quantos sorteios com duplicata ocorrerão até obter 6 números distintos).
    

## 27. Detalhe matemático

A probabilidade de repetição existe ao sortear 6 números dentro de 60. A combinação de `Random` + `SortedSet` + `while` cobre essa margem estatística com segurança e simplicidade de código.

## 28. Código final consolidado

C#

```
private SortedSet<int> GenerateLuckyNumbers()
{
    Random random = new Random();
    SortedSet<int> luckyNumbers = new SortedSet<int>();

    while (luckyNumbers.Count < 6)
    {
        int luckyNumber = random.Next(1, 61);
        luckyNumbers.Add(luckyNumber);
    }

    return luckyNumbers;
}

// Manipulação do evento de clique:
SortedSet<int> numbers = GenerateLuckyNumbers();

label1.Text = numbers.ElementAt(0).ToString("D2");
label2.Text = numbers.ElementAt(1).ToString("D2");
label3.Text = numbers.ElementAt(2).ToString("D2");
label4.Text = numbers.ElementAt(3).ToString("D2");
label5.Text = numbers.ElementAt(4).ToString("D2");
label6.Text = numbers.ElementAt(5).ToString("D2");
```

## 29. Resumo para revisão

> [!TIP] **Problema & Requisitos**
> 
> - **Intervalo:** $1 \le \text{número} \le 60$
>     
> - **Quantidade:** 6 números distintos
>     
> - **Ordenação:** Crescente
>     
> - **Interface:** Exibição com 2 dígitos (`D2`)
>     

> [!CHECK] **Mapeamento da Solução**
> 
> - `Random` $\rightarrow$ Sorteio
>     
> - `SortedSet<int>` $\rightarrow$ Elimina duplicatas e ordena
>     
> - `while` $\rightarrow$ Garante a contagem de 6 números
>     
> - `ToString("D2")` $\rightarrow$ Formata a saída visual
>