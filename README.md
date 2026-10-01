# Dashboard Executivo — Portfólio de Arquitetura

Dashboard executivo interativo criado para transformar uma base de projetos de um escritório de arquitetura em uma narrativa clara para investidores.

**Demo pública:** [Abrir dashboard no GitHub Pages](https://rubensplima.github.io/architecture-investor-dashboard/)

**Repositório:** [github.com/rubensplima/architecture-investor-dashboard](https://github.com/rubensplima/architecture-investor-dashboard)

> Os dados são inteiramente sintéticos e foram criados para demonstração e estudo analítico.

## O problema

Uma carteira de projetos pode parecer saudável pelo volume contratado e ainda esconder pressões de prazo, custo e margem. O objetivo deste projeto foi organizar esses sinais em uma visão que permitisse responder rapidamente:

- Qual é o tamanho econômico do portfólio?
- Quanto da receita futura já está contratado?
- Onde estão os maiores riscos de execução?
- Quais segmentos concentram valor?
- Que história os dados contam para um investidor?

## A solução

O dashboard combina análise operacional e narrativa executiva. Ele oferece filtros por segmento, status, risco, diretor, projeto e cliente, recalculando os indicadores e gráficos em tempo real.

Principais componentes:

- honorários contratados, receita reconhecida, backlog, margem e contas a receber;
- distribuição de projetos por status;
- comparação de honorários e backlog por segmento;
- gráfico de margem prevista versus desvio de prazo;
- ranking de projetos que exigem atenção;
- modo de apresentação com uma história em cinco capítulos.

## A história apresentada

1. **Escala:** o escritório construiu uma carteira relevante de contratos.
2. **Visibilidade:** parte importante do crescimento já está no backlog.
3. **Qualidade econômica:** a margem mostra uma operação atraente.
4. **Tensão:** o risco está na execução dos projetos críticos.
5. **Tese:** converter backlog, recuperar prazos e gerar recorrência.

## Tecnologias

- HTML5 semântico
- CSS responsivo
- JavaScript puro
- SVG para visualização de dados
- Nenhuma dependência externa

## Base de dados

A base contém 60 projetos fictícios e 37 campos financeiros, operacionais e de relacionamento com clientes. A posição é 31 de agosto de 2026 e os valores monetários estão em reais.

- [Baixar a base em Excel](data/base_projetos_arquitetura.xlsx)
- [Consultar o dicionário de dados](docs/dicionario-de-dados.md)

O arquivo Excel contém três abas:

- `Resumo`: principais indicadores com fórmulas auditáveis;
- `Projetos`: os 60 registros utilizados pelo dashboard;
- `Dicionario`: definição, tipo e finalidade de cada campo.

Para utilizar no Google Sheets, baixe o arquivo, abra o Google Drive e selecione **Novo → Upload de arquivo**. Depois, abra o `.xlsx` com o Google Planilhas. As fórmulas, datas, filtros e formatações principais são compatíveis com a importação.

## Executar localmente

Na pasta do projeto, rode:

```bash
python3 -m http.server 8000
```

Depois abra `http://localhost:8000`.

Também é possível abrir `index.html` diretamente no navegador.

## Publicar no GitHub Pages

1. Envie o projeto para um repositório público no GitHub.
2. Abra **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**.
4. Selecione a branch `main` e a pasta `/root`.
5. Salve e aguarde a publicação.

## Estrutura

```text
.
├── index.html          # estrutura da interface
├── styles.css          # identidade visual e responsividade
├── app.js              # filtros, cálculos, gráficos e narrativa
├── data.js             # base sintética incorporada
├── data/
│   └── base_projetos_arquitetura.xlsx
├── favicon.svg         # identidade do projeto
├── docs/
│   ├── memoria-de-calculo.md
│   ├── dicionario-de-dados.md
│   └── analise-e-insights.md
├── portfolio-entry.md  # texto pronto para o portfólio
└── README.md
```

## Documentação da análise

- [Memória de cálculo e regras de negócio](docs/memoria-de-calculo.md)
- [Dicionário de dados](docs/dicionario-de-dados.md)
- [Análise, insights e recomendações](docs/analise-e-insights.md)

Esses documentos registram a origem sintética da base, as fórmulas dos indicadores, as regras usadas no dashboard, a interpretação das visualizações, as decisões apoiadas e os próximos passos da solução.

## Decisões de design

A interface adota uma linguagem editorial e institucional: azul profundo para confiança, ciano para dados e laranja para tensão e oportunidade. O primeiro nível mostra os números essenciais; os gráficos explicam a carteira; o modo de apresentação transforma a análise em argumento.

## Autor

**Rubens Lima** — escritor, criador de conteúdo e estrategista de projetos digitais.

## Licença

Distribuído sob a licença MIT. Veja [LICENSE](LICENSE).
