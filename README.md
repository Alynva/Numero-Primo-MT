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

1. Escrever o divisor `(2)_10 = (10)_2` na 2ª trilha;
2. Repetir o número da 1ª trilha na 3ª trilha;
3. Subtrair tantas vezes quanto for possível o número da 2ª trilha do número da 3ª trilha, guardando os resultados na 3ª trilha;
- Se o resultado na 3ª trilha for diferente de 0, deve-se incrementar o divisor (número na 2ª trilha) e retornar para (2.);
- Se o resultado na 3ª trilha for igual à 0:
    - se o número da 1ª trilha for igual ao número da 2ª trilha, portanto o número da 1ª trilha **é primo**;
    - se o número da 1ª trilha for diferente  do número da 2ª trilha, portanto o número da 1ª trilha **não é primo**.

### Declaração da Máquina

- `Q = {q0, q1, q2}`
- `Σ = {}`
- `Γ = {0, 1, ¢, $}`
- `s = q0`
- `b = ¬`
- `F = q2`
- `δ`:
    1. `δ(q0, {¢, 𝑎, 𝑏}) = (q1, {¢, 𝑎, 𝑏}, →)`
    2. `δ(q1, {𝑎, 𝑏, 𝑐}) = (q1, {𝑎, 𝑏, 𝑎}, →)`
    3. `δ(q1, {$, 𝑎, 𝑏}) = (q1, {$, 𝑎, 𝑏}, ←)`

## Conclusão

## Referências bibliográficas
