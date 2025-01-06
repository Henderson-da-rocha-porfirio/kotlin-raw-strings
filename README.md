# Raw Strings

Vamos analisar o conceito de **raw strings** em **Kotlin** em comparação com Java, usando o código fornecido como base. O objetivo é entender como o Kotlin simplifica a manipulação de strings multilinha e formatadas, enquanto o Java requer abordagens alternativas.

---

## **1. Raw Strings no Kotlin**

### **Características de Raw Strings:**
1. **Uso de `"""`**:
   - Strings brutas são delimitadas por três aspas (`"""`) e podem conter múltiplas linhas sem a necessidade de escape.
   - Ideal para texto formatado ou multilinha.

2. **Interpolação Suportada:**
   - Mesmo em raw strings, é possível usar interpolação com `$` e `${}`.

3. **Controle de Margem:**
   - O método `trimMargin()` pode ser usado para remover margens definidas com o caractere `|` (ou outro caractere especificado).

---

### **Exemplo no Código Kotlin**

```kotlin
val nurseryRhyme = """$eggName Dumpty sat on the wall
                      |$eggName Dumpty had a great fall
                      |All the king's horses and all the king's men
                      |Couldn't put $eggName together again.""".trimMargin()
println(nurseryRhyme)
```

- **Raw String Multilinha:**
  - O texto pode ser escrito diretamente em múltiplas linhas sem caracteres de escape.
  - `$eggName` é interpolado em todas as linhas.

- **Uso de `trimMargin()`:**
  - Remove as margens definidas pelo caractere `|`, garantindo que a indentação não afete a saída.

---

### **Saída Gerada no Kotlin**
```
Humpty Dumpty sat on the wall
Humpty Dumpty had a great fall
All the king's horses and all the king's men
Couldn't put Humpty together again.
```

---

## **2. Como Fazer Isso em Java**

Java não possui suporte nativo para raw strings. Para manipular strings multilinha ou formatadas, é necessário:

1. **Usar Concatenação de Strings:**
   - Multiplas strings são concatenadas linha a linha com o operador `+`.

2. **Usar Strings Literais de Múltiplas Linhas (a partir do Java 13):**
   - Java introduziu **text blocks** (`"""`) a partir do **Java 13**, que oferecem suporte similar ao raw string do Kotlin.

---

### **Equivalente em Java (Antes do Java 13)**

```java
public class Main {
    public static void main(String[] args) {
        String eggName = "Humpty";
        String nurseryRhyme = eggName + " Dumpty sat on the wall\n" +
                              eggName + " Dumpty had a great fall\n" +
                              "All the king's horses and all the king's men\n" +
                              "Couldn't put " + eggName + " together again.";
        System.out.println(nurseryRhyme);
    }
}
```

- **Concatenação Manual:**
  - Exige o uso de `+` para cada linha.
  - Interpolação deve ser feita manualmente com concatenação.

---

### **Equivalente em Java (Com Text Blocks - Java 13+)**

```java
public class Main {
    public static void main(String[] args) {
        String eggName = "Humpty";
        String nurseryRhyme = """
            %s Dumpty sat on the wall
            %s Dumpty had a great fall
            All the king's horses and all the king's men
            Couldn't put %s together again.
            """.formatted(eggName, eggName, eggName);

        System.out.println(nurseryRhyme);
    }
}
```

- **Text Blocks (`"""`):**
  - Introduzido no Java 13, text blocks eliminam a necessidade de concatenar strings manualmente.
  - **Formatação (`.formatted`)**:
    - Substitui placeholders `%s` pelos valores desejados.
    - Sem interpolação direta como no Kotlin.

---

## **3. Diferenças Entre Kotlin e Java**

| Aspecto                   | Kotlin                                         | Java (Antes do Java 13)                  | Java (Com Text Blocks)                   |
|---------------------------|-----------------------------------------------|-----------------------------------------|------------------------------------------|
| **Multilinha**            | Suporte nativo com `"""`.                     | Concatenar strings com `+`.             | Suporte nativo com `"""`.                |
| **Interpolação**          | Suporte direto com `$` e `${}`.               | Feito manualmente com concatenação.     | Feito com placeholders (`%s`) e `.formatted`. |
| **Remoção de Margem**     | `trimMargin()` remove indentação.             | Não há equivalente direto.              | Não há equivalente direto.               |
| **Legibilidade**          | Muito mais legível e conciso.                 | Propenso a erros e repetitivo.          | Legibilidade similar ao Kotlin.          |
| **Lançamento**            | Disponível desde o início do Kotlin.          | Requer versões anteriores a Java 13.    | Disponível a partir do Java 13.          |

---

## **4. Vantagens do Kotlin**

1. **Simplicidade e Concisão:**
   - A sintaxe com `"""` e interpolação direta faz com que o código seja mais limpo e fácil de entender.

2. **Trim de Margens:**
   - O método `trimMargin()` permite manipular a indentação de maneira mais flexível, o que é útil para manter a estrutura visual do código.

3. **Interpolação Direta:**
   - O uso de `$` e `${}` para interpolação elimina a necessidade de placeholders ou métodos adicionais.

4. **Independência de Versão:**
   - Funcionalidade disponível em todas as versões do Kotlin, enquanto o suporte equivalente em Java (text blocks) é limitado a partir do Java 13.

---

## **5. Exemplo Comparativo**

### **Kotlin**
```kotlin
val eggName = "Humpty"
val nurseryRhyme = """$eggName Dumpty sat on the wall
                      |$eggName Dumpty had a great fall
                      |All the king's horses and all the king's men
                      |Couldn't put $eggName together again.""".trimMargin()
println(nurseryRhyme)
```

### **Java (Com Text Blocks)**
```java
String eggName = "Humpty";
String nurseryRhyme = """
    %s Dumpty sat on the wall
    %s Dumpty had a great fall
    All the king's horses and all the king's men
    Couldn't put %s together again.
    """.formatted(eggName, eggName, eggName);

System.out.println(nurseryRhyme);
```

---

## **6. Saída Gerada**

Em ambos os casos (Kotlin e Java), a saída será:

```
Humpty Dumpty sat on the wall
Humpty Dumpty had a great fall
All the king's horses and all the king's men
Couldn't put Humpty together again.
```

---

## **Resumo**

- **Kotlin** é mais intuitivo e direto para trabalhar com strings multilinha e interpolação, sem necessidade de métodos auxiliares.
- **Java** com text blocks (a partir do Java 13) se aproxima da flexibilidade do Kotlin, mas ainda requer métodos adicionais para interpolação.
- Se você precisa de strings multilinha e interpolação simples, Kotlin oferece a melhor experiência de uso e legibilidade.
