#include <iostream>
#include <fstream>
using namespace std;

//struct com informações do jogo
struct Jogodavelha {
char* tabuleiro; //ponteiro
char rodada; // X ou O
int pontuacaoDoX; // pontuação do jogador X
int pontuacaoDoO; // inicialização do O
};

//função para inicializar  o jogo
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

//procedimento que imprime o tabuleiro do jogo
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
//procedimento para criar o arquivo de armazenamento da pontuação
void guardapontuacao(const Jogodavelha& Jogodavelha) {
    ofstream arquivo("pontuacoes.txt");//ofstream é a classe que permite escrever em arquivos 
    //ela faz parte da biblioteca fstream, foi por conta disso que incluímos a biblioteca fstream
    arquivo << "Jogador X - Pontuação: " << Jogodavelha.pontuacaoDoX << "\n"; // pontuação no arquivo
    arquivo << "Jogador O - Pontuação: " << Jogodavelha.pontuacaoDoO << "\n"; 
    arquivo.close(); //salva a pontuação no arquivo e fecha
    //no código, a função guarda pontuação escreve em um arquivo o resultado do jogo que acabou de ser jogado 
    // ela não acumula pontuações, apenas registra a vitoria(1), e a derrota(0). 
}
//proceddimento que roda o jogo 
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
// função main a braba que junta as funções tudo
int main() {
    //chamada das funções 
    Jogodavelha Jogodavelha;
    kumessarujogu(Jogodavelha);
    jogujogu(Jogodavelha);
    liberarJogo(Jogodavelha);
    return 0;
}
// fim!! Lembrando que a gigele faz os slides, o alex faz o vídeo e o bruno faz o repositório com a giovanna
// valeu galera!!
