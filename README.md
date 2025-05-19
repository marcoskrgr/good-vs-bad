# Comparação de Código Java: Sem vs Com Google Java Style Guide

Este documento apresenta 15 exemplos comparativos de código Java, mostrando a versão sem seguir o Google Java Style Guide e a versão corrigida seguindo as diretrizes do guia.

## Exemplo 1: Indentação e Nomenclatura

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

## Exemplo 2: Organização de Imports

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

## Exemplo 3: Formatação de Chaves e Espaçamento

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

## Exemplo 4: Nomenclatura

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

## Exemplo 5: Comentários

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

## Exemplo 6: Métodos Longos vs. Métodos Focados

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

## Exemplo 7: Documentação Javadoc

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

## Exemplo 8: Estruturas Condicionais

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

## Exemplo 9: Comprimento de Linhas

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

## Exemplo 10: Declarações Múltiplas

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

## Exemplo 11: Uso de Chaves em Estruturas Condicionais

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

## Exemplo 12: Formatação de Switch-Case

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

## Exemplo 13: Nomenclatura de Métodos e Constantes

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

## Exemplo 14: Uso de Modificadores

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

## Exemplo 15: Formatação de Parâmetros

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
