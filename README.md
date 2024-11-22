def criaMatriz():
    return [[1, 2, 3],
            [4, 5, 6],
            [7, 8, 9]]


def apresentaMatriz(mat):
    print(mat[0][0], "|", mat[0][1], "|", mat[0][2])
    print("-" * 5)
    print(mat[1][0], "|", mat[1][1], "|", mat[1][2])
    print("-" * 5)
    print(mat[2][0], "|", mat[2][1], "|", mat[2][2])


def posicaoOcupada(matriz, posicao): # Cria uma função com dois procedimentos
    linha = (posicao - 1) // 3
    coluna = (posicao - 1) % 3
    return matriz[linha][coluna] == "X" or matriz[linha][coluna] == "O"


def registraJogada(mat, posicao, jogador):
    linha = (posicao - 1) // 3
    coluna = (posicao - 1) % 3
    mat[linha][coluna] = jogador


def trocaJogador(jogador):
    return "O" if jogador == "X" else "X"


def verificaGanhador(mat, jogador):
 
    for i in range(3):
        if mat[i][0] == mat[i][1] == mat[i][2] == jogador:  
            return True
        if mat[0][i] == mat[1][i] == mat[2][i] == jogador:  
            return True
    if mat[0][0] == mat[1][1] == mat[2][2] == jogador:  
        return True
    if mat[0][2] == mat[1][1] == mat[2][0] == jogador: 
        return True
    return False


print("* JOGO DA VELHA *\n")
print("Desafie o seu colega no jogo da velha.\n")

print("Regras:")
print(" a) O primeiro jogador participará com a letra X e o segundo com a letra O.")
print(" b) Os números de 1 a 9 representam os espaços que estão livres.")
print(" c) Você só poderá escolher as posições livres.")
print(" d) O vencedor será o primeiro jogador a preencher uma linha, uma coluna ou uma diagonal.")


matriz = criaMatriz()


jogador = "X"
c = 0


while c < 9:
    print()
    apresentaMatriz(matriz)
    print()
    print("Jogador ==> ", jogador)
    posicao = int(input("Informe a posição desejada: "))

   
    if posicaoOcupada(matriz, posicao):
        print("A posição já está ocupada! Tente novamente.")
        continue

    
    registraJogada(matriz, posicao, jogador)
    
    
    if verificaGanhador(matriz, jogador):
        apresentaMatriz(matriz)
        print(f"Jogador {jogador} ganhou!")
        break
    jogador = trocaJogador(jogador)
    c += 1  

if c == 9 and not verificaGanhador(matriz, jogador):
    apresentaMatriz(matriz)
    print("Empate! Não há mais posições disponíveis.")
