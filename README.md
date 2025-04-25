import random

# Criando o tabuleiro 5x5
tabuleiro = [["~" for _ in range(5)] for _ in range(5)]
navios = []

# Letras para referência de linha
letras = ["A", "B", "C", "D", "E"]

# Gerando 3 navios em posições aleatórias
while len(navios) < 3:
    linha = random.randint(0, 4)
    coluna = random.randint(0, 4)
    if (linha, coluna) not in navios:
        navios.append((linha, coluna))

tentativas = 10
acertos = 0

def mostrar_tabuleiro():
    print("  1 2 3 4 5")
    for i in range(5):
        print(letras[i], " ".join(tabuleiro[i]))

print("Bem-vindo à Batalha Naval!")
print("Tente afundar os 3 navios escondidos.")
mostrar_tabuleiro()

while tentativas > 0 and acertos < 3:
    jogada = input("Digite a coordenada (ex: A3): ").upper().strip()

    if len(jogada) != 2 or jogada[0] not in letras or not jogada[1].isdigit():
        print("Entrada inválida. Use formato como A3.")
        continue

    linha = letras.index(jogada[0])
    coluna = int(jogada[1]) - 1

    if tabuleiro[linha][coluna] != "~":
        print("Você já tentou essa posição!")
        continue

    if (linha, coluna) in navios:
        print("Acertou um navio!")
        tabuleiro[linha][coluna] = "X"
        acertos += 1
    else:
        print("Água!")
        tabuleiro[linha][coluna] = "O"

    tentativas -= 1
    mostrar_tabuleiro()
    print(f"Restam {tentativas} tentativas e {3 - acertos} navios.")

# Fim de jogo
if acertos == 3:
    print("Parabéns! Você afundou todos os navios!")
else:
    print("Fim de jogo! Você não conseguiu encontrar todos os navios.")
    print("Posições dos navios eram:")
    for linha, coluna in navios:
        print(f"{letras[linha]}{coluna + 1}")
