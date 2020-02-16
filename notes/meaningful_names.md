# Meaningful Names
### Meaningful
1. Use Intention-Revealing Names   
2. Avoid Disinformation
3. Class Names   
Classes and objects should have noun or noun phrase names like Customer, WikiPage,
Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name
of a class. A class name should not be a verb.
4. Object Names   
Methods should have verb or verb phrase names like postPayment, deletePage, or save.
### Example
Bad code:
```java
private void printGuessStatistics(char candidate, int count) {
  String number;
  String verb;
  String pluralModifier;
  if (count == 0) {
    number = "no";
    verb = "are";
  pluralModifier = "s";
  } else if (count == 1) {
    number = "1";
    verb = "is";
    pluralModifier = "";
  } else {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
  }
  String guessMessage = String.format(
    "There %s %s %s%s", verb, number, candidate, pluralModifier
  );
  print(guessMessage);
}
```
clean code:
```java
public class GuessStatisticsMessage {
  private String number;
  private String verb;
  private String pluralModifier;
  public String make(char candidate, int count) {
    createPluralDependentMessageParts(count);
    return String.format(
    "There %s %s %s%s",
    verb, number, candidate, pluralModifier );
  }
  private void createPluralDependentMessageParts(int count) {
    if (count == 0) {
       thereAreNoLetters();
    } else if (count == 1) {
      thereIsOneLetter();
    } else {
      thereAreManyLetters(count);
    }
  }
  private void thereAreManyLetters(int count) {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
  }
  private void thereIsOneLetter() {
    number = "1";
    verb = "is";
    pluralModifier = "";
  }
   private void thereAreNoLetters() {
    number = "no";
    verb = "are";
    pluralModifier = "s";
  }
}
```
对比还是挺直观的
