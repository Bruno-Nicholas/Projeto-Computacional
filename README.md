# 👨‍💻 Projeto Computacional
Projeto Computacional - Computação para Engenharia - Turma 01 - Professor Wesin Alves

# 📖 Membros do Grupo
➣ ***Alex*** (

➣ ***Bruno Nicholas Marques da Silva*** (Mat.: 242014435)

➣ ***Giovanna*** (

➣ ***Gisele*** (

➣ ***Mikael Vitor da Silva Leão*** (Mat.: 242014364)

# 💡 Introdução
Este é um código programado em linguagem C++ tendo como objetivo simular uma partida de jogo da velha entre duas pessoas. Armazenando o resultado de vitoria de cada jogador em um arquivo denominado pontuacoes.txt, desta forma possibilitando a comparação entre os jogadores mesmo jogando partidas em dias diferentes. O jogo só pode ser jogado com 2 jogadores localmente. O código foi completamente comentado a fim de ajudar na compreensão da forma como ele funciona.

# 🔥 Códigos Importantes

## Códigos iniciais
+ `#include <iostream>` - Biblioteca padrão do C++
+ `#include <fstream>` - Biblioteca para uso de arquivos
+ `using namespace std;` - Retirando a necessidade de incluir std::

## Infromações do jogo
```c_cpp
struct Jogodavelha {
char* tabuleiro; //ponteiro
char rodada; // X ou O
int pontuacaoDoX; // pontuação do jogador X
int pontuacaoDoO; // inicialização do O
};
```
Struct criada para armazenas as infromações do jogo.

## Inicializar o Jogo
```
void kumessarujogu(Jogodavelha& Jogodavelha) {
    Jogodavelha.tabuleiro = new char[9]{'1','2','3','4','5','6','7','8','9'};// alocação de memória para o tabuleiro
    //posições iniciadas 
    Jogodavelha.rodada = 'X'; // o x é o primeiro a jogar 
    Jogodavelha.pontuacaoDoX = 0; // pontuação do x
    Jogodavelha.pontuacaoDoO = 0; // pontuação do
    }
//procedimento que libera memória alocada
void liberarJogo(Jogodavelha& Jogodavelha) {
    delete[] Jogodavelha.tabuleiro; 
}
```
Função para inicializar o jogo e procedimento que libera a memória alocada

## Imprimindo o Tabuleiro
