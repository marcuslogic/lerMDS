![Cabecalho](../../../ReadMe-Anexos/Cabecalho.png)

[Home](../../../ReadMe.md) :: [Módulo Treinamento](../../Modulo-Treinamento.md) :: [FU-Integração Financeira de Clientes](../FU-Integracao-Financeira-Clientes.md) :: [RN-Reativação de Cliente](RN-Reativacao-de-Cliente.md)


# Regra de Negócios: Reativação de Cliente

Um cliente pode ser _reativado_ se este não estiver com nenhuma parcela em atraso, para clientes do Plano Básico, ou se tiver apenas uma parcela em atraso, somente caso seja cliente do Plano Premium.
A reativação deve ser realizada pelo **Analista Financeiro** validado por permissão de acesso à tela destinada à este fim. Qualquer reativação só poderá ser realizada com aprovação do **Gerente de Contas**, validado por permissão especial.

**Parametrizações:**
- O limite de meses para cliente do Plano Básico é parametrável pela chave: `sistema.financeiro.quantidade_parcelas_minimas_reativacao_basico`, com valor padrão: 0 (três meses)
- O limite de meses para cliente do Plano Premium é parametrável pela chave: `sistema.financeiro.quantidade_parcelas_minimas_reativacao_premium`, com valor padrão: 1 (três meses)
- A operação vinculada a permissão para aprovação do Gerente de Contas tem o código: `4.35.194` - Aprovação para Reativação de Cliente

_[Sobre o Portal de Documentação](../../../About/About.md)_

![Rodape](../../../ReadMe-Anexos/Rodape.png)
