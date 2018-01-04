![Cabecalho](../../../ReadMe-Anexos/Cabecalho.png)

[Home](../../../ReadMe.md) :: [Módulo Treinamento](../../Modulo-Treinamento.md) :: [FU-Integração Financeira de Clientes](../FU-Integracao-Financeira-Clientes.md) :: [UC-Reativar Cliente](UC-Reativar-Cliente.md)

# Caso de Uso: Reativar Cliente


| **[UC]**                | Reativar Cliente                                                                                                                                                                                                                                                           |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Objetivo**            | Permite reativar um cliente inativado (**Básico** ou **Premium**) sem faturas em atraso em conformidade com [RN-Reativação de Cliente](../Regras-de-Negocios/RN-Reativacao-de-Cliente.md)                                                                           |
| **Ator Principal**      | Analista Financeiro                                                                                                                                                                                                                                                       |
| **Atores Secundários**  | Gerente de Contas                                                                                                                                                                                                                                                         |
| **Fluxo Principal**     | [PR: Reativar Cliente](#pr-reativar-cliente)                                                                                                                                                                                                                               |
| **Fluxos de Exceção**   | [EX01: Cliente possui parcela em atraso](#ex01-cliente-passui-parcela-em-atraso)                                                                                                                                                                                           |
|                         | [EX02: Ocorreu um erro interno no sistema durante a reativação](#ex02-ocorreu-um-erro-interno-no-sistema-durante-a-reativacao)                                                                                                                                           |
|                         | [EX03: Gerente de Contas não informa Login/Senha](#ex03-gerente-de-contas-nao-informa-login-senha)                                                                                                                                                                     |
|                         | [EX04: Gerente de Contas não confirma a reativação](#ex04-gerente-de-contas-nao-confirma-a-reativacao)                                                                                                                                                               |
|                         | [EX05: Analista Financeiro não seleciona um cliente](#ex05-analista-financeiro-nao-seleciona-um-cliente)                                                                                                                                                                   |
|                         | [EX06: Gerente de Contas não possui permissão para inativação](#ex06-gerente-de-contas-nao-possui-permissao-inativacao)                                                                                                                                               |
|                         | [EX07: Analista Financeiro não informa a observação para inativação do cliente](#ex05-Analista-Financeiro-nao-informa-observacao)                                                                                                                                         |



## PR: Reativar Cliente

1. **Analista Financeiro** seleciona opção de _Reativar Cliente_ no Sistema.
2. **Sistema** apresenta o formulário _Reativação de Clientes_.
3. **Analista Financeiro** informa cliente para reativação.
4. **Sistema** obtém na base de dados o cliente para reativação, cf: [RN-Reativação de Cliente](../Regras-de-Negocios/RN-Reativacao-de-Cliente.md) [[EX01](#ex01-cliente-possui-parcela-em-atraso)] [[EX05](#ex05-analista-financeiro-nao-seleciona-um-cliente)].
5. **Sistema** apresenta dados do cliente com:
  - Nome
  - Plano (cf: [RN-Planos de Clientes](../Regras-de-Negocios/RN-Planos-de-Clientes.md))
  - Número de meses em atraso
6. **Analista Financeiro** aciona opção para aprovar a reativação do cliente, informa a data de pagamento das parcelas e, opcionalmente, informa uma observação [[EX02](#ex02-ocorreu-um-erro-interno-no-sistema-durante-a-reativacao)].
7. **Sistema** solicita confirmação pelo **Gerente de Contas** [[EX02](#ex02-ocorreu-um-erro-interno-no-sistema-durante-a-reativacao)].
8. **Gerente de Contas** informa sua identificação (login e senha) e aciona comando para aprovar [[EX04](#ex04-gerente-de-contas-nao-informa-login-senha)] [[EX05](#ex05-gerente-de-contas-nao-confirma-a-reativacao)].
9. **Sistema** confirma que o **Gerente de Contas** possui permissão para reativação de clientes [[EX06](#ex06)].
10. **Sistema** registra a reativação do cliente [[EX02](#ex02-ocorreu-um-erro-interno-no-sistema-durante-a-reativacao)].
11. **Fim do Caso de Uso**


## Fluxos de Exceção

### EX01: Cliente possui parcela em atraso

Exceção quando o cliente ainda possui parcelas em atraso segundo a regra [RN-Reativação de Cliente](../Regras-de-Negocios/RN-Reativacao-de-Cliente.md).

1. **Sistema** exibe mensagem: _"O cliente possui parcelas em atraso"_.
2. **Sistema** retorna ao passo 2 do [[PR](#pr-reativar-cliente)]


### EX02: Ocorreu um erro interno no sistema durante a reativação

Exceção quando algum **erro interno** inesperado ocorreu no sistema e a operação não foi efetivada.

1. **Sistema** estorna qualquer operação parcialmente executada.
2. **Sistema** exibe uma mensagem com detalhes do erro e com orientações de como solicitar suporte técnico.
3. **Sistema** retorna ao passo 2 do [[PR](#pr-inativar-cliente)].


### EX03: Gerente de Contas não informa Login/Senha

Exceção quando o **Gerente de Contas** não informa seu Login e Senha e aciona opção para aprovar a reativação.

1. **Sistema** exibe mensagem: _"Informe o Login e a Senha para aprovação de Reativação de cliente"_.
3. **Sistema** retorna ao passo 2 do [[PR](#pr-inativar-cliente)].

### EX04: Gerente de Contas não confirma a reativação

Exceção quando o **Gerente de Contas** se recusa a aprovar a reativação do cliente, acionando opção "Recusar".

1. **Sistema** exibe mensagem: _"Reativação de cliente não aprovada."_.
3. **Sistema** retorna ao passo 2 do [[PR](#pr-inativar-cliente)].

### EX05: Analista Financeiro não informa um cliente

Exceção quando **Analista Financeiro** não informa o cliente para reativação.

1. **Sistema** exibe mensagem: _"Informe o cliente para reativação"_.
2. **Sistema** retorna ao passo 2 do [[PR](#pr-inativar-cliente)].


### EX06: Gerente de Contas não possui permissão para reativação

Exceção quando o **Gerente de Contas** aprova a reativação do cliente, porém o **Sistema** identifica que ele não possui permissão para tal, cf. [RN-Reativação de Cliente](../Regras-de-Negocios/RN-Reativacao-de-Cliente.md).

1. **Sistema** NÃO confirma que o **Gerente de Contas** possui permissão para reativação de clientes.
2. **Sistema** exibe mensagem: _"Falha ao reativar cliente: (nome-do-Gerente-de-Contas) não possui permissão: (código-da-permissão)."_.
3. **Sistema** retorna ao passo 8 do [[PR](#pr-reativar-cliente)].


### EX07: Analista Financeiro não informa data dos pagamentos das parcelas para reativação do cliente

Exceção quando **Analista Financeiro** não informa data dos pagamentos das parcelas para reativar o cliente.

1. **Sistema** exibe mensagem: _"Informe data dos pagamentos das parcelas para reativar o cliente"_.
2. **Sistema** retorna ao passo 6 do [[PR](#pr-reativar-cliente)].



_[Sobre o Portal de Documentação](../../../About/About.md)_

![Rodape](../../../ReadMe-Anexos/Rodape.png)
