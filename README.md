# Projeto de Máquina de Turing com Múltiplas Fitas Reconhecedore de Número Primo

Projeto desenvolvido como trabalho na disciplina de LFA (2017.2) no curso BCC da UFSCar

## Introdução

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
