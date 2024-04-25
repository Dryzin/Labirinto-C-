# Labirinto em C#

Este projeto em C# cria um labirinto representado por uma matriz bidimensional de caracteres. O objetivo é guiar um "rato" representado por 'R' para encontrar o "queijo" representado por 'Q' dentro do labirinto.

## Funcionalidades Principais

1. **mostrarLabirinto(char[,] array, int l, int c):**
   - Mostra o estado atual do labirinto na console.
   - `array`: Matriz bidimensional representando o labirinto.
   - `l`: Número de linhas do labirinto.
   - `c`: Número de colunas do labirinto.

2. **criaLabirinto(char[,] meuLab):**
   - Gera aleatoriamente o labirinto, onde '*' representa paredes e ' ' espaços vazios.
   - Coloca o queijo ('Q') em uma posição aleatória dentro do labirinto.

3. **buscarQueijo(char[,] meuLab, int i, int j):**
   - Algoritmo para o rato (representado por 'R') encontrar o queijo ('Q') no labirinto.
   - Utiliza uma pilha para registrar o caminho percorrido.
   - Move o rato de forma aleatória, seguindo regras simples:
     - Se houver um espaço vazio ao lado, o rato se move para lá.
     - Se não houver espaço vazio, ele volta para a última posição registrada na pilha.
   - O algoritmo é visualizado passo a passo na console, mostrando o caminho do rato até o queijo.

## Entendendo a função buscarQueijo

- A função inicia na posição `(i, j)` dentro do labirinto.
- O rato marca sua posição com 'R'.
- Ele tenta se mover em todas as direções possíveis.
- Se encontrar o queijo, o programa termina e exibe a mensagem "O rato encontrou o queijo!".
- Se não encontrar o queijo e não tiver mais movimentos possíveis, exibe "Não foi possível encontrar o queijo.".

O código usa uma pilha para rastrear o caminho percorrido e garantir que o rato explore todo o labirinto em busca do queijo. Cada movimento é visualizado na console, permitindo acompanhar a busca passo a passo.

---

## Detalhamento do buscarQueijo

- `Stack<int> pilha`: É uma pilha que armazena as coordenadas (i, j) do labirinto, permitindo ao rato retroceder em sua trajetória quando necessário.
- `int linha = 0, coluna = 0`: Variáveis para registrar a última posição válida do rato no labirinto.
- `char sentido = '0'`: Indica a direção que o rato está seguindo ('|' para vertical e '-' para horizontal).

### Condições (ifs)

- `if (meuLab[i - 1, j] == 'Q' || meuLab[i + 1, j] == 'Q' || meuLab[i, j + 1] == 'Q' || meuLab[i, j - 1] == 'Q')`: Verifica se o rato encontrou o queijo em alguma direção adjacente.
- `if (meuLab[i, j + 1] == ' ') { ... }`: Verifica se há espaço vazio à direita para mover o rato.
  - `pilha.Push(i); pilha.Push(j);`: Registra a posição atual na pilha antes de mover o rato.
- `else if (meuLab[i + 1, j] == ' ') { ... }`: Verifica se há espaço vazio abaixo para mover o rato.
  - `pilha.Push(i); pilha.Push(j);`: Registra a posição atual na pilha antes de mover o rato.
- `else if (meuLab[i, j - 1] == ' ') { ... }`: Verifica se há espaço vazio à esquerda para mover o rato.
  - `pilha.Push(i); pilha.Push(j);`: Registra a posição atual na pilha antes de mover o rato.
- `else if (meuLab[i - 1, j] == ' ') { ... }`: Verifica se há espaço vazio acima para mover o rato.
  - `pilha.Push(i); pilha.Push(j);`: Registra a posição atual na pilha antes de mover o rato.
- `else if (pilha.Count > 0) { ... }`: Verifica se há posições na pilha para voltar caso não haja mais movimentos possíveis.
  - `j = pilha.Pop(); i = pilha.Pop();`: Volta para a última posição registrada na pilha.
- `else { ... }`: Caso não seja possível encontrar o queijo e não haja mais movimentos disponíveis, o algoritmo encerra.
