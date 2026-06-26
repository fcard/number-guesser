# number-guesser
Projeto 1 de Circuitos Digitais UFCA

## Comparador 1

<img width="1302" height="358" alt="image" src="https://github.com/user-attachments/assets/e958dcc5-712d-4595-a67f-ec975b188288" />

O comparador de 1 bit tem saída 1 quando as duas entradas são iguais, e 0 caso contrário.

Tabela Verdade:
| X | Y | X = Y |
|---|---|-------|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Mapa de karnaugh:

<img width="368" height="358" alt="image" src="https://github.com/user-attachments/assets/d114cf89-a44b-495b-9023-dcb71df4b1fd" />

Expressão Simplificada:

<img width="402" height="133" alt="image" src="https://github.com/user-attachments/assets/be9cc68a-ef4c-4b44-b122-785c98776ba7" />


## Comparador 4

<img width="1367" height="499" alt="image" src="https://github.com/user-attachments/assets/e39d654c-aa1c-44dd-a67d-66166f027096" />

O comparador de 4 bits tem saida 1 quando as duas entradas de 4 bits são iguais, e 0 caso contrário.

Primeiramente, cada bit de cada entrada é dividida pelo splitter (<img width="84" height="101" alt="image" src="https://github.com/user-attachments/assets/bb55fd7a-4de1-4a20-b208-ed415ccdb702" />) e estes bits individuais são postos em pares (primeiro bit da primeira entrada A com o primeiro bit da segunda entrada, segundo bit da primeira entrada com o segundo bit da segunda entrada, etc) e cada um destes pares são postos como entradas de um de quatro comparadores de 1 bit.

<img width="743" height="538" alt="image" src="https://github.com/user-attachments/assets/d098bcc6-a1e9-46c9-9860-ee9e74824230" />

Finalmente, cada saida dos comparadores são postos como entrada de um AND, o que equivale a dizer que a saída será 1 se todos os comparadores forem 1, ou seja, se todos os pares de bits forem iguais.

## Subtrator 1

<img width="542" height="743" alt="image" src="https://github.com/user-attachments/assets/598d97c6-b126-461f-b7a4-395191eb02ee" />

Dadas entradas X e Y e B<sub>in</sub> (borrow in, que é 1 se está sendo "pegue emprestado" deste digito, 0 caso contrário), o subtrator de 1 bit tem como saidas X - Y e o valor de borrow out (que é 1 se o subtrator precisa "pegar emprestado" do digito sucessor, 0 caso contrário)

Tabela Verdade:
| X | Y | B<sub>in</sub> | X - Y | B<sub>out</sub> |
|---|---|----------------|-------|-----------------|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 1 |
| 0 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 0 |
| 1 | 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 | 1 |

Mapas de Karnaugh:

<img width="735" height="338" alt="image" src="https://github.com/user-attachments/assets/6df3930c-7051-46ba-888a-1def999bcc48" />

Expressões Simplificadas:

<img width="735" height="338" alt="image" src="https://github.com/user-attachments/assets/113d1f37-54b0-4612-8184-3eac96935448" />

## Subtrator 4

<img width="1190" height="858" alt="image" src="https://github.com/user-attachments/assets/0c6c3714-b681-41d2-9579-5d2d04d50913" />

Dadas entradas de 4 bits X = X<sub>3</sub>X<sub>2</sub>X<sub>1</sub>X<sub>0</sub> e Y = Y<sub>3</sub>Y<sub>2</sub>Y<sub>1</sub>Y<sub>0</sub>, o subtrator de 4 bits tem como saída X - Y (4 bits) e B<sub>out</sub> (1 bit).

Primeiramente, usamos splitters para separarmos os bits de cada entrada, então foram postos os pares de bits correspondentes de cada entrada (X<sub>3</sub>, Y<sub>3</sub>), ((X<sub>2</sub>, Y<sub>2</sub>), etc. como entradas de quatro subtratores de 1 bit, onde o B<sub>in</sub> do primeiro subtrator é 0 e os seguintes tem como B<sub>in</sub> o B<sub>out</sub> do subtrator anterior. O B<sub>out</sub> do circuito é o B<sub>out</sub> do ultimo subtrator. Finalmente, as saídas S<sub>k</sub> = X<sub>k</sub> - Y<sub>k</sub> de cada subtrator são postas em uma cadeia de extensores de bit tal que a saída final X - Y = S<sub>3</sub>S<sub>2</sub>S<sub>1</sub>S<sub>0</sub>.

## Diferença

<img width="1303" height="797" alt="image" src="https://github.com/user-attachments/assets/e4537f01-c10b-4f11-993d-fcc1e4a3c699" />

Dadas entradas X e Y de 4 bits, a diferença tem como saída X - Y se X &geq; Y e tem como saída Y - X se X < Y.

Temos um multiplexador que seleciona entre X - Y e Y - X baseado no B<sub>out</sub> do subtrator de X - Y. O B<sub>out</sub> de X - Y é 1 quando Y > X, logo neste caso o multiplexador selecionará Y - X, e caso contrário selecionará X - Y.

## LeftShift 4

<img width="1374" height="659" alt="image" src="https://github.com/user-attachments/assets/11343bdd-bba3-4cbb-8109-ed498978dd08" />

Dada uma entrada de 4 bits X = X<sub>3</sub>X<sub>2</sub>X<sub>1</sub>X<sub>0</sub>, o LeftShift de 4 bits tem como saída um S = X<sub>3</sub>X<sub>2</sub>X<sub>1</sub>X<sub>0</sub>0000 de 8 bits.

Faz-se um encadeamento de 4 extensores de bit de tipo input, cada um recebendo o anterior como entrada principal (o primeiro recebendo a constante 0 de 4 bits) tendo como saída um bit a mais que sua entrada, e como entrada secundária um dos bits da entrada do circuito.

## LEDs

O display de 7 segmentos é compostos por 7 leds identificados pelas letras A, B, C, D, E, F e G. Foi criado um circuito para cada led, de modo que ficasse ligado apenas os leds que formassem o número ou a letra desejada, que no caso seria de 0 ate 9 ou A ate F.

Tabela Verdade:

| X<sub>3</sub> | X<sub>2</sub> | X<sub>1</sub> | X<sub>0</sub> | A | B | C | D | E | F | G |
|---------------|---------------|---------------|---------------|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 0 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 1 |
| 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 1 | 1 |
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 1 |
| 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 0 |
| 1 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 |

O circuito foi criado com a ferramenta de analise combinatória do Logisim.

## Guess

<img width="1289" height="934" alt="image" src="https://github.com/user-attachments/assets/379f1d17-1730-466b-aeff-eb5d2c8eaf56" />

O circuito principal se tratando do comportamento do jogo. Tem como entrada o "chute" do jogador (número a ser comparado com o número secreto interno), um bit de confirmação e um bit que reinicia o número secreto. As saída são:

O bit que liga o LED direito: 1 quando o chute do jogador é exatamente igual ao número secreto e o bit de confirmação é 1. Simplesmente usa-se o comparador de 4 bits para comparar os números e usa-se um AND entre o resultadado da comparação e o bit de confirmação.

A cor vermelha do LED esquerdo: O LED brilha com cor mais vermelha quanto menor a diferença. Usamos um subtrator de 4 bits e um leftshifter de 4 bits para fazer com que o valor final seja `(15 - D) << 4`, ou `(15 - D) * 16`, onde D é a diferença. Usamos um AND para que o LED só tenha qualquer quantidade de vermelho quando o bit de confirmação for 1 e o LED direito esteja apagado.

A cor azul do LED esquerdo: O LED brilha com cor mais azul quanto maior a diferença. Usamos um leftshifter de 4 bits para fazer com que o valor final seja `D << 4`, ou `D * 16`, onde D é a diferença. Usamos um AND para que o LED só tenha qualquer quantidade de azul quando o bit de confirmação for 1 e o LED direito esteja apagado.

Em geral, só um dos LEDs pode estar acesso, no máximo.


