# 👨‍💻 Projeto Computacional
**Projeto Computacional - Computação para Engenharia - Turma 01 - Professor Wesin Alves**

# 📖 Membros do Grupo
➣ ***Alex*** (

➣ ***Bruno Nicholas Marques da Silva*** (Mat.: 242014435)

➣ ***Giovanna*** (

➣ ***Gisele*** (

➣ ***Mikael Vitor da Silva Leão*** (Mat.: 242014364)

# 💡 Introdução
Este é um código programado em linguagem C++ tendo como objetivo **simular uma partida de jogo da velha entre duas pessoas**. Armazenando o resultado de vitória de cada jogador em um arquivo denominado **pontuacoes.txt**, desta forma possibilitando a comparação entre os jogadores **mesmo jogando partidas em dias diferentes**. O jogo só pode ser jogado **com 2 jogadores** localmente. O código foi completamente comentado a fim de ajudar na compreensão da forma como ele funciona.

# 🔥 Códigos Importantes

## Códigos Iniciais:
+ `#include <iostream>` - Biblioteca padrão do C++.
+ `#include <fstream>` - Biblioteca para uso de arquivos.
+ `using namespace std;` - Retirando a necessidade de incluir std:: em todos os linhas.

## Infromações do Jogo:
```cpp
struct Jogodavelha {
char* tabuleiro; //ponteiro
char rodada; // X ou O
int pontuacaoDoX; // pontuação do jogador X
int pontuacaoDoO; // inicialização do O
};
```
Struct criada para **armazenar as infromações do jogo**.

## Inicializar o Jogo:
```cpp
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
Função para **inicializar o jogo** e procedimento que **libera a memória alocada**.

## Imprimir o Tabuleiro:
```cpp
void printabuleiro(const Jogodavelha& Jogodavelha) {
    for (int i = 0; i < 9; ++i) 
    {
        cout << Jogodavelha.tabuleiro[i];
        if (i % 3 == 2) {
            cout << endl;
            } else{cout << " | ";} 
    if (i % 3 == 2 && i < 8) cout << "---------\n";
    } // tem que ser múiplo de 3 pois o tabuleiro é de 3x3, então se for multiplo de 3 é pq está no final da linha por isso imprimimos "endl";
}
```
Procedimento que **imprime o tabuleiro do jogo**.

## Verificando Quem Ganhou ou Teve Empate:
```cpp
// função que verifica quem ganhou e retorna um valor booleano
bool verificarVitoria(const Jogodavelha& Jogodavelha){
char(*t)[3] = (char(*)[3]) Jogodavelha.tabuleiro; // comando que reiterpreta o tabuleiro como uma matriz 3x3
// t é um ponteiro que aponta para o tabuleiro com 3 colunas
// meio que uma array de 3 elementos, mas iso é meio que declarado implicitamente pois não temos o valor de t ainda
    for (int i = 0; i < 3; ++i)// aqui o valor de t é meio que declarado implicitamente como sendo 3
        if ((t[i][0] == t[i][1] && t[i][1] == t[i][2]) || (t[0][i] == t[1][i] && t[1][i] == t[2][i]))// verifica se as linhas são iguais ou as colunas 
            return true;
    return (t[0][0] == t[1][1] && t[1][1] == t[2][2]) || (t[0][2] == t[1][1] && t[1][1] == t[2][0]); //verifica as diagonais
    //aqui o ponteiro foi um pouco complicado mas não está errado, ele é um ponteiro que aponta para o tabuleiro com 3 colunas
}
//função que verifica empate
bool verificarEmpate(const Jogodavelha& Jogodavelha) {
    for (int i = 0; i < 9; ++i)
        if (Jogodavelha.tabuleiro[i] != 'X' && Jogodavelha.tabuleiro[i] != 'O') return false; //se ainda estiver espaço vazio, não é empate
    return true; //não tem espaço vazio, então é empate
}
```
Função que **verifica quem ganhou e se houve empate na partida**.

## Armazenamento de Pontuação:
```cpp
void guardapontuacao(const Jogodavelha& Jogodavelha) {
    ofstream arquivo("pontuacoes.txt");//ofstream é a classe que permite escrever em arquivos 
    //ela faz parte da biblioteca fstream, foi por conta disso que incluímos a biblioteca fstream
    arquivo << "Jogador X - Pontuação: " << Jogodavelha.pontuacaoDoX << "\n"; // pontuação no arquivo
    arquivo << "Jogador O - Pontuação: " << Jogodavelha.pontuacaoDoO << "\n"; 
    arquivo.close(); //salva a pontuação no arquivo e fecha
    //no código, a função guarda pontuação escreve em um arquivo o resultado do jogo que acabou de ser jogado 
    // ela não acumula pontuações, apenas registra a vitoria(1), e a derrota(0). 
}
```
Procedimento para **criar o arquivo de armazenamento da pontuação**.

## Rodando o Jogo:
```cpp
void jogujogu(Jogodavelha& Jogodavelha) {
int escolha; // posição que o jogador escolhe no tabuleito
    while (!verificarVitoria(Jogodavelha) && !verificarEmpate(Jogodavelha)) { //enquanto não tem vencedor nem empate
    printabuleiro(Jogodavelha);
    cout << "Vez do jogador " << Jogodavelha.rodada << ": ";
        cin >> escolha;
        //a escolha precisa ser um número de 1 até 9 e tambem não pode estar ocupada
        if (escolha < 1 || escolha > 9 || Jogodavelha.tabuleiro[escolha - 1] == 'X' || Jogodavelha.tabuleiro[escolha - 1] == 'O') {
            cout << "Escolha inválida!\n";
            continue;
        }
        Jogodavelha.tabuleiro[escolha - 1] = Jogodavelha.rodada;
        Jogodavelha.rodada = (Jogodavelha.rodada == 'X') ? 'O' : 'X';
        // a linha acima estava dando um problema com o if else entaão eu usei esse jeito aqui que eu descobri que faz a mesma coisa
    }
    printabuleiro(Jogodavelha); //chmada da função que imprime o tabuleiro
    if (verificarVitoria(Jogodavelha)) {
        cout << "Jogador " << (Jogodavelha.rodada == 'X' ? 'O' : 'X') << " vence!\n"; //anuncio do vencedor 
        (Jogodavelha.rodada == 'X') ? Jogodavelha.pontuacaoDoO++ : Jogodavelha.pontuacaoDoX++; //encrememnta a pontuação do vencedor 
    } else {
        cout << "Empate!\n";
    }
    guardapontuacao(Jogodavelha); // chama a função que guarda a pontuação
}
```
Procedimento que **inicializa o jogo**.

## Função Principal
```cpp
int main() {
    //chamada das funções 
    Jogodavelha Jogodavelha;
    kumessarujogu(Jogodavelha);
    jogujogu(Jogodavelha);
    liberarJogo(Jogodavelha);
    return 0;
}
```
Função principal que **junta todas as funções procedimentos**.

# 📽️ Vídeo do Projeto
Para acessar o link do vídeo [Clique aqui](https://drive.google.com/file/d/161DAK6v04em11ZzwPwohojdMt7rHPuq-/view?usp=drive_link)

# 📊 Slides do projeto
Para acessar os slide [Clique aqui](https://drive.google.com/file/d/161DAK6v04em11ZzwPwohojdMt7rHPuq-/view?usp=drive_link)

# 📌 Conclusão
Neste projeto podemos **colocar em prática** tudo o que vimos durante o semestre nas aulas de Computação para Engenharia na Universidade de Brasília, além de entender como utilizar as ferramentas para otimizar os códigos e deixá-los mais eficientes. O código apresenta os conceitos de vetores, funções, arquvios e manipulação de entradas/saídas em C++.
