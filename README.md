# Pulso — Dashboard de operações

[Acessar o dashboard](https://alexmanhes.github.io/pulso-operacoes/)

Dashboard demonstrativo em português, sem dependências de execução ou build. Indicadores e gráficos são calculados a partir de uma base fictícia de 200 dias, gerada de forma reproduzível por data.

## Funcionalidades

- Visão geral com volume, conclusões, prazo e ciclo médio; comparação com janela anterior do mesmo tamanho.
- Filtros globais por período, unidade, tipo e status. A busca por código, cliente e responsável também afeta indicadores e exportações.
- Períodos de 7, 30 e 90 dias e intervalo personalizado, com validação das datas.
- Gráfico de volume com séries alternáveis, agrupamento diário, semanal e mensal, consulta de valores e tabela acessível dos dados.
- Distribuição de status, desempenho por unidade e composição por tipo; gráficos permitem filtrar o recorte.
- Tabela com ordenação, paginação, busca e detalhes de cada operação.
- CSV em UTF-8 com BOM, separador ponto e vírgula, tratamento de aspas e proteção contra fórmulas de planilha.
- Relatório HTML independente com filtros, metodologia, indicadores, unidades e todos os registros do recorte.

## Metodologia

O período filtra a **data de abertura**, no fuso de Brasília. O status é apurado até 23:59:59 da data final. Conclusões posteriores não são antecipadas. No gráfico de volume, abertas e concluídas são agrupadas pela data de abertura, e não pela data da conclusão.

Taxa de conclusão = concluídas / total filtrado. Conclusões no prazo = concluídas até o prazo / todas as concluídas. Canceladas são excluídas da taxa de prazo. O ciclo médio usa horas corridas entre abertura e conclusão, somente para concluídas. Sem denominador, a interface mostra traço; não inventa zero desempenho.

A comparação usa os mesmos filtros em uma janela anterior de duração idêntica. Se a base não cobre a janela completa, a comparação é ocultada. Variações de prazo são expressas em pontos percentuais; ciclo em diferença de horas. Base anterior de zero não gera uma porcentagem de variação infinita.

Todos os dados são fictícios. A aplicação não se conecta a serviços, não envia registros a empresas e não permite editar operações. As preferências de filtros podem ficar no armazenamento local do navegador; a base é gerada novamente ao abrir, com referência ao dia corrente. Não há autenticação de usuários ou sincronização de dados.

## Executar e verificar

```sh
node serve.cjs
```

Abra `http://127.0.0.1:8810`. Sirva a raiz do projeto em uma hospedagem estática.

```sh
node --check js/model.js
node --check js/app.js
node tests/model.cjs
```

Os testes cobrem datas e fuso, coortes, status históricos, denominadores, filtros, comparação, agrupamentos, integridade da base e exportações.

```text
index.html
css/styles.css
js/model.js       # Dados, cálculos, filtros e exportações
js/app.js         # Interface e gráficos SVG
assets/favicon.svg
tests/model.cjs
serve.cjs
```

Fontes DM Sans e Manrope carregadas do Google Fonts, com alternativas do sistema. Gráficos locais em SVG, sem biblioteca ou serviço externo.


## GitHub Pages

Publicação estática pela branch main, pasta / (root). O arquivo .nojekyll mantém os arquivos como estão. Não há dependências, servidor de aplicação ou etapa de build.
