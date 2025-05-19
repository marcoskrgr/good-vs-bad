# Comparação de Código Java: Sem vs Com Google Java Style Guide

## Introdução

O Google Java Style Guide é um conjunto abrangente de padrões de codificação desenvolvido pelo Google para garantir consistência, legibilidade e manutenibilidade em projetos Java. Este documento apresenta uma análise detalhada de 15 exemplos comparativos, mostrando código Java sem seguir o style guide e sua versão corrigida, destacando as principais diferenças e benefícios da padronização.

Seguir um style guide como o do Google traz diversos benefícios:

- **Consistência**: Todo o código segue o mesmo padrão, facilitando a leitura e compreensão
- **Legibilidade**: Código bem formatado é mais fácil de ler e entender
- **Manutenibilidade**: Padrões consistentes facilitam a manutenção a longo prazo
- **Colaboração**: Facilita o trabalho em equipe, pois todos seguem as mesmas convenções
- **Qualidade**: Código padronizado tende a ter menos bugs e problemas de design

Vamos explorar os principais aspectos do Google Java Style Guide através de exemplos práticos e explicações detalhadas.

## Exemplo 1: Indentação e Nomenclatura

A indentação consistente e a nomenclatura clara são fundamentais para a legibilidade do código. O Google Style Guide recomenda indentação de 2 espaços (não tabs) e nomes significativos para variáveis, métodos e classes.

### Sem Style Guide

```java
// Indentação inconsistente, linhas muito longas, nomenclatura ruim
public class userManager{
    private int d; // dias desde a criação
    private String n; // nome do usuário
    
    public boolean checkIfUserIsValid(String userName, int userAge, boolean userIsActive, String userEmail, String userAddress){
        if(userAge>=18){
            if(userIsActive==true){
                if(userEmail!=null && userEmail.contains("@")){
                    return true;
                }else{return false;}
            }else{return false;}
        }else{return false;}
    }
}
```

### Com Style Guide

```java
// Indentação consistente, nomenclatura clara, formatação adequada
public class UserManager {
  private int daysSinceCreation;
  private String userName;
  
  /**
   * Verifica se o usuário é válido com base em vários critérios.
   *
   * @param userName Nome do usuário
   * @param userAge Idade do usuário
   * @param userIsActive Status de atividade do usuário
   * @param userEmail Email do usuário
   * @param userAddress Endereço do usuário
   * @return true se o usuário for válido, false caso contrário
   */
  public boolean isUserValid(String userName, int userAge, boolean userIsActive,
      String userEmail, String userAddress) {
    if (userAge < 18) {
      return false;
    }
    
    if (!userIsActive) {
      return false;
    }
    
    if (userEmail == null || !userEmail.contains("@")) {
      return false;
    }
    
    return true;
  }
}
```

### Explicação Detalhada

1. **Nomenclatura de Classes**: Classes devem usar PascalCase (primeira letra maiúscula). `userManager` foi corrigido para `UserManager`.

2. **Nomenclatura de Variáveis**: Variáveis devem ter nomes descritivos em camelCase. `d` e `n` foram substituídos por `daysSinceCreation` e `userName`.

3. **Indentação**: O Google Style Guide recomenda indentação de 2 espaços, não 4 espaços ou tabs.

4. **Espaçamento**: Deve haver espaços após palavras-chave como `if` e antes de chaves de abertura.

5. **Estrutura Lógica**: A versão corrigida inverte a lógica para retornar cedo em caso de falha, tornando o código mais limpo e fácil de seguir.

6. **Documentação**: A versão corrigida inclui comentários Javadoc explicando o propósito do método e seus parâmetros.

7. **Quebra de Linha**: Parâmetros longos são quebrados em múltiplas linhas com indentação adequada.

8. **Comparação Booleana**: `userIsActive==true` foi simplificado para apenas `!userIsActive`.

## Exemplo 2: Organização de Imports

O Google Style Guide especifica uma ordem clara para declarações de import e proíbe o uso de imports com asterisco (*).

### Sem Style Guide

```java
// Imports desordenados e com wildcard
import java.util.*;
import static java.lang.Math.*;
import java.io.File;
import com.example.project.*;
import java.nio.file.Path;

public class DataProcessor {
    // Código aqui
}
```

### Com Style Guide

```java
// Imports organizados corretamente
// Primeiro imports estáticos
import static java.lang.Math.PI;
import static java.lang.Math.max;

// Depois imports do Java
import java.io.File;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;

// Por último imports de terceiros e do projeto
import com.example.project.Model;
import com.example.project.Utils;

public class DataProcessor {
  // Código aqui
}
```

### Explicação Detalhada

1. **Ordem de Imports**: O Google Style Guide define uma ordem específica:
   - Primeiro, todos os imports estáticos em um único bloco
   - Depois, todos os imports não-estáticos do Java
   - Por último, imports de terceiros e do projeto

2. **Sem Imports com Wildcard**: Imports com asterisco (`*`) são proibidos. Cada classe deve ser importada explicitamente.

3. **Agrupamento**: Uma linha em branco separa cada grupo de imports.

4. **Ordenação Alfabética**: Dentro de cada bloco, os imports são ordenados alfabeticamente.

5. **Imports Estáticos Específicos**: Em vez de importar todos os métodos estáticos de Math, apenas os métodos necessários (PI e max) são importados.

6. **Imports Específicos**: Em vez de importar todo o pacote `com.example.project.*`, apenas as classes necessárias (Model e Utils) são importadas.

Esta organização torna o código mais legível e evita conflitos de nomes, além de deixar claro quais classes externas estão sendo utilizadas.

## Exemplo 3: Formatação de Chaves e Espaçamento

O Google Style Guide adota o estilo "one true brace" (1TBS), onde a chave de abertura fica na mesma linha da declaração e a chave de fechamento fica em uma linha separada.

### Sem Style Guide

```java
// Formatação inconsistente de chaves e espaçamento
public class Calculator{
public int add(int a,int b){return a+b;}
public int subtract(int a,int b)
{
return a-b;
}
public int multiply(int a,int b){
    return a*b;}
}
```

### Com Style Guide

```java
// Formatação consistente de chaves e espaçamento
public class Calculator {
  public int add(int a, int b) {
    return a + b;
  }
  
  public int subtract(int a, int b) {
    return a - b;
  }
  
  public int multiply(int a, int b) {
    return a * b;
  }
}
```

### Explicação Detalhada

1. **Posicionamento de Chaves**: A chave de abertura `{` fica na mesma linha da declaração, com um espaço antes. A chave de fechamento `}` fica em uma linha separada, alinhada com o início da declaração.

2. **Espaçamento entre Parâmetros**: Deve haver um espaço após cada vírgula em listas de parâmetros: `(int a, int b)` em vez de `(int a,int b)`.

3. **Espaçamento em Operadores**: Deve haver espaços em torno de operadores: `a + b` em vez de `a+b`.

4. **Indentação Consistente**: Todo o corpo do método é indentado com 2 espaços.

5. **Uma Instrução por Linha**: Cada instrução deve estar em sua própria linha, não na mesma linha que a declaração do método.

6. **Espaçamento Vertical**: Uma linha em branco entre métodos melhora a legibilidade.

Esta formatação consistente torna o código muito mais legível e fácil de seguir, especialmente em classes maiores com muitos métodos.

## Exemplo 4: Nomenclatura

O Google Style Guide define convenções claras para nomenclatura: classes em PascalCase, métodos e variáveis em camelCase, constantes em UPPER_SNAKE_CASE.

### Sem Style Guide

```java
// Nomenclatura inconsistente e não descritiva
public class DB {
    private String URL;
    private String user_name;
    private String PASSWORD;
    
    public void ConnectToDB() {
        // Código de conexão
    }
    
    public void get_data() {
        // Código para obter dados
    }
}
```

### Com Style Guide

```java
// Nomenclatura consistente e descritiva
public class Database {
  private String url;
  private String username;
  private String password;
  
  public void connectToDatabase() {
    // Código de conexão
  }
  
  public void getData() {
    // Código para obter dados
  }
}
```

### Explicação Detalhada

1. **Nomes de Classes**: Classes devem ter nomes descritivos em PascalCase. `DB` foi substituído por `Database`, que é mais descritivo.

2. **Nomes de Variáveis**: Variáveis devem usar camelCase. `URL` foi corrigido para `url`, `user_name` para `username` e `PASSWORD` para `password`.

3. **Nomes de Métodos**: Métodos devem usar camelCase. `ConnectToDB` foi corrigido para `connectToDatabase` e `get_data` para `getData`.

4. **Consistência**: Todos os identificadores seguem o mesmo padrão, sem misturar estilos como snake_case e camelCase.

5. **Descritivo**: Os nomes são mais descritivos e completos, facilitando a compreensão do propósito de cada elemento.

6. **Sem Abreviações Ambíguas**: Abreviações como `DB` são evitadas em favor de nomes completos como `Database`.

A nomenclatura consistente e descritiva é crucial para a legibilidade e manutenibilidade do código, especialmente em projetos grandes com muitos desenvolvedores.

## Exemplo 5: Comentários

O Google Style Guide recomenda o uso de comentários Javadoc para classes e métodos públicos, e desencoraja comentários óbvios ou redundantes.

### Sem Style Guide

```java
// Comentários desnecessários e formatação ruim
public class StringUtils {
    // Este método verifica se a string está vazia
    public boolean isEmpty(String s) {
        // Retorna verdadeiro se a string for nula ou vazia
        return s == null || s.length() == 0; // Retorna o resultado da verificação
    }
    
    // Este método inverte a string
    public String reverse(String s) {
        // Cria um StringBuilder com a string
        StringBuilder sb = new StringBuilder(s);
        // Inverte o StringBuilder
        sb.reverse();
        // Retorna a string invertida
        return sb.toString();
    }
}
```

### Com Style Guide

```java
// Comentários úteis e formatação adequada
public class StringUtils {
  /**
   * Verifica se a string está vazia.
   *
   * @param s String a ser verificada
   * @return true se a string for nula ou vazia
   */
  public boolean isEmpty(String s) {
    return s == null || s.length() == 0;
  }
  
  /**
   * Inverte a string fornecida.
   *
   * @param s String a ser invertida
   * @return A string invertida
   */
  public String reverse(String s) {
    return new StringBuilder(s).reverse().toString();
  }
}
```

### Explicação Detalhada

1. **Comentários Javadoc**: A versão corrigida usa comentários Javadoc (`/**...*/`) para documentar métodos, incluindo descrições dos parâmetros e valores de retorno.

2. **Eliminação de Comentários Óbvios**: Comentários que apenas repetem o que o código já diz claramente foram removidos.

3. **Foco no "Por quê" e não no "O quê"**: Bons comentários explicam o propósito e a razão do código, não apenas o que ele faz.

4. **Simplificação do Código**: O código foi simplificado, eliminando variáveis temporárias desnecessárias.

5. **Formatação Consistente**: A formatação segue o padrão do Google Style Guide, com indentação de 2 espaços.

6. **Documentação Estruturada**: Os comentários Javadoc seguem uma estrutura clara com descrição, parâmetros (`@param`) e retorno (`@return`).

Comentários bem escritos são uma parte essencial de código de qualidade, mas devem agregar valor e não apenas repetir o óbvio. O Google Style Guide enfatiza a importância de documentação clara e concisa.

## Exemplo 6: Métodos Longos vs. Métodos Focados

O Google Style Guide incentiva métodos curtos e focados que fazem apenas uma coisa. Isso melhora a legibilidade, testabilidade e manutenibilidade do código.

### Sem Style Guide

```java
// Métodos muito longos e complexos
public class OrderProcessor {
    public void processOrder(Order order) {
        if (order != null) {
            if (order.getItems() != null && !order.getItems().isEmpty()) {
                double total = 0;
                for (Item item : order.getItems()) {
                    if (item.getPrice() > 0 && item.getQuantity() > 0) {
                        double itemTotal = item.getPrice() * item.getQuantity();
                        if (item.hasDiscount()) {
                            itemTotal = itemTotal * (1 - item.getDiscountRate());
                        }
                        total += itemTotal;
                        item.setProcessed(true);
                        System.out.println("Item processed: " + item.getName());
                    } else {
                        System.out.println("Invalid item: " + item.getName());
                    }
                }
                order.setTotal(total);
                order.setStatus("PROCESSED");
                System.out.println("Order processed with total: " + total);
            } else {
                System.out.println("Order has no items");
            }
        } else {
            System.out.println("Order is null");
        }
    }
}
```

### Com Style Guide

```java
// Métodos mais curtos e focados
public class OrderProcessor {
  public void processOrder(Order order) {
    if (order == null) {
      logError("Order is null");
      return;
    }
    
    if (order.getItems() == null || order.getItems().isEmpty()) {
      logError("Order has no items");
      return;
    }
    
    double total = calculateOrderTotal(order);
    updateOrderStatus(order, total);
  }
  
  private double calculateOrderTotal(Order order) {
    double total = 0;
    for (Item item : order.getItems()) {
      if (isValidItem(item)) {
        total += calculateItemTotal(item);
        markItemAsProcessed(item);
      } else {
        logInvalidItem(item);
      }
    }
    return total;
  }
  
  private boolean isValidItem(Item item) {
    return item.getPrice() > 0 && item.getQuantity() > 0;
  }
  
  private double calculateItemTotal(Item item) {
    double itemTotal = item.getPrice() * item.getQuantity();
    if (item.hasDiscount()) {
      itemTotal = itemTotal * (1 - item.getDiscountRate());
    }
    return itemTotal;
  }
  
  private void markItemAsProcessed(Item item) {
    item.setProcessed(true);
    logItemProcessed(item);
  }
  
  private void updateOrderStatus(Order order, double total) {
    order.setTotal(total);
    order.setStatus("PROCESSED");
    logOrderProcessed(order);
  }
  
  private void logItemProcessed(Item item) {
    System.out.println("Item processed: " + item.getName());
  }
  
  private void logInvalidItem(Item item) {
    System.out.println("Invalid item: " + item.getName());
  }
  
  private void logOrderProcessed(Order order) {
    System.out.println("Order processed with total: " + order.getTotal());
  }
  
  private void logError(String message) {
    System.out.println(message);
  }
}
```

### Explicação Detalhada

1. **Métodos Pequenos e Focados**: A versão corrigida divide o grande método `processOrder` em vários métodos menores, cada um com uma responsabilidade específica.

2. **Princípio da Responsabilidade Única**: Cada método faz apenas uma coisa e a faz bem.

3. **Retorno Antecipado**: A versão corrigida usa retornos antecipados para casos de erro, simplificando a lógica.

4. **Nomes Descritivos**: Cada método tem um nome que descreve claramente o que ele faz.

5. **Abstração de Lógica**: Operações como validação de itens, cálculo de totais e atualização de status são abstraídas em métodos separados.

6. **Encapsulamento de Lógica**: A lógica de negócios está encapsulada em métodos específicos, facilitando alterações futuras.

7. **Redução de Aninhamento**: O nível de aninhamento de condicionais foi reduzido significativamente, tornando o código mais legível.

8. **Testabilidade**: Métodos menores são mais fáceis de testar individualmente.

Esta abordagem de métodos pequenos e focados é um princípio fundamental de código limpo e facilita enormemente a manutenção e evolução do código ao longo do tempo.

## Exemplo 7: Documentação Javadoc

O Google Style Guide especifica como formatar a documentação Javadoc, incluindo a ordem dos elementos e a formatação dos parágrafos.

### Sem Style Guide

```java
// Uso excessivo de comentários e formatação inconsistente
/**
 * Esta classe representa um usuário
 * @author Desenvolvedor
 */
public class User {
    /** O nome do usuário */
    private String name;
    /** A idade do usuário */private int age;
    /** O email do usuário */
    private String email;
    
    /**
     * Construtor
     * @param name O nome
     * @param age A idade
     * @param email O email
     */
    public User(String name, int age, String email) {
        this.name = name;this.age = age;this.email = email;
    }
    
    /** Retorna o nome */
    public String getName() { return name; }
    /** Define o nome */
    public void setName(String name) { this.name = name; }
}
```

### Com Style Guide

```java
/**
 * Representa um usuário no sistema.
 */
public class User {
  private String name;
  private int age;
  private String email;
  
  /**
   * Cria um novo usuário com os dados fornecidos.
   *
   * @param name Nome do usuário
   * @param age Idade do usuário
   * @param email Email do usuário
   */
  public User(String name, int age, String email) {
    this.name = name;
    this.age = age;
    this.email = email;
  }
  
  public String getName() {
    return name;
  }
  
  public void setName(String name) {
    this.name = name;
  }
}
```

### Explicação Detalhada

1. **Documentação Concisa**: A versão corrigida tem documentação mais concisa e focada no essencial.

2. **Formatação Javadoc**: Os comentários Javadoc seguem o formato recomendado, com uma linha em branco após a descrição e antes dos parâmetros.

3. **Remoção de Comentários Redundantes**: Comentários óbvios para getters e setters foram removidos.

4. **Descrições Significativas**: As descrições são mais informativas e contextualizadas.

5. **Formatação de Código**: O código segue a formatação recomendada, com indentação de 2 espaços e uma instrução por linha.

6. **Sem Tags Desnecessárias**: A tag `@author` foi removida, pois o Google Style Guide não a recomenda em código de produção.

7. **Sem Comentários para Campos Privados**: Campos privados não precisam de comentários Javadoc, a menos que sejam complexos ou não óbvios.

A documentação Javadoc adequada é essencial para APIs públicas, mas deve ser concisa e focar no que é realmente importante para os usuários da classe ou método.

## Exemplo 8: Estruturas Condicionais

O Google Style Guide recomenda o uso de switch-case em vez de múltiplos if-else quando apropriado, e exige espaçamento adequado em torno de operadores e parênteses.

### Sem Style Guide

```java
// Uso inconsistente de espaços e operadores
public class MathUtils{
    public int calculate(int a,int b,String operation){
        if(operation.equals("add")){
            return a+b;
        }else if(operation.equals("subtract")){
            return a-b;
        }else if(operation.equals("multiply")){
            return a*b;
        }else if(operation.equals("divide")){
            if(b==0)throw new ArithmeticException("Division by zero");
            return a/b;
        }else{
            throw new IllegalArgumentException("Unknown operation: "+operation);
        }
    }
}
```

### Com Style Guide

```java
// Uso consistente de espaços e operadores
public class MathUtils {
  public int calculate(int a, int b, String operation) {
    switch (operation) {
      case "add":
        return a + b;
      case "subtract":
        return a - b;
      case "multiply":
        return a * b;
      case "divide":
        if (b == 0) {
          throw new ArithmeticException("Division by zero");
        }
        return a / b;
      default:
        throw new IllegalArgumentException("Unknown operation: " + operation);
    }
  }
}
```

### Explicação Detalhada

1. **Uso de switch-case**: A versão corrigida usa `switch-case` em vez de múltiplos `if-else` para melhor legibilidade quando há múltiplas opções baseadas no mesmo valor.

2. **Espaçamento Consistente**: Há espaços após palavras-chave (`if`, `switch`), antes de chaves de abertura, e em torno de operadores.

3. **Uso de Chaves**: Mesmo para blocos de uma única linha, as chaves são usadas.

4. **Indentação Consistente**: A indentação segue o padrão de 2 espaços.

5. **Formatação de Exceções**: A instrução `throw` está em sua própria linha, com chaves adequadas.

6. **Espaçamento em Concatenação de Strings**: Há espaços em torno do operador `+` na concatenação de strings.

7. **Formatação de Parâmetros**: Há espaços após as vírgulas na lista de parâmetros.

A escolha entre `if-else` e `switch-case` depende do contexto, mas para múltiplas condições baseadas no mesmo valor, `switch-case` geralmente oferece melhor legibilidade e pode ser otimizado pelo compilador.

## Exemplo 9: Comprimento de Linhas

O Google Style Guide limita o comprimento das linhas a 100 caracteres, exigindo quebras de linha adequadas para linhas mais longas.

### Sem Style Guide

```java
// Linhas muito longas e formatação inconsistente
public class FileProcessor {
    public static final String DEFAULT_DIRECTORY = "/tmp/files/";
    public static final String[] SUPPORTED_EXTENSIONS = new String[] { "txt", "csv", "json", "xml", "html", "md", "log", "properties", "conf", "ini" };
    
    public List<File> findFiles(String directory, String extension, boolean includeSubdirectories, int maxDepth, boolean skipHiddenFiles, Comparator<File> sortOrder) {
        // Implementação
        return null;
    }
}
```

### Com Style Guide

```java
// Linhas com comprimento adequado e formatação consistente
public class FileProcessor {
  public static final String DEFAULT_DIRECTORY = "/tmp/files/";
  public static final String[] SUPPORTED_EXTENSIONS = {
      "txt", "csv", "json", "xml", "html", "md", "log", "properties", "conf", "ini"
  };
  
  /**
   * Encontra arquivos com base nos critérios especificados.
   *
   * @param directory Diretório onde procurar
   * @param extension Extensão dos arquivos
   * @param includeSubdirectories Se deve incluir subdiretórios
   * @param maxDepth Profundidade máxima de busca
   * @param skipHiddenFiles Se deve ignorar arquivos ocultos
   * @param sortOrder Ordem de classificação dos resultados
   * @return Lista de arquivos encontrados
   */
  public List<File> findFiles(
      String directory,
      String extension,
      boolean includeSubdirectories,
      int maxDepth,
      boolean skipHiddenFiles,
      Comparator<File> sortOrder) {
    // Implementação
    return null;
  }
}
```

### Explicação Detalhada

1. **Limite de 100 Caracteres**: O Google Style Guide limita as linhas a 100 caracteres para melhorar a legibilidade, especialmente em telas divididas ou revisões de código.

2. **Quebra de Arrays**: O array de extensões é quebrado em múltiplas linhas, com cada linha indentada adequadamente.

3. **Quebra de Parâmetros**: A lista de parâmetros do método `findFiles` é quebrada em múltiplas linhas, com um parâmetro por linha.

4. **Indentação de Continuação**: A indentação de continuação é de 4 espaços (2 espaços base + 2 espaços adicionais).

5. **Documentação Javadoc**: A versão corrigida inclui documentação Javadoc completa para o método.

6. **Sintaxe de Array Simplificada**: A sintaxe do array foi simplificada, removendo o `new String[]` desnecessário.

7. **Formatação Consistente**: Todo o código segue a formatação recomendada pelo Google Style Guide.

Limitar o comprimento das linhas melhora a legibilidade do código, especialmente quando visualizado em diferentes ambientes (editores, revisões de código, terminais, etc.).

## Exemplo 10: Declarações Múltiplas

O Google Style Guide recomenda uma declaração por linha, em vez de múltiplas declarações na mesma linha.

### Sem Style Guide

```java
// Declarações múltiplas na mesma linha e formatação inconsistente
public class Customer {
    private String firstName, lastName, email; private int age; private boolean active;
    
    public Customer() { firstName = ""; lastName = ""; email = ""; age = 0; active = false; }
    
    public String getFullName() { return firstName + " " + lastName; }
    
    public boolean isEligible() { return age >= 18 && active; }
}
```

### Com Style Guide

```java
// Declarações individuais e formatação consistente
public class Customer {
  private String firstName;
  private String lastName;
  private String email;
  private int age;
  private boolean active;
  
  public Customer() {
    firstName = "";
    lastName = "";
    email = "";
    age = 0;
    active = false;
  }
  
  public String getFullName() {
    return firstName + " " + lastName;
  }
  
  public boolean isEligible() {
    return age >= 18 && active;
  }
}
```

### Explicação Detalhada

1. **Uma Declaração por Linha**: Cada variável é declarada em sua própria linha, melhorando a legibilidade.

2. **Corpo do Método em Múltiplas Linhas**: O corpo de cada método está em múltiplas linhas, mesmo para métodos simples.

3. **Chaves em Linhas Separadas**: As chaves de abertura e fechamento seguem o padrão recomendado.

4. **Espaçamento Vertical**: Há espaçamento adequado entre métodos e blocos de código.

5. **Indentação Consistente**: Todo o código segue a indentação de 2 espaços.

6. **Inicialização Separada**: Cada inicialização no construtor está em sua própria linha.

7. **Formatação de Operadores**: Há espaços adequados em torno de operadores como `+`, `>=` e `&&`.

Declarar uma variável por linha facilita a leitura, a documentação e a modificação do código, além de tornar as diferenças em sistemas de controle de versão mais claras.

## Exemplo 11: Uso de Chaves em Estruturas Condicionais

O Google Style Guide exige o uso de chaves em todas as estruturas de controle, mesmo para blocos de uma única linha.

### Sem Style Guide

```java
// Indentação inconsistente e uso incorreto de chaves
public class ValidationUtils
{
  public static boolean isValidEmail(String email)
  {
    if (email == null) return false;
    if (email.isEmpty()) return false;
    if (!email.contains("@")) return false;
    
    String[] parts = email.split("@");
    if (parts.length != 2) return false;
    
    if (parts[0].isEmpty()) return false;
    if (parts[1].isEmpty()) return false;
    
    return true;
  }
}
```

### Com Style Guide

```java
// Indentação consistente e uso correto de chaves
public class ValidationUtils {
  /**
   * Verifica se um email é válido.
   *
   * @param email Email a ser validado
   * @return true se o email for válido, false caso contrário
   */
  public static boolean isValidEmail(String email) {
    if (email == null) {
      return false;
    }
    
    if (email.isEmpty()) {
      return false;
    }
    
    if (!email.contains("@")) {
      return false;
    }
    
    String[] parts = email.split("@");
    if (parts.length != 2) {
      return false;
    }
    
    if (parts[0].isEmpty()) {
      return false;
    }
    
    if (parts[1].isEmpty()) {
      return false;
    }
    
    return true;
  }
}
```

### Explicação Detalhada

1. **Uso Obrigatório de Chaves**: Mesmo para blocos de uma única linha, as chaves são obrigatórias.

2. **Posicionamento de Chaves**: A chave de abertura fica na mesma linha da declaração, e a chave de fechamento fica em uma linha separada.

3. **Indentação de 2 Espaços**: Todo o código segue a indentação de 2 espaços, não 4.

4. **Espaçamento Vertical**: Há uma linha em branco entre blocos condicionais para melhorar a legibilidade.

5. **Documentação Javadoc**: A versão corrigida inclui documentação Javadoc para o método.

6. **Instrução em Linha Separada**: Cada instrução `return` está em sua própria linha, não na mesma linha que a condição.

7. **Estilo de Chaves Consistente**: Todas as chaves seguem o mesmo estilo em todo o código.

O uso consistente de chaves, mesmo para blocos de uma única linha, evita erros comuns quando novas linhas são adicionadas a um bloco existente e melhora a legibilidade do código.

## Exemplo 12: Formatação de Switch-Case

O Google Style Guide especifica como formatar instruções switch-case, incluindo indentação e posicionamento de chaves.

### Sem Style Guide

```java
// Uso inconsistente de espaços e formatação
public class DateUtils{
    public static boolean isLeapYear(int year){
        if(year%400==0)return true;
        if(year%100==0)return false;
        return year%4==0;
    }
    
    public static int getDaysInMonth(int month,int year){
        switch(month){
            case 1:case 3:case 5:case 7:case 8:case 10:case 12:return 31;
            case 4:case 6:case 9:case 11:return 30;
            case 2:return isLeapYear(year)?29:28;
            default:throw new IllegalArgumentException("Invalid month: "+month);
        }
    }
}
```

### Com Style Guide

```java
// Uso consistente de espaços e formatação
public class DateUtils {
  /**
   * Verifica se o ano é bissexto.
   *
   * @param year Ano a ser verificado
   * @return true se o ano for bissexto, false caso contrário
   */
  public static boolean isLeapYear(int year) {
    if (year % 400 == 0) {
      return true;
    }
    
    if (year % 100 == 0) {
      return false;
    }
    
    return year % 4 == 0;
  }
  
  /**
   * Retorna o número de dias em um mês específico.
   *
   * @param month Mês (1-12)
   * @param year Ano
   * @return Número de dias no mês
   * @throws IllegalArgumentException se o mês for inválido
   */
  public static int getDaysInMonth(int month, int year) {
    switch (month) {
      case 1:
      case 3:
      case 5:
      case 7:
      case 8:
      case 10:
      case 12:
        return 31;
      case 4:
      case 6:
      case 9:
      case 11:
        return 30;
      case 2:
        return isLeapYear(year) ? 29 : 28;
      default:
        throw new IllegalArgumentException("Invalid month: " + month);
    }
  }
}
```

### Explicação Detalhada

1. **Formatação de Switch-Case**: Cada `case` está em sua própria linha, e o código para cada caso está indentado.

2. **Uso de Chaves**: Chaves são usadas consistentemente em todas as estruturas de controle.

3. **Espaçamento em Operadores**: Há espaços em torno de operadores como `%`, `==`, `?:` e `+`.

4. **Documentação Javadoc**: A versão corrigida inclui documentação Javadoc para ambos os métodos.

5. **Espaçamento após Vírgulas**: Há espaços após as vírgulas na lista de parâmetros.

6. **Indentação Consistente**: Todo o código segue a indentação de 2 espaços.

7. **Formatação de Exceções**: A instrução `throw` está adequadamente formatada.

8. **Operador Ternário**: O operador ternário `? :` é usado com espaçamento adequado.

A formatação adequada de instruções switch-case é importante para a legibilidade, especialmente em casos com múltiplas opções ou lógica complexa.

## Exemplo 13: Nomenclatura de Métodos e Constantes

O Google Style Guide define convenções para nomenclatura de métodos (camelCase) e constantes (UPPER_SNAKE_CASE).

### Sem Style Guide

```java
// Nomenclatura inconsistente e formatação ruim
public class HTTPUtil {
    private static final int TIME_OUT = 5000;
    
    public static Response SendGetRequest(String URL, Map<String, String> Headers) {
        // Implementação
        return null;
    }
    
    public static Response send_post_request(String url, String body, Map<String, String> headers) {
        // Implementação
        return null;
    }
    
    private static void LOG_ERROR(Exception e) {
        System.err.println("Error: " + e.getMessage());
    }
}
```

### Com Style Guide

```java
// Nomenclatura consistente e formatação adequada
public class HttpUtil {
  private static final int TIMEOUT_MS = 5000;
  
  /**
   * Envia uma requisição GET HTTP.
   *
   * @param url URL para a requisição
   * @param headers Cabeçalhos da requisição
   * @return Resposta da requisição
   */
  public static Response sendGetRequest(String url, Map<String, String> headers) {
    // Implementação
    return null;
  }
  
  /**
   * Envia uma requisição POST HTTP.
   *
   * @param url URL para a requisição
   * @param body Corpo da requisição
   * @param headers Cabeçalhos da requisição
   * @return Resposta da requisição
   */
  public static Response sendPostRequest(String url, String body, Map<String, String> headers) {
    // Implementação
    return null;
  }
  
  private static void logError(Exception e) {
    System.err.println("Error: " + e.getMessage());
  }
}
```

### Explicação Detalhada

1. **Nomenclatura de Classes**: Classes usam PascalCase, com acrônimos tratados como palavras normais. `HTTPUtil` foi corrigido para `HttpUtil`.

2. **Nomenclatura de Constantes**: Constantes usam UPPER_SNAKE_CASE. `TIME_OUT` foi corrigido para `TIMEOUT_MS`, também adicionando a unidade para maior clareza.

3. **Nomenclatura de Métodos**: Métodos usam camelCase. `SendGetRequest` foi corrigido para `sendGetRequest` e `send_post_request` para `sendPostRequest`.

4. **Nomenclatura de Parâmetros**: Parâmetros usam camelCase. `URL` e `Headers` foram corrigidos para `url` e `headers`.

5. **Nomenclatura de Métodos Privados**: Métodos privados também usam camelCase. `LOG_ERROR` foi corrigido para `logError`.

6. **Documentação Javadoc**: A versão corrigida inclui documentação Javadoc para os métodos públicos.

7. **Consistência**: Toda a nomenclatura segue um padrão consistente, sem misturar estilos.

A nomenclatura consistente é crucial para a legibilidade e manutenibilidade do código, especialmente em projetos grandes com muitos desenvolvedores.

## Exemplo 14: Uso de Modificadores

O Google Style Guide especifica a ordem dos modificadores e recomenda o uso explícito do modificador de acesso (public, private, etc.).

### Sem Style Guide

```java
// Uso inconsistente de modificadores e formatação
class ConfigManager {
    static Map<String, Object> config = new HashMap<>();
    
    public static void loadConfig(String path) {
        // Implementação
    }
    
    static Object getConfigValue(String key) {
        return config.get(key);
    }
    
    private static void parseConfigFile(File file) {
        // Implementação
    }
    
    public void reloadConfig() {
        // Implementação
    }
}
```

### Com Style Guide

```java
// Uso consistente de modificadores e formatação
public class ConfigManager {
  private static final Map<String, Object> config = new HashMap<>();
  
  /**
   * Carrega a configuração a partir do caminho especificado.
   *
   * @param path Caminho do arquivo de configuração
   */
  public static void loadConfig(String path) {
    // Implementação
  }
  
  /**
   * Obtém um valor de configuração.
   *
   * @param key Chave da configuração
   * @return Valor da configuração ou null se não existir
   */
  public static Object getConfigValue(String key) {
    return config.get(key);
  }
  
  private static void parseConfigFile(File file) {
    // Implementação
  }
  
  /**
   * Recarrega a configuração.
   */
  public void reloadConfig() {
    // Implementação
  }
}
```

### Explicação Detalhada

1. **Modificador de Classe**: A classe agora tem o modificador `public` explícito.

2. **Modificadores de Campo**: O campo `config` agora é `private static final`, seguindo o princípio de menor visibilidade possível.

3. **Modificadores de Método**: Todos os métodos têm modificadores de acesso explícitos.

4. **Ordem de Modificadores**: A ordem dos modificadores segue a recomendação da JLS (Java Language Specification).

5. **Documentação Javadoc**: A versão corrigida inclui documentação Javadoc para os métodos públicos.

6. **Consistência**: Todos os modificadores são usados de forma consistente em todo o código.

7. **Imutabilidade**: O uso de `final` para o mapa `config` indica que a referência não pode ser alterada, embora o conteúdo possa.

O uso adequado de modificadores é importante para controlar a visibilidade e o comportamento dos elementos do código, seguindo o princípio de menor privilégio.

## Exemplo 15: Formatação de Parâmetros

O Google Style Guide especifica como formatar parâmetros de métodos, especialmente quando há muitos parâmetros ou quando a linha excede o limite de 100 caracteres.

### Sem Style Guide

```java
// Uso inconsistente de espaços e formatação de parâmetros
public class EmailSender{
    private String smtpServer;private int port;private String username;private String password;
    
    public EmailSender(String smtpServer,int port,String username,String password){
        this.smtpServer=smtpServer;
        this.port=port;
        this.username=username;
        this.password=password;
    }
    
    public boolean sendEmail(String from,String to,String subject,String body,boolean isHtml,List<String>attachments){
        // Implementação
        return true;
    }
}
```

### Com Style Guide

```java
// Uso consistente de espaços e formatação de parâmetros
public class EmailSender {
  private final String smtpServer;
  private final int port;
  private final String username;
  private final String password;
  
  /**
   * Cria um novo enviador de emails.
   *
   * @param smtpServer Servidor SMTP
   * @param port Porta do servidor
   * @param username Nome de usuário
   * @param password Senha
   */
  public EmailSender(
      String smtpServer,
      int port,
      String username,
      String password) {
    this.smtpServer = smtpServer;
    this.port = port;
    this.username = username;
    this.password = password;
  }
  
  /**
   * Envia um email.
   *
   * @param from Remetente
   * @param to Destinatário
   * @param subject Assunto
   * @param body Corpo
   * @param isHtml Se o corpo é HTML
   * @param attachments Anexos
   * @return true se o email foi enviado com sucesso
   */
  public boolean sendEmail(
      String from,
      String to,
      String subject,
      String body,
      boolean isHtml,
      List<String> attachments) {
    // Implementação
    return true;
  }
}
```

### Explicação Detalhada

1. **Formatação de Parâmetros**: Quando há muitos parâmetros, cada um está em sua própria linha, indentado adequadamente.

2. **Campos Finais**: Os campos são declarados como `final` quando apropriado, indicando que não serão alterados após a inicialização.

3. **Espaçamento entre Declarações**: Cada declaração de campo está em sua própria linha.

4. **Espaçamento após Vírgulas**: Há espaços após as vírgulas na lista de parâmetros.

5. **Espaçamento em Atribuições**: Há espaços em torno do operador de atribuição `=`.

6. **Documentação Javadoc**: A versão corrigida inclui documentação Javadoc para os métodos.

7. **Espaçamento entre Parâmetros e Generics**: Há um espaço entre o tipo genérico e o nome do parâmetro: `List<String> attachments` em vez de `List<String>attachments`.

A formatação adequada de parâmetros é especialmente importante para métodos com muitos parâmetros, tornando o código mais legível e facilitando a identificação de cada parâmetro.

## Conclusão

O Google Java Style Guide oferece diretrizes claras e abrangentes para escrever código Java consistente, legível e manutenível. Seguir estas diretrizes traz diversos benefícios:

1. **Consistência**: Todo o código segue o mesmo padrão, facilitando a leitura e compreensão.
2. **Legibilidade**: Código bem formatado é mais fácil de ler e entender.
3. **Manutenibilidade**: Padrões consistentes facilitam a manutenção a longo prazo.
4. **Colaboração**: Facilita o trabalho em equipe, pois todos seguem as mesmas convenções.
5. **Qualidade**: Código padronizado tende a ter menos bugs e problemas de design.

Os exemplos apresentados neste documento ilustram os principais aspectos do Google Java Style Guide, desde a formatação básica até práticas mais avançadas de design de código. Adotar estas práticas pode melhorar significativamente a qualidade do seu código Java e a produtividade da sua equipe.

Para mais informações, consulte a [documentação oficial do Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).
