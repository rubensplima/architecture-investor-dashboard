# Dicionário de dados

## 1. Fonte e escopo

A fonte é uma base sintética criada para um exercício de mentoria em análise e visualização de dados. Ela simula a carteira de um escritório brasileiro de arquitetura, com 60 projetos distribuídos por oito segmentos. Nenhum cliente, contrato ou valor corresponde a uma organização real.

No repositório, os registros estão disponíveis em dois formatos:

- `data.js`, usado diretamente pela aplicação web;
- `data/base_projetos_arquitetura.xlsx`, preparado para Excel e importação no Google Sheets.

A data de referência é 31 de agosto de 2026.

## 2. Campos da base de projetos

| Campo | Tipo | Descrição |
|---|---|---|
| `ID Projeto` | Texto | Identificador único no formato `ARQ-000` |
| `Projeto` | Texto | Nome fictício do empreendimento |
| `Cliente` | Texto | Nome fictício do cliente contratante |
| `Segmento` | Categoria | Segmento do empreendimento: hotelaria, hospitalar, urbanismo, residencial, industrial, varejo, corporativo ou educacional |
| `Cidade` | Texto | Município de localização do projeto |
| `UF` | Texto | Unidade federativa do projeto |
| `Diretor` | Texto | Diretor responsável pela conta ou carteira |
| `Gerente` | Texto | Gerente responsável pela execução |
| `Fase Atual` | Categoria | Etapa atual, como estudo preliminar, anteprojeto, projeto legal, projeto executivo, compatibilização ou acompanhamento de obra |
| `Status` | Categoria | Situação operacional: em andamento, em espera, concluído ou cancelado |
| `Risco` | Categoria | Classificação simulada de risco: baixo, médio ou alto |
| `Data Inicio` | Data | Data de início do projeto |
| `Prazo Contratual (meses)` | Número inteiro | Duração prevista em contrato; não preenchida nesta versão da base |
| `Fim Previsto` | Data | Data originalmente prevista para encerramento |
| `Fim Revisado` | Data | Previsão mais recente para encerramento |
| `Desvio Prazo (dias)` | Número inteiro | Diferença, em dias, entre fim revisado e fim previsto; valor negativo indica antecipação |
| `Progresso Planejado` | Decimal | Avanço planejado na data de corte, de 0 a 1 |
| `Progresso Real` | Decimal | Avanço efetivamente realizado, de 0 a 1 |
| `Desvio Progresso` | Decimal | Progresso real menos progresso planejado |
| `Honorarios Contratados` | Moeda | Valor total contratado pelo escritório |
| `Receita Reconhecida` | Moeda | Receita apropriada contabilmente até a data de corte |
| `Valor Faturado` | Moeda | Valor de notas ou cobranças emitidas |
| `Valor Recebido` | Moeda | Valor efetivamente recebido do cliente |
| `Backlog` | Moeda | Saldo contratado ainda não reconhecido como receita |
| `Custo Orcado` | Moeda | Custo total previsto no orçamento original |
| `Custo Real` | Moeda | Custo incorrido até a data de corte |
| `Custo Projetado Final` | Moeda | Estimativa atual do custo total ao término |
| `Margem Prevista` | Decimal | Margem estimada ao término do projeto |
| `Margem Atual` | Decimal | Margem observada sobre receita e custo realizados |
| `Horas Planejadas` | Número | Total de horas planejadas para o projeto |
| `Horas Realizadas` | Número | Horas trabalhadas até a data de corte |
| `Desvio Horas` | Decimal | Desvio proporcional do consumo de horas em relação ao avanço esperado |
| `Alteracoes de Escopo` | Número inteiro | Quantidade de mudanças de escopo registradas |
| `Satisfacao Cliente` | Decimal | Avaliação simulada do cliente, de 0 a 10 |
| `Probabilidade Renovacao` | Decimal | Estimativa simulada de renovação, de 0 a 1 |
| `Observacao Executiva` | Texto | Síntese qualitativa sobre o projeto |
| `Ultima Atualizacao` | Data | Data da última atualização do registro |

## 3. Dimensões analíticas

Os filtros do dashboard utilizam quatro dimensões principais:

- segmento;
- status;
- risco;
- diretor.

A busca textual considera `Projeto`, `Cliente` e `ID Projeto`.

## 4. Medidas principais

As medidas financeiras são honorários, receita, faturamento, recebimento, backlog, custos e margens. As medidas operacionais são prazo, progresso, horas, alterações de escopo e risco. Satisfação e probabilidade de renovação representam a dimensão de relacionamento com o cliente.

## 5. Tratamento e qualidade

- datas seguem o padrão ISO `AAAA-MM-DD`;
- valores monetários são números inteiros em reais;
- percentuais e progressos são armazenados entre 0 e 1;
- a aplicação converte os valores para reais, milhões e percentuais apenas na apresentação;
- campos vazios ou não numéricos não participam das médias;
- nomes e entidades são fictícios e foram mantidos apenas para dar realismo ao exercício.
