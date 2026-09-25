# prolog-example

```pl
% SISTEMA ESPECIALISTA EM PROLOG

% Fatos
situacao(ferias_nao_pagas).
situacao(horas_extras).
situacao(rescisao_sem_pagamento).
situacao(atraso_salarial).
situacao(documentacao_nao_entregue).
situacao(salario_pago_em_dia).
situacao(ferias_pagas).
situacao(rescisao_com_pagamento).

% Problemas relacionados às situações
problema(ferias_nao_pagas, ferias).
problema(horas_extras, hora_extra).
problema(rescisao_sem_pagamento, rescisao).
problema(atraso_salarial, salario).
problema(documentacao_nao_entregue, documentacao).

% Conselhos
conselho(ferias, 'Ferias devem ser pagas ate 2 dias antes do inicio (art. 145 da CLT).').
conselho(hora_extra, 'Hora extra deve ter adicional minimo de 50% sobre a hora normal (art. 7, XVI da Constituicao Federal).').
conselho(rescisao, 'As verbas rescisorias devem ser pagas em ate 10 dias apos o fim do contrato (art. 477, par. 6 da CLT).').
conselho(salario, 'O salario mensal deve ser pago ate o 5o dia util do mes seguinte (art. 459, par. 1 da CLT).').
conselho(documentacao, 'Os documentos da rescisao devem ser entregues no prazo legal (art. 477 da CLT).').

% Regras
% R1 - Combinacao de condicoes: situacao conhecida + problema + conselho
orientacao(S, Texto) :-
    situacao(S),
    problema(S, Tipo),
    conselho(Tipo, Texto).

% R2 - Negacao: situacao conhecida sem problema
orientacao(S, 'Nenhuma irregularidade identificada.') :-
    situacao(S),
    \+ problema(S, _).

% R3 - Negacao: situacao nao cadastrada
orientacao(S, 'Situacao nao reconhecida pelo sistema.') :-
    \+ situacao(S).

% R4 - Combinacao: problema que envolve dinheiro (tudo menos documentacao)
pendencia_financeira(S) :-
    problema(S, Tipo),
    Tipo \= documentacao.
```
