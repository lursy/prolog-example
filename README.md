# prolog-example

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
orientacao(Situacao, Texto) :-
    problema(Situacao, Tipo),
    conselho(Tipo, Texto).
% Regra com negacao
orientacao(Situacao, 'Nenhuma irregularidade identificada.') :-
    situacao(Situacao),
    \+ problema(Situacao, _).
