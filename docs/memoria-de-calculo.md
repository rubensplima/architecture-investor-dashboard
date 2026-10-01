# Memória de cálculo e regras de negócio

## 1. Objetivo

Este documento descreve como os indicadores do Dashboard Executivo — Portfólio de Arquitetura são calculados. A posição analítica é 31 de agosto de 2026, os valores monetários estão em reais e todos os dados são sintéticos.

Os filtros de segmento, status, risco, diretor e busca por projeto ou cliente redefinem o conjunto analisado. Depois de cada seleção, todos os indicadores e gráficos são recalculados sobre os registros filtrados.

## 2. Indicadores principais

| Indicador | Cálculo | Regra de negócio | Resultado geral |
|---|---|---|---:|
| Projetos ativos | Contagem dos projetos com status `Em andamento` ou `Em espera` | Projetos concluídos e cancelados não são considerados ativos | 33 |
| Honorários contratados | `Σ Honorarios Contratados` | Valor comercial total da carteira selecionada | R$ 109,58 mi |
| Receita reconhecida | `Σ Receita Reconhecida` | Receita apropriada até a data de corte | R$ 70,46 mi |
| Conversão do contratado | `Receita reconhecida ÷ Honorários contratados` | Percentual da carteira já convertido em receita | 64,3% |
| Backlog | `Σ Backlog` | Receita contratada ainda não reconhecida; na geração da base, corresponde ao saldo não convertido, limitado a zero | R$ 39,60 mi |
| Custo projetado final | `Σ Custo Projetado Final` | Estimativa de custo para concluir a carteira | R$ 73,04 mi |
| Margem prevista consolidada | `(Honorários contratados − Custo projetado final) ÷ Honorários contratados` | Calculada sobre os totais, não pela média simples das margens individuais | 33,3% |
| Valor a receber | `Σ Valor Faturado − Σ Valor Recebido` | Considera somente valores já faturados e ainda não recebidos | R$ 8,34 mi |
| Projetos em risco alto | Contagem de registros com `Risco = Alto` | A classificação de risco pertence à base simulada | 26 |
| Projetos com atraso crítico | Contagem de projetos não concluídos e não cancelados com `Desvio Prazo (dias) > 30` | O limite gerencial adotado é 30 dias | 20 |
| Satisfação média | `Σ Satisfacao Cliente ÷ quantidade de projetos com nota` | Média simples, em escala de 0 a 10 | 8,23 |

## 3. Cálculos no nível do projeto

| Campo | Fórmula ou interpretação |
|---|---|
| Desvio de prazo | `Fim Revisado − Fim Previsto`, em dias |
| Desvio de progresso | `Progresso Real − Progresso Planejado` |
| Margem prevista | `(Honorários Contratados − Custo Projetado Final) ÷ Honorários Contratados` |
| Margem atual | `(Receita Reconhecida − Custo Real) ÷ Receita Reconhecida` |
| Desvio de horas | Relação entre horas realizadas e o consumo esperado para o progresso do projeto |
| Valor a receber | `Valor Faturado − Valor Recebido` |

## 4. Priorização dos projetos

A tabela **Projetos que exigem atenção** ordena a carteira por uma pontuação técnica usada apenas para priorização visual:

```text
Pontuação =
  10.000.000, se o risco for Alto
  + máximo(0, dias de atraso) × 50.000
  + honorários contratados
```

São exibidos os 12 projetos com maior pontuação dentro da seleção atual. A pontuação não representa valor financeiro, probabilidade estatística de perda nem recomendação de investimento. Ela somente combina criticidade, atraso e relevância econômica para direcionar a atenção gerencial.

## 5. Lógica das visualizações

### Composição do portfólio

Agrupa e conta os projetos por status. O percentual de cada grupo é calculado sobre a quantidade de projetos da seleção.

### Escala por segmento

Agrupa os registros por segmento e soma honorários e backlog. O comprimento máximo das barras é normalizado pelo segmento com maior volume de honorários.

### Margem prevista versus desvio de prazo

- eixo horizontal: `Desvio Prazo (dias)`;
- eixo vertical: `Margem Prevista`;
- tamanho do círculo: proporcional à raiz quadrada dos honorários contratados;
- destaque visual: projetos classificados como risco alto.

A raiz quadrada reduz a diferença visual entre contratos muito grandes e pequenos sem eliminar a percepção de escala.

## 6. Regras de exibição

- valores monetários são abreviados em milhões de reais;
- percentuais são exibidos com uma casa decimal;
- margens inferiores a 30% recebem atenção no KPI consolidado;
- margens individuais inferiores a 25% recebem destaque na tabela;
- atrasos superiores a 30 dias recebem destaque negativo;
- registros sem valor numérico válido são desconsiderados nas médias.

## 7. Validações recomendadas

Em uma implantação real, os seguintes controles deveriam ocorrer antes da atualização do dashboard:

1. verificar unicidade do `ID Projeto`;
2. validar datas e a coerência entre início, fim previsto e fim revisado;
3. impedir valores recebidos superiores aos faturados sem justificativa;
4. reconciliar backlog com contrato, aditivos e receita reconhecida;
5. exigir preenchimento do prazo contratual;
6. revisar projetos concluídos ou cancelados que ainda apresentem backlog;
7. documentar formalmente os critérios da classificação de risco.

## 8. Limitações

- a base é sintética e serve exclusivamente para estudo;
- não há série histórica mensal;
- `Prazo Contratual (meses)` não está preenchido na versão utilizada;
- risco e probabilidade de renovação não derivam de modelos estatísticos;
- não há dados de impostos, capital de giro ou fluxo de caixa;
- margem prevista é uma estimativa e não substitui a margem realizada.

