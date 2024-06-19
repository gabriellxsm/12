#include <stdio.h>
#include <stdlib.h>

 NUM_ALUNOS 5
 NUM_NOTAS 4

typedef struct {
    char nome[50];
    float notas[NUM_NOTAS];
    float media;
    char resultado[20];
} Aluno;

void menu() {
    printf("\n--- Sistema de Gestao de Notas de Alunos ---\n");
    printf("1. Cadastrar Alunos\n");
    printf("2. Atribuir Notas\n");
    printf("3. Exibir Resultados\n");
    printf("4. Editar Resultados\n");
    printf("5. Sair\n");
}

void cadastrarAlunos(Aluno alunos[]) {
    for (int i = 0; i < NUM_ALUNOS; i++) {
        printf("Digite o nome do aluno %d: ", i + 1);
        scanf(" %[^\n]%*c", alunos[i].nome);
    }
}

void atribuirNotas(Aluno alunos[]) {
    for (int i = 0; i < NUM_ALUNOS; i++) {
        printf("Atribuindo notas para %s\n", alunos[i].nome);
        for (int j = 0; j < NUM_NOTAS; j++) {
            do {
                printf("Nota %d (0 a 10): ", j + 1);
                scanf("%f", &alunos[i].notas[j]);
            } while (alunos[i].notas[j] < 0 || alunos[i].notas[j] > 10);
        }
    }
}

void calcularResultados(Aluno alunos[]) {
    for (int i = 0; i < NUM_ALUNOS; i++) {
        float total = 0;
        for (int j = 0; j < NUM_NOTAS; j++) total += alunos[i].notas[j];
        alunos[i].media = total / NUM_NOTAS;
        if (alunos[i].media < 4) sprintf(alunos[i].resultado, "Reprovado");
        else if (alunos[i].media < 6) sprintf(alunos[i].resultado, "Recuperacao");
        else sprintf(alunos[i].resultado, "Aprovado");
    }
}

void exibirResultados(Aluno alunos[]) {
    for (int i = 0; i < NUM_ALUNOS; i++) {
        printf("Aluno: %s\n", alunos[i].nome);
        printf("Notas: ");
        for (int j = 0; j < NUM_NOTAS; j++) printf("%.2f ", alunos[i].notas[j]);
        printf("\nMedia: %.2f\nResultado: %s\n\n", alunos[i].media, alunos[i].resultado);
    }
}

void editarResultados(Aluno alunos[]) {
    int indice;
    printf("Digite o numero do aluno (1 a %d): ", NUM_ALUNOS);
    scanf("%d", &indice);
    indice--;
    for (int j = 0; j < NUM_NOTAS; j++) {
        do {
            printf("Nova nota %d (0 a 10): ", j + 1);
            scanf("%f", &alunos[indice].notas[j]);
        } while (alunos[indice].notas[j] < 0 || alunos[indice].notas[j] > 10);
    }
}

int main() {
    Aluno alunos[NUM_ALUNOS];
    int opcao;

    while (1) {
        menu();
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1: cadastrarAlunos(alunos); break;
            case 2: atribuirNotas(alunos); calcularResultados(alunos); break;
            case 3: exibirResultados(alunos); break;
            case 4: editarResultados(alunos); calcularResultados(alunos); break;
            case 5: exit(0);
            default: printf("Opcao invalida! Tente novamente.\n");
        }
    }
    return 0;
}
