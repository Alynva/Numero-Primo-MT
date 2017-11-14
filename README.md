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

- `Q = {q0, q1, q2}`
- `Σ = {}`
- `Γ = {0, 1, ¢, $}`
- `s = q0`
- `b = ¬`
- `F = q2`
- `δ`:
    - `δ(q0, {¢, 𝑎, 𝑏}) = (q1, {¢, 𝑎, 𝑏}, →)`
    - `δ(q1, {𝑎, 𝑏, 𝑐}) = (q1, {𝑎, 𝑏, 𝑎}, →)`
    - `δ(q1, {$, 𝑎, 𝑏}) = (q1, {$, 𝑎, 𝑏}, ←)`

## Conclusão

## Referências bibliográficas
