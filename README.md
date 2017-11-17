# Projeto de Máquina de Turing com Múltiplas Fitas Reconhecedora de Número Primo

Projeto desenvolvido como trabalho na disciplina de LFA (2017.2) no curso BCC da UFSCar

## Índice

1. [Introdução](#introdução)
2. [Teoria](#teoria)
3. [Descrição](#descrição)
4. [Conclusão](#conclusão)
5. [Referências Bibliográficas](#referências-bibliográficas)

## Introdução

<p align="center">
    <img alt="Turing Machine" src="https://pagez.com/attachments/337/article/3508/e22a805a0cab3825ecddce1102553c02.gif" />
    <br>
    Imagem por <a href="https://medium.com/concerning-pharo/a-turing-machine-simulator-written-in-pharo-fda74e1a705b">Julien Delplanque no Medium</a>
</p>

Este trabalho tem como objetivo a criação de uma Máquina de Turing que lê na 1ª linha um número `(N)_2 > (2)_10`, delimitado pelos símbolos `¢` e `$`, e determina se este é primo.

## Teoria

`T = (Q, Σ, Γ, s, b, F, δ)`

- `Q` é um conjunto finito de estados
- `Σ` é um alfabeto finito de símbolos
- `Γ` é o alfabeto da fita (conjunto finito de símbolos)
- `s ∈ Q` é o estado inicial
- `b ∈ Γ` é o símbolo branco (o único símbolo que se permite ocorrer na fita infinitamente em qualquer passo durante a computação)
- `F ⊆ Q` é o conjunto dos estados finais
- `δ : Q × Γ ⇒ Q × Γ × {←, →}` é uma função parcial chamada função de transição, onde `←` é o movimento para a esquerda e `→` é o movimento para a direita.

`⊢`

## Descrição

### O Algoritmo

Este algoritmo se baseia em subtrações sucessivas do número desejado até que se obtenha um resultado igual a 0. Ele é descrito nos seguintes passos:

1. Escrever o divisor `(2)_10 = (10)_2` na 2ª trilha;
2. Repetir o número da 1ª trilha na 3ª trilha;
3. Subtrair tantas vezes quanto for possível o número da 2ª trilha do número da 3ª trilha, guardando os resultados na 3ª trilha;
- Se o resultado na 3ª trilha for diferente de 0, deve-se incrementar o divisor (número na 2ª trilha) e retornar para (2.);
- Se o resultado na 3ª trilha for igual à 0:
    - se o número da 1ª trilha for igual ao número da 2ª trilha, portanto o número da 1ª trilha **é primo**;
    - se o número da 1ª trilha for diferente  do número da 2ª trilha, portanto o número da 1ª trilha **não é primo**.

### Declaração da Máquina

`T = (Q, Σ, Γ, s, b, F, δ)`:

- `Q = {q0, q1, q2}`;
- `Σ = {}`;
- `Γ = {0, 1, ¢, $}`;
- `s = q0`;
- `b = ¬`;
- `F = q2`;
- `δ` será definido no tópico a seguir.

### Transições

#### Sub-rotinas

##### _MOVE_

Como foi detectado a necessidade de mover o controle finito para o final do número repetidas vezes, foi utilizado uma sub-rotina denominada _MOVE_.

_MOVE_ inicia na descrição instantânea:

```
¢|     |xx[...]$
y|r_0,A|yy[...]y
z|     |zz[...]z
```

e termina na:

```
¢x[...]|     |x$
yy[...]|r_1,A|yy
zz[...]|     |zz
```

onde `x` pode assumir `0` ou `1`, `y` e `z` podem assumir `¬`, `0` ou `1` e `A` é uma variável que pode assumir **qualquer componente**. As movimentações de _MOVE_ são:

1. `δ([r_0, A], [x, y, z]) = ([r_0, A], [x, y, z], →)`
2. `δ([r_0, A], [$, y, z]) = ([r_1, A], [$, y, z], ←)`

com as mesmas variáveis utilizadas anteriormente.

#### MT Principal

Seguindo o algoritmo:

1. Escrever `(10)_2` na 2ª trilha
    Primeiramente, precisamos fazer com que o controle finito vá para o final do número, pela transição:
    1. `δ([q_0, a], [¢, y, z]) = ([r_0, a], [¢, y, z], →)`
    Agora, utilizando dois estados, insere o valor:
    2. `δ([r_1, a], [x, y, z]) = ([q_1, a], [x, 0, z], ←)`
    3. `δ([q_1, a], [x, y, z]) = ([q_2, a], [x, 1, z], ←)`
2. Repetir 1ª trilha na 3ª
    Novamente, precisamos mover o controle finito para o começo ou para o fim do número, como já possuímos uma sub-rotina que leva-o para o final, começaremos a preencher a partir do final do número:
    1. `δ([q_2, a], [x, y, z]) = ([r_0, b], [x, y, z], →)`
    Neste ponto somos capazes de começar a cópia:
    2. `δ([r_1, b], [x, y, z]) = ([q_3, b], [x, y, x], ←)`
    3. `δ([q_3, b], [x, y, z]) = ([q_3, b], [x, y, x], ←)`
    4. `δ([q_3, b], [¢, y, z]) = ([s_0, c], [¢, y, z], →)` (já chama o próximo passo)
3. Subtrair 2ª trilha da 3ª (sub-rotina _SUBTRAI_)
    Seguindo o algoritmo de subtração binária apresentado em aula, precisamos partir do dígito menos significativo, portanto chamaremos novamente a sub-rotina _MOVE_:
    1. `δ([s_0, A], [x, y, z]) = ([r_0, A], [x, y, x], →)`
    A partir deste ponto, começa a ser realizada a subtração:
    2. `δ([r_1, A], [x, 0, z]) = ([s_1, A], [x, 0, x], ←)`
    3. `δ([s_1, A], [x, 0, z]) = ([s_1, A], [x, 0, x], ←)`
    4. `δ([s_1, A], [x, ¬, z]) = ([s_1, A], [x, ¬, x], ←)`
    5. `δ([s_1, A], [x, 1, 1]) = ([s_1, A], [x, 1, 0], ←)`
    6. `δ([s_1, A], [x, 1, 0]) = ([s_2, A], [x, 1, 1], ←)`
    7. `δ([s_2, A], [x, 0, 0]) = ([s_2, A], [x, 0, 1], ←)`
    8. `δ([s_2, A], [x, ¬, 0]) = ([s_2, A], [x, ¬, 1], ←)`
    9. `δ([s_2, A], [x, 1, 1]) = ([s_2, A], [x, 1, 1], ←)`
    10. `δ([s_2, A], [x, 1, 0]) = ([s_2, A], [x, 1, 0], ←)`
    11. `δ([s_2, A], [x, 0, 1]) = ([s_2, A], [x, 0, 0], ←)`
    12. `δ([s_2, A], [x, ¬, 1]) = ([s_2, A], [x, ¬, 0], ←)`
    13. `δ([s_1, A], [¢, ¬, ¬]) = ([s_3, A], [¢, ¬, ¬], →)`
- Verificar 3ª trilha [...]


1. `δ(q0, {¢, 𝑎, 𝑏}) = (q1, {¢, 𝑎, 𝑏}, →)`
2. `δ(q1, {𝑎, 𝑏, 𝑐}) = (q1, {𝑎, 𝑏, 𝑎}, →)`
3. `δ(q1, {$, 𝑎, 𝑏}) = (q1, {$, 𝑎, 𝑏}, ←)`

## Conclusão

## Referências bibliográficas
