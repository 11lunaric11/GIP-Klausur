# GIP-Klausur
# 1a) https://wahrheitstabelle.daug.de/#/tabelle
# 1b) (A ∧ (B ∨ C)) → D ≡ ¬(A ∧ (B ∨ C)) ∨ D  
≡ (¬A ∨ ¬(B ∨ C)) ∨ D  
≡ (¬A ∨ (¬B ∧ ¬C)) ∨ D
# UND
(A → B) → C ≡ ¬(A → B) ∨ C  
≡ ¬(¬A ∨ B) ∨ C  
≡ (A ∧ ¬B) ∨ C

# 1c)
Kreise:
int d(float x, float y) {
return a(x, y) && !( b(x, y) && c(x, y) );
}
Rechtecke:
return ( a(x,y) && !c(x,y) ) || ( !a(x,y) && b(x,y) );

# 2a)
https://www.matheretter.de/rechner/zahlenkonverter
# 2b) 
https://manderc.com/apps/umrechner/index.php
# 2c)
#include <stdio.h>

int main() {
    printf("Iteration | i | a | b | c\n");
    for (int i = 0; i < 5; ++i) {
        int a = i << 1; 
        int b = a & 0x06; 
        int c = b | 0x08;
        printf("%9d | %d | %d | %d | %d\n", i, i, a, b, c);
    }
    return 0;
}


#include <stdio.h>
int main() {
    for (int i = 0; i < 5; ++i) { 
        int a = i << 1; 
        int b = a | 0x0A; 
        int c = b & 0x0B; 
        printf(" i=%2d a=%2d b=%2d c=%2d\n", i, a, b, c); 
    }
    return 0;
}
