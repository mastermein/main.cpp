#include<iostream>

/* Prototypes des fonctions */

size_t LongueurChaine(const char* chaine);

void CopierChaine(char* destination, const char* source);

void ConcatenerChaines(char* destination, const char* source);

char* TrouverCaractere(const char* chaine, char caractere);

size_t CompterOccurrences(const char* chaine, char caractere);

void CopierMemoire(void* destination, const void* source, size_t taille);

void InitialiserMemoire(void* zone, unsigned char valeur, size_t taille);

void ExtraireSousChaine(char* destination, const char* source,  size_t debut, size_t longueur);

size_t DiviserChaine(const char* chaine, char separateur, char resultat[][100], size_t max_resultats);

int ComparerChaines(const char* chaine1, const char* chaine2);

void ConvertirMinuscules(char* chaine);

bool EstChaineNumerique(const char* chaine);

int main()
{
  std::cout << "=== TEST DES FONCTIONS DE MANIPULATION DE CHAINES STYLE C ===" << std::endl;
    std::cout << "Compile avec C++ et CLang++" << std::endl << std::endl;
    
    // Test 1: Longueur de chaîne
    char message[] = "Bonjour le monde";
    std::cout << "1. Longueur de '" << message << "': " << LongueurChaine(message) << std::endl;
    
    // Test 2: Copie de chaîne
    char copie[50];
    CopierChaine(copie, message);
    std::cout << "2. Copie: '" << copie << "'" << std::endl;
    
    // Test 3: Concatenation
    char salutation[100] = "Hello ";
    ConcatenerChaines(salutation, "World!");
    std::cout << "3. Concatenation: '" << salutation << "'" << std::endl;
    
    // Test 4: Recherche de caractere
    char* position = TrouverCaractere(message, 'j');
    if (position != nullptr) {
        std::cout << "4. Caractere 'j' trouve a la position: " << (position - message) << std::endl;
    } else {
        std::cout << "4. Caractere 'j' non trouve" << std::endl;
    }
    
    // Test 5: Comptage d'occurrences
    std::cout << "5. Occurrences de 'o' dans '" << message << "': " 
              << CompterOccurrences(message, 'o') << std::endl;
    
    // Test 6: Extraction de sous-chaine
    char sous_chaine[20];
    ExtraireSousChaine(sous_chaine, message, 3, 5);
    std::cout << "6. Sous-chaine (pos 3, longueur 5): '" << sous_chaine << "'" << std::endl;
    
    // Test 7: Division de chaine
    char phrase[] = "pomme,orange,banane,kiwi";
    char fruits[10][100];
    size_t nb_fruits = DiviserChaine(phrase, ',', fruits, 10);
    
    std::cout << "7. Division de '" << phrase << "':" << std::endl;
    for (size_t i = 0; i < nb_fruits; i++) {
        std::cout << "   [" << i << "] " << fruits[i] << std::endl;
    }
    
    // Test 8: Fonctions memoire
    char zone1[10] = "ABCDEFGHI";
    char zone2[10];
    CopierMemoire(zone2, zone1, 5);
    zone2[5] = '\0';
    std::cout << "8. Copie memoire (5 octets): '" << zone2 << "'" << std::endl;
    
    char zone3[10];
    InitialiserMemoire(zone3, 'X', 5);
    zone3[5] = '\0';
    std::cout << "9. Initialisation memoire: '" << zone3 << "'" << std::endl;
    
    // Test 10: Comparaison de chaînes
    char chaineA[] = "apple";
    char chaineB[] = "banana";
    int resultat_comparaison = ComparerChaines(chaineA, chaineB);
    std::cout << "10. Comparaison '" << chaineA << "' vs '" << chaineB << "': " 
              << resultat_comparaison << std::endl;
    
    // Test 11: Conversion minuscules
    char mixte[] = "Hello World!";
    std::cout << "11. Avant conversion: '" << mixte << "'" << std::endl;
    ConvertirMinuscules(mixte);
    std::cout << "    Apres conversion: '" << mixte << "'" << std::endl;
    
    // Test 12: Vérification numérique
    char numerique[] = "12345";
    char non_numerique[] = "12a45";
    std::cout << "12. '" << numerique << "' est numerique: " 
              << (EstChaineNumerique(numerique) ? "OUI" : "NON") << std::endl;
    std::cout << "    '" << non_numerique << "' est numerique: " 
              << (EstChaineNumerique(non_numerique) ? "OUI" : "NON") << std::endl;
    
    return 0;

}
// Initialisation des fonctions 

size_t LongueurChaine(const char* chaine) {
    int i=0;
    while (chaine[i] != '\0') {
        i++;
    }
    return i;
}


void CopierChaine(char* destination, const char* source) {
    int i = 0;
    while (source[i] != '\0') {
        destination[i] = source[i];
        i++;
    }
    destination[i] = '\0';
}


void ConcatenerChaines(char* destination, const char* source) {
    int taille = LongueurChaine(destination);
    int i = 0;
    while (source[i] != '\0') {
        destination[taille + i] = source[i];
        i++;
    }
    destination[taille + i] = '\0';
}


char* TrouverCaractere(const char* chaine, char caractere) {
    for (int i = 0; chaine[i] != '\0'; i++) {
        if (chaine[i] == caractere) {
            return (char*)(chaine + i);
        }
    }
    return nullptr;
}

size_t CompterOccurrences(const char* chaine, char caractere) {
    size_t count = 0;
    for (size_t i = 0; chaine[i] != '\0'; i++) {
        if (chaine[i] == caractere) {
            count++;
        }
    }
    return count;
}

void CopierMemoire(void* destination, const void* source, size_t taille) {
    char* dest = (char*)destination;
    const char* src = (const char*)source;
    for (size_t i = 0; i < taille; i++) {
        dest[i] = src[i];
    }
}

void InitialiserMemoire(void* zone, unsigned char valeur, size_t taille) {
    char* ptr = (char*)zone;
    for (size_t i = 0; i < taille; i++) {
        ptr[i] = valeur;
    }
}

void ExtraireSousChaine(char* destination, const char* source, size_t debut, size_t longueur) {
    size_t i;
    for (i = 0; i < longueur && source[debut + i] != '\0'; i++) {
        destination[i] = source[debut + i];
    }
    destination[i] = '\0';
}

size_t DiviserChaine(const char* chaine, char separateur, char resultat[][100], size_t max_resultats) {
    size_t compteur = 0;
    size_t index_courant = 0;
    size_t i = 0;
    
    while (chaine[i] != '\0' && compteur < max_resultats) {
        if (chaine[i] == separateur) {
            resultat[compteur][index_courant] = '\0';
            compteur++;
            index_courant = 0;
        } else {
            resultat[compteur][index_courant] = chaine[i];
            index_courant++;
        }
        i++;
    }
    
    // Dernier élément
    if (index_courant > 0 && compteur < max_resultats) {
        resultat[compteur][index_courant] = '\0';
        compteur++;
    }
    
    return compteur;
}

int ComparerChaines(const char* chaine1, const char* chaine2) {
    size_t i = 0;
    while (chaine1[i] != '\0' && chaine2[i] != '\0') {
        if (chaine1[i] != chaine2[i]) {
            return chaine1[i] - chaine2[i];
        }
        i++;
    }
    return chaine1[i] - chaine2[i];
}

void ConvertirMinuscules(char* chaine) {
    for (size_t i = 0; chaine[i] != '\0'; i++) {
        chaine[i] = tolower(chaine[i]);
    }
}

bool EstChaineNumerique(const char* chaine) {
    for (size_t i = 0; chaine[i] != '\0'; i++) {
        if (!isdigit(chaine[i])) {
            return false;
        }
    }
    return true;
}
