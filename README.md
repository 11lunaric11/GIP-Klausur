# GIP1/INF1 Klausur - Kompletter Leitfaden mit Online-Tools

> **Wichtig:** Diese Vorlage basiert auf den Probeklausuren WS 2018/19 und WS 2019/20. Die echte Klausur folgt derselben Struktur mit 10 Aufgaben à 10 Punkte = 100 Punkte total. Bearbeitungszeit: 180 Minuten.

---

## 📋 Klausurstruktur

| Aufgabe | Thema | Punkte | Dauer (min) | Schwierigkeit |
|---------|-------|--------|------------|---------------|
| 1 | Logik & Boole'sche Algebra | 10 | 15-20 | Mittel |
| 2 | Zahlen & Bitoperationen | 10 | 15-20 | Mittel |
| 3 | Eingabe/Ausgabe (I/O) | 10 | 12-15 | Einfach |
| 4 | Funktionen & Parameter | 10 | 15-18 | Mittel |
| 5 | Zeichenketten & Arrays | 10 | 15-18 | Einfach |
| 6 | Rekursion | 10 | 20-25 | Schwer |
| 7 | Zeiger & Arithmetik | 10 | 18-22 | Schwer |
| 8 | Datenstrukturen (Structs) | 10 | 12-15 | Einfach |
| 9 | Container & Datenstrukturen | 10 | 15-18 | Mittel |
| 10 | Sortierverfahren | 10 | 15-18 | Mittel |

---

## 🎯 Aufgabe 1: Logik und Boole'sche Algebra

### Teilaufgabe 1a: Wahrheitstafeln (3 Punkte)

**Konzept:**
- Negation (¬A / Ā): Umkehrung des Wahrheitswerts
- Konjunktion (A ∧ B): Wahr nur wenn beide wahr
- Disjunktion (A ∨ B): Wahr wenn mindestens eine wahr
- Implikation (A ⇒ B): Falsch nur wenn A wahr und B falsch
- Äquivalenz (A ⇔ B): Wahr wenn beide gleich

**Beispiel Wahrheitstafel:**

| $A$ | $B$ | $\bar{A}$ | $\bar{B}$ | $A \wedge B$ | $A\vee B$ | $A \Rightarrow B$ | $A \Leftrightarrow B$ |
| --- | --- | --------- | --------- | ------------ | --------- | ----------------- | --------------------- |
| $F$ | $F$ | $W$       | $W$       | $F$          | $F$       | $W$               | $W$                   |
| $F$ | $W$ | $W$       | $F$       | $F$          | $W$       | $W$               | $F$                   |
| $W$ | $F$ | $F$       | $W$       | $F$          | $W$       | $F$               | $F$                   |
| $W$ | $W$ | $F$       | $F$       | $W$          | $W$       | $W$               | $W$                   |


**Online-Tool:** [Wahrheitstabelle](https://wahrheitstabelle.daug.de/#/tabelle)
- Eingabe: Boole'sche Ausdrücke
- Ausgabe: Automatisch generierte Wahrheitstafeln

---

### Teilaufgabe 1b: Algebraische Umformung (2 Punkte)

**Regeln:**
- `A ⇒ B` = `¬A ∨ B` (Implikation auflösen)
- `A ⇔ B` = `(A ⇒ B) ∧ (B ⇒ A)` = `(¬A ∨ B) ∧ (¬B ∨ A)`
- De Morgan: `¬(A ∧ B)` = `¬A ∨ ¬B`, `¬(A ∨ B)` = `¬A ∧ ¬B`

**Beispiel:**
```
(A ⇒ B) ⇔ C
= ((¬A ∨ B) ⇒ C) ⇔ C
= (¬(¬A ∨ B) ∨ C) ⇔ C
= ((A ∧ ¬B) ∨ C) ⇔ C
```

**Online-Tool:** [Symbolab Boolean Algebra](https://www.symbolab.com/solver/boolean-algebra-simplifier) oder [Circuit Sim](https://simulator.io/)

---

### Teilaufgabe 1c: Logische Funktionen kombinieren (5 Punkte)

**Strategie:**
1. Analysiere die Diagramme der Funktionen a(), b(), c()
2. Identifiziere: Wo sind die grauen (1er) Bereiche?
3. Kombiniere mit Operatoren: `&&`, `||`, `!`

**Beispiel-Analyse:**
- Funktion a(): Grau = obere rechte Ecke → `(x > 1) && (y > 1)`
- Funktion b(): Grau = linke Seite → `x < 1`
- Funktion c(): Grau = Kreis → `(x-1.5)*(x-1.5) + (y-1.5)*(y-1.5) < 0.5`

**Lösungsansatz für d():**
```c
int d(float x, float y) {
    return (a(x, y) && !b(x, y)) || (!a(x, y) && c(x, y));
}
```

**Online-Tool:** [Desmos Calculator](https://www.desmos.com/) - Visualisiere die Bereiche graphisch!

---

## 🔢 Aufgabe 2: Zahlen, Zahlendarstellungen, Bitoperationen

### Teilaufgabe 2a: Binärdarstellung (3 Punkte)

**Algorithmus für positive Zahlen:**
1. Dividiere die Zahl wiederholt durch 2
2. Merke die Reste (von unten nach oben)

**Beispiel: 20 in 8-Bit Binär**
```
20 ÷ 2 = 10 Rest 0
10 ÷ 2 = 5  Rest 0
5  ÷ 2 = 2  Rest 1
2  ÷ 2 = 1  Rest 0
1  ÷ 2 = 0  Rest 1

Ergebnis: 00010100
Prüfung: 0×2⁷ + 0×2⁶ + 0×2⁵ + 1×2⁴ + 0×2³ + 1×2² + 0×2¹ + 0×2⁰ = 16 + 4 = 20 ✓
```

**Online-Tool:** [Rapidtables Binary Converter](https://www.rapidtables.com/convert/number/decimal-to-binary.html)

---

### Teilaufgabe 2b: Zweierkomplement (2 Punkte)

**Für negative Zahlen:**
1. Binärdarstellung der positiven Zahl erzeugen
2. Alle Bits invertieren (0 → 1, 1 → 0)
3. 1 addieren

**Beispiel: -122 in 8-Bit Zweierkomplement**
```
Positive Zahl 122:
122 ÷ 2 = 61 Rest 0
61  ÷ 2 = 30 Rest 1
30  ÷ 2 = 15 Rest 0
15  ÷ 2 = 7  Rest 1
7   ÷ 2 = 3  Rest 1
3   ÷ 2 = 1  Rest 1
1   ÷ 2 = 0  Rest 1

122 = 01111010

Invertieren (Einserkomplement):
10000101

Eins addieren (Zweierkomplement):
10000101 + 1 = 10000110

Prüfung: -128 + 0 + 0 + 0 + 0 + 1 + 1 + 0 = -128 + 6 = -122 ✓
```

**Online-Tool:** [Twos Complement Calculator](https://www.rapidtables.com/convert/number/twos-complement.html)

---

### Teilaufgabe 2c: Bitoperationen in Schleifen (5 Punkte)

**Bitoperatoren:**
- `<<` (Linksshift): Multipliziert mit 2^n
- `>>` (Rechtsshift): Dividiert durch 2^n
- `&` (UND): Logisches AND bitweise
- `|` (ODER): Logisches OR bitweise
- `^` (XOR): Exclusive OR bitweise

**Schritt-für-Schritt-Lösung:**
```
Iteration i=0:
  a = 0 << 1 = 0 (0 × 2 = 0)
  b = 0 | 0x0A = 0 | 1010 = 1010 = 10
  c = 10 & 0x0B = 1010 & 1011 = 1010 = 10

Iteration i=1:
  a = 1 << 1 = 2 (1 × 2 = 2)
  b = 2 | 0x0A = 0010 | 1010 = 1010 = 10
  c = 10 & 0x0B = 1010 & 1011 = 1010 = 10

Iteration i=2:
  a = 2 << 1 = 4 (2 × 2 = 4)
  b = 4 | 0x0A = 0100 | 1010 = 1110 = 14
  c = 14 & 0x0B = 1110 & 1011 = 1010 = 10

Iteration i=3:
  a = 3 << 1 = 6
  b = 6 | 0x0A = 0110 | 1010 = 1110 = 14
  c = 14 & 0x0B = 1110 & 1011 = 1010 = 10

Iteration i=4:
  a = 4 << 1 = 8
  b = 8 | 0x0A = 1000 | 1010 = 1010 = 10
  c = 10 & 0x0B = 1010 & 1011 = 1010 = 10
```

| i | a | b | c |
|---|---|---|---|
| 0 | 0 | 10 | 10 |
| 1 | 2 | 10 | 10 |
| 2 | 4 | 14 | 10 |
| 3 | 6 | 14 | 10 |
| 4 | 8 | 10 | 10 |

**Online-Tool:** [Bitwise Calculator](https://www.rapidtables.com/calc/math/binary-calculator.html)

---

## 📥 Aufgabe 3: Eingabe und Ausgabe (I/O)

### Teilaufgabe 3a: Fließkommazahl einlesen (2 Punkte)

```c
#include <stdio.h>

int main() {
    float number;
    printf("Geben Sie eine Zahl ein: ");
    scanf("%f", &number);
    printf("Die eingelesene Zahl lautet: %.2f\n", number);
    return 0;
}
```

**Online-Tool:** [C Compiler](https://www.onlinegdb.com/) - Teste dein Code!

---

### Teilaufgabe 3b: Fließkommazahl ausgeben (3 Punkte)

```c
// Deklaration + Initialisierung + Ausgabe
float number = 3.14159;
printf("Die Zahl lautet: %f\n", number);

// Alternative mit Formatierung
printf("Die Zahl lautet: %.2f\n", number);  // 2 Dezimalstellen
```

---

### Teilaufgabe 3c: Bedingte Bitoperationen (5 Punkte)

```c
int num1, num2;
char operator;

// Eingabe
scanf("%d", &num1);
scanf("%d", &num2);
scanf(" %c", &operator);  // Beachte das Leerzeichen vor %c!

// Verarbeitung
if (operator == '&') {
    printf("%d\n", num1 & num2);
} else if (operator == '|') {
    printf("%d\n", num1 | num2);
} else {
    printf("Fehler: Ungültiger Operator\n");
}
```

**Online-Tool:** [OnlineGDB](https://www.onlinegdb.com/) - Teste mit verschiedenen Eingaben

---

## 🔧 Aufgabe 4: Funktionen

### Teilaufgabe 4a: Funktionssignatur (5 Punkte)

**Syntax für Funktionskopf:**
```c
char foo(int a, char* b, float array[5]);
```

**Erklärung:**
- Rückgabewert: `char`
- Parameter 1: `int a` (Ganzzahl)
- Parameter 2: `char* b` (Zeiger auf Zeichen = Adresse)
- Parameter 3: `float array[5]` (Array von 5 Floats)

---

### Teilaufgabe 4b: Funktionsparameter mit Zeigern (5 Punkte)

**Konzept:** Funktionen mit Ausgabe-Parametern via Zeiger

```c
// /* code A */ - Parameter der statistics Funktion
float* p_mean, float* p_std_dev

// /* code B */ - Werte in die Zeiger schreiben
*p_mean = mean_value;
*p_std_dev = std_dev_value;

// /* code C */ - Funktionsaufruf mit Adressen
statistics(numbers, 10, &mean, &std_dev);
```

**Erklärung:**
- `&mean` = Adresse der Variable `mean` (Zeiger)
- `*p_mean = ...` = Wert an der Adresse `p_mean` speichern (Dereferenzierung)

---

## 📝 Aufgabe 5: Zeichenketten und Arrays

### Teilaufgabe 5a: Stringlänge ohne strlen() (5 Punkte)

**Algorithmus:**
1. Iteriere über jeden Charakter
2. Zähle bis zur Null-Terminierung `\0`

```c
char string[] = "Dies ist die GIP1-Klausur.";
int length = 0;

// Methode 1: while-Schleife
while (string[length] != '\0') {
    length++;
}

// Methode 2: for-Schleife mit Zeigern
int length = 0;
char* ptr = string;
while (*ptr != '\0') {
    length++;
    ptr++;
}

printf("Länge: %d\n", length);  // Output: 26
```

**Online-Tool:** [OnlineGDB](https://www.onlinegdb.com/)

---

### Teilaufgabe 5b: Zweitgrößtes Element (5 Punkte)

**Algorithmus:**
1. Finde Maximum
2. Ersetze Maximum mit -∞
3. Finde neues Maximum = Zweitgrößtes

```c
float numbers[] = {8.8, 8.0, 4.9, 1.4, 9.4, 1.4, 9.7, 6.3, 3.3, 8.3};
int length = 10;

// Methode: Zwei Durchläufe
float max1 = numbers[0], max2 = -FLT_MAX;

for (int i = 0; i < length; i++) {
    if (numbers[i] > max1) {
        max2 = max1;
        max1 = numbers[i];
    } else if (numbers[i] > max2 && numbers[i] != max1) {
        max2 = numbers[i];
    }
}

printf("Zweitgrößtes: %.1f\n", max2);  // 9.4
```

---

## 🔁 Aufgabe 6: Rekursion

### Teilaufgabe 6a: Logistische Gleichung (5 Punkte)

**Rekursive Definition:**
```
x_{n+1} = r × x_n × (1 - x_n)
```

**C-Code:**
```c
float logmap(int n, float r, float x0) {
    // Basisfall
    if (n == 0) {
        return x0;
    }
    // Rekursiver Fall
    float x_prev = logmap(n - 1, r, x0);
    return r * x_prev * (1 - x_prev);
}

// Beispiel: logmap(5, 2.5, 0.5)
```

---

### Teilaufgabe 6b: Schneeflocken-Fraktal (5 Punkte)

**Rekursiver Ansatz:** Zeichne fraktale Muster durch wiederholte Muster

```c
void flake(int n, float step) {
    if (n == 0) {
        // Basisfall: Einfache Linie
        draw(1.0);
        move(-1.0);
        turn(120);
        draw(1.0);
        move(-1.0);
        turn(-240);
        draw(1.0);
        move(-1.0);
        turn(120);
    } else {
        // Rekursiver Fall: Vereinfachte Linie, dann fraktale Struktur
        flake(n - 1, step / 3);
        turn(-60);
        flake(n - 1, step / 3);
        turn(120);
        flake(n - 1, step / 3);
        turn(-60);
        flake(n - 1, step / 3);
    }
}
```

**Online-Tool:** [Recursion Visualizer](https://www.recursionvisualizer.com/)

---

## 🎯 Aufgabe 7: Zeiger

### Teilaufgabe 7a: Zeiger-Arithmetik (2 Punkte)

**Konzept:**
```
*(&array[i] + n) = array[i + n]
```

**Beispiel:**
```c
char characters[] = {'1', '2', '3', '4', '5', '6', '7', '8', '9'};
printf("%c\n", *(&characters[1] + 3));

// &characters[1] = Adresse von '2'
// &characters[1] + 3 = Adresse von '2' + 3 Positionen = Adresse von '5'
// *(...) = Dereferenzierung = '5'
// Output: 5
```

---

### Teilaufgabe 7b: Funktionszeiger (1 Punkt)

```c
// Definition
float (*foo)(int, int);

// Kompatible Funktion bar
float bar(int a, int b) {
    return a + b;
}

// Zuweisung
foo = bar;

// Aufruf
float result = foo(5, 3);  // = 8
```

---

### Teilaufgabe 7c: Swap-Funktionen (2 Punkte)

**swap_a: FALSCH** - Übergabe per Wert: Kopie wird getauscht, nicht Original
```c
void swap_a(int a, int b) {  // Kopien!
    int tmp = a;
    a = b;
    b = tmp;
}
```

**swap_b: RICHTIG** - Übergabe per Referenz: Zeiger auf Originale
```c
void swap_b(int* a, int* b) {  // Zeiger auf Originale
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```

---

### Teilaufgabe 7d: Array mit Zeiger-Arithmetik ausgeben (5 Punkte)

```c
char characters[] = {'1', '2', '3', '4', '5', '6', '7', '8', '9'};
char* ptr = characters;

// Methode 1: while-Schleife mit Inkrement
while (ptr < characters + 9) {
    printf("%c\n", *ptr);
    ptr++;
}

// Methode 2: for-Schleife
for (char* ptr = characters; ptr < characters + 9; ptr++) {
    printf("%c\n", *ptr);
}
```

---

## 📦 Aufgabe 8: Datenstrukturen (Structs)

### Teilaufgabe 8a: Struct mit Arrays (3 Punkte)

```c
typedef struct {
    float x[5];
    float y[5];
} Data;

Data data_instance;  // Variable erzeugen
```

---

### Teilaufgabe 8b: Struct-Felder initialisieren (2 Punkte)

```c
typedef struct {
    int day;
    int month;
    int year;
} Date;

Date today;
today.day = 21;
today.month = 1;
today.year = 2026;
```

---

### Teilaufgabe 8c: Nested Structs (5 Punkte)

```c
// Struct 1: Student
typedef struct {
    char name[76];  // max. 75 + \0
    int matrikelnumber;
} Student;

// Struct 2: Exam
typedef struct {
    Student student;
    char exam_order[50];  // Prüfungsordnung
} Exam;

// Variable mit Initialisierung
Exam my_exam = {
    {"Max Mustermann", 123456},
    "PO 2023"
};
```

**Online-Tool:** [Struct Visualizer](https://www.onlinegdb.com/)

---

## 🗂️ Aufgabe 9: Container und Datenstrukturen

### Teilaufgabe 9a: Dynamisches Array (3 Punkte)

**Mindestens erforderliche Informationen:**

| Information | Grund |
|---|---|
| **Daten-Zeiger** | Zeigt auf allokierten Speicher |
| **Länge (size)** | Aktuelle Anzahl der Elemente |
| **Kapazität (capacity)** | Reservierter Speicher / maximale Elemente |

```c
typedef struct {
    int* data;        // Zeiger auf dynamisches Array
    int size;         // Aktuelle Länge
    int capacity;     // Reservierte Größe
} DynamicArray;
```

---

### Teilaufgabe 9b: Element einfügen (bei Platz vorhanden) (3 Punkte)

**Schritte:**
1. Prüfe ob `size < capacity`
2. Platziere neues Element am Ende: `data[size] = new_element`
3. Erhöhe `size` um 1

```c
if (array.size < array.capacity) {
    array.data[array.size] = new_element;
    array.size++;
}
```

---

### Teilaufgabe 9c: Verkettete Liste mit O(1) Einfügen am Ende (2 Punkte)

**Erforderliche Informationen:**

| Information | Grund |
|---|---|
| **Head-Zeiger** | Zeigt auf erstes Element |
| **Tail-Zeiger** | Zeigt auf letztes Element = O(1) Zugriff! |
| **Node-Struktur** | Enthält Daten + next-Zeiger |

```c
typedef struct Node {
    int data;
    struct Node* next;
} Node;

typedef struct {
    Node* head;  // Zeiger auf Anfang
    Node* tail;  // Zeiger auf Ende = ermöglicht O(1) Einfügen!
} LinkedList;
```

---

### Teilaufgabe 9d: Element in doppelt verketteter Liste einfügen (2 Punkte)

**Schritte:**
1. Erzeuges neues Node-Element
2. Setze `new->next = current->next`
3. Setze `new->prev = current`
4. Setze `current->next->prev = new`
5. Setze `current->next = new`

```c
Node* new_node = malloc(sizeof(Node));
new_node->next = current->next;
new_node->prev = current;
current->next->prev = new_node;
current->next = new_node;
```

---

## 🔀 Aufgabe 10: Sortierverfahren

### Teilaufgabe 10a: Komplexitäten zuordnen (5 Punkte)

| Verfahren | Beste Zeit | Durchschnittliche Zeit | Schlechteste Zeit | Speicher |
|-----------|-----------|----------------------|-------------------|----------|
| **Bubblesort** | O(n) | **O(n²)** | O(n²) | O(1) |
| **Selectionsort** | **O(n²)** | **O(n²)** | O(n²) | O(1) |
| **Insertionsort** | O(n) | **O(n²)** | O(n²) | O(1) |
| **Mergesort** | **O(n log n)** | **O(n log n)** | O(n log n) | O(n) |
| **Quicksort** | **O(n log n)** | **O(n log n)** | O(n²) | O(log n) |

---

### Teilaufgabe 10b: Selectionsort Visualisierung (2 Punkte)

**Liste:** 9 8 5 10 4 3 2 7

```
Start:        9  8  5  10 4  3  2  7

1. Tausch:    2  8  5  10 4  3  9  7    (2 <-> 9, kleinste nach vorne)
2. Tausch:    2  3  5  10 4  8  9  7    (3 <-> 8)
3. Tausch:    2  3  4  10 5  8  9  7    (4 <-> 5)
```

**Online-Tool:** [Sorting Algorithm Visualizer](https://www.sorting-algorithms.com/)

---

### Teilaufgabe 10c: Mergesort Rekursionsebenen (3 Punkte)

**Liste:** 9 8 5 10 4 3 2 7

```
Rekursionsebene 0 (Anfang):
[9] [8] [5] [10] [4] [3] [2] [7]

Ebene 1 (nach erstem Merge):
[8,9] [5,10] [3,4] [2,7]

Ebene 2 (nach zweitem Merge):
[5,8,9,10] [2,3,4,7]

Ebene 3 (finales Merge):
[2,3,4,5,7,8,9,10]
```

---

## ⏱️ Klausur-Zeitplan (180 Minuten)

| Aufgabe | Empfohlene Zeit | Kumulative Zeit |
|---------|-----------------|-----------------|
| 1 | 18 min | 18 min |
| 2 | 18 min | 36 min |
| 3 | 13 min | 49 min |
| 4 | 16 min | 65 min |
| 5 | 16 min | 81 min |
| 6 | 22 min | 103 min |
| 7 | 20 min | 123 min |
| 8 | 13 min | 136 min |
| 9 | 16 min | 152 min |
| 10 | 16 min | 168 min |
| **Puffer/Kontrolle** | **12 min** | **180 min** |

---

## 🌐 Empfohlene Online-Tools für die Klausur

### Für alle Aufgaben

| Tool | Link | Nutzen |
|------|------|--------|
| **OnlineGDB** | https://www.onlinegdb.com/ | C-Code kompilieren & testen |
| **Compiler Explorer** | https://godbolt.org/ | Assembly-Code ansehen |
| **C-Dokumentation** | https://cppreference.com/ | Syntax nachschlagen |

### Nach Aufgabe

| Aufgabe | Tool | Link |
|---------|------|------|
| 1 | Truth Table Generator | https://www.truetable.net/ |
| 1c | Desmos Graphing | https://www.desmos.com/ |
| 2a,2b | Binary Converter | https://www.rapidtables.com/convert/number/decimal-to-binary.html |
| 2c | Bit Calculator | https://www.rapidtables.com/calc/math/binary-calculator.html |
| 3 | OnlineGDB | https://www.onlinegdb.com/ |
| 4 | OnlineGDB | https://www.onlinegdb.com/ |
| 5 | OnlineGDB | https://www.onlinegdb.com/ |
| 6 | Recursion Visualizer | https://www.recursionvisualizer.com/ |
| 7 | Pointer Visualizer | https://www.onlinegdb.com/ |
| 8 | Struct Visualizer | https://www.onlinegdb.com/ |
| 9 | Data Structure Visualizer | https://www.cs.usfca.edu/~galles/visualization/Algorithms.html |
| 10 | Sorting Visualizer | https://www.sorting-algorithms.com/ |

---

## 📌 Kritische Fehlerquellen

| Fehler | Vermeidung |
|--------|-----------|
| **Stringlänge falsch** | Nicht vergessen: `\0` ist nicht enthalten in der Länge! |
| **Swap-Funktion falsch** | Zeiger verwenden (`int*`), nicht Werte (`int`) |
| **Sizeof falsch** | `sizeof(char*) = 8` (Adresse), nicht `sizeof(char) = 1` |
| **Array vs. Zeiger** | Arrays zerfallen zu Zeiger in Funktionen! |
| **Speicherleck** | Immer `malloc` mit `free` paaren |
| **Bitoperationen** | Hexadezimal korrekt konvertieren: `0x0A = 1010` |
| **Rekursion Basisfall** | Basisfall MUSS vorhanden sein, sonst Stack Overflow |
| **Struct Initialisierung** | Reihenfolge der Felder beachten! |

---

## 💡 Allgemeine Tipps

✅ **Mach das:**
- Schreibe kleine Test-Programme für komplexe Aufgaben
- Nutze Online-Tools zur Validierung
- Visualisiere Probleme (Diagramme, Wahrheitstafeln)
- Beginne mit einfachen Aufgaben (3, 5, 8)
- Lese die Aufgabenstellung 2x durch
- Schreibe pseudocode, bevor du C-Code schreibst

❌ **Vermeide das:**
- Funktionen ohne Rückgabe schreiben
- Zeiger ohne `&` oder `*` verwenden
- Schleifen ohne Abbruchbedingung schreiben
- Speicher allokieren ohne freizugeben
- Auf Grenzen von Arrays vergessen

---

## 🎓 Lernressourcen

- **C-Referenz:** https://www.cppreference.com/w/c/
- **Visualisierungen:** https://www.cs.usfca.edu/~galles/visualization/
- **Übungsaufgaben:** OnlineGDB mit den Probeklausuren durcharbeiten
- **Dokumentation:** `man printf`, `man scanf` im Terminal

---

## 📊 Punkteverteilung Strategie

```
Leicht (sollte man kriegen):  Aufgaben 3, 5, 8       = 30 Punkte
Mittel (mit Übung):         Aufgaben 1, 2, 4, 9, 10 = 50 Punkte
Schwer (Bonus):             Aufgaben 6, 7           = 20 Punkte

Mindestens 50-60 Punkte sollten realistisch sein mit guter Vorbereitung!
```

---

## 🚀 Finale Checkliste vor der Klausur

- [ ] OnlineGDB Browser-Tab offen
- [ ] Binary Converter Tab offen
- [ ] Sorting Visualizer Tab offen
- [ ] C-Referenz Tab offen
- [ ] Wasser/Getränk vorhanden
- [ ] Zettel + Stift vorhanden
- [ ] Ruhe bewahren - du schaffst das! 💪

---

**Viel Erfolg bei deiner GIP1/INF1 Klausur! 🎯**

*Basiert auf Probeklausuren WS 2018/19 und WS 2019/20 von Prof. Dr. Tom Vierjahn*
