#include <stdio.h>
#include <string.h>
#include <ctype.h> //biblioteca das detecções de letras maiusculas e minusculas

#define ALFABETO 26 // define a palavra ALFABETO como 26 caracteres de 0 a 25 / de A a Z


void gerarCesarAlfabeto(char cesar[], int shift) {
    for(int i = 0; i < ALFABETO; i++) {
        cesar[i] = 'A' + (i + shift) % ALFABETO; //aplica a cifra de cesar pelo shift escolhido
    }
}


void embaralharAlfabeto(char cesar[], char embaralhado[], int pa) {
    for(int i = 0; i < ALFABETO; i++) {
        int novoIndice = (i + pa * (i + 1)) % ALFABETO; 
        embaralhado[i] = cesar[novoIndice]; //embaralha a cifra de cesar de acordo com a progressão aritimética definida
    }
}


void criptografar(char palavra[], char embaralhado[]) {
    int tamanho = strlen(palavra); //identifica o quantidade de letras da palavras 
    for(int i = 0; i < tamanho; i++) {
        if(isupper((unsigned char)palavra[i])) {
            int indice = palavra[i] - 'A';
            palavra[i] = embaralhado[indice]; //identifica se a palavra esta em MAIUSCULA
        }
        else if(islower((unsigned char)palavra[i])) {
            int indice = palavra[i] - 'a';
            palavra[i] = tolower(embaralhado[indice]); //identifica se a palavra esta em MINUSCULA
        }
    }
}

int main() {
    char palavra[15];
    int shift, pa;
    char cesar[ALFABETO];
    char embaralhado[ALFABETO];

    printf("Digite uma palavra (apenas letras): ");
    scanf("%99s", palavra);

    printf("Digite o shift da Cifra de Cesar: ");
    scanf("%d", &shift);

    printf("Digite o valor da PA para embaralhar o alfabeto: ");
    scanf("%d", &pa);

  
    gerarCesarAlfabeto(cesar, shift);

  
    embaralharAlfabeto(cesar, embaralhado, pa);


    criptografar(palavra, embaralhado);

    printf("\nPalavra criptografada: %s\n", palavra);

  

    return 0;
}
