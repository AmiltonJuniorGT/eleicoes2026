# Dashboard eleitoral 2026

Aplicação estática para GitHub Pages. Arquivos: `index.html`, `styles.css`, `app.js`.

## Publicação
Coloque os três arquivos na raiz de um repositório GitHub e ative Settings > Pages > Deploy from branch.

## Dados e limitações
A aplicação **não contém endpoint oficial pré-configurado**, pois o esquema e a permissão CORS de uma API de apuração em tempo real não foram validados. Não faz scraping do G1. Pode importar JSON normalizado ou consultar uma URL HTTPS que retorne JSON no formato abaixo, com atualização a cada 20 segundos. O servidor deve permitir CORS. Sem isso, a atualização ao vivo não funcionará. Dados oficiais históricos podem ser obtidos em https://dadosabertos.tse.jus.br/dataset/resultados-2026 , mas CSVs brutos exigem transformação prévia.

Exemplo **fictício de estrutura** (não são votos reais):
```json
{
 "updatedAt":"2026-10-25T17:00:00-03:00",
 "turn":2,
 "places":[
  {"id":"BR","name":"Brasil","uf":"BR","city":"","electorate":1000,"absent":200,"blank":10,"nullVotes":10,"sectionsTotal":10,"sectionsCount":10,"candidates":[{"id":"13","name":"Candidato A","votes":390},{"id":"22","name":"Candidato B","votes":390}]},
  {"id":"PE","name":"Pernambuco","uf":"PE","city":"","electorate":100,"absent":20,"blank":1,"nullVotes":1,"sectionsTotal":1,"sectionsCount":1,"candidates":[{"id":"13","name":"Candidato A","votes":40},{"id":"22","name":"Candidato B","votes":38}]},
  {"id":"PE-RECIFE","name":"Recife","uf":"PE","city":"Recife","electorate":50,"absent":10,"blank":1,"nullVotes":1,"sectionsTotal":1,"sectionsCount":1,"candidates":[{"id":"13","name":"Candidato A","votes":20},{"id":"22","name":"Candidato B","votes":18}]}
 ]
}
```

**Não misture níveis geográficos ao agregar**: se incluir linha BR e linhas UF, o painel usa BR para total nacional; se incluir linha UF e linhas municipais, usa UF para o estado. Identificadores de candidatos devem ser iguais nos dois turnos. Abstenção exige eleitores aptos e ausentes efetivamente conhecidos; não deduza ausentes de dados parciais sem confirmação. O histórico é local, começa quando o painel recebe dados, não recupera consultas anteriores e não é persistido entre navegadores. A atualização de 20 s é uma frequência de consulta, não garantia de novos dados.

## Próxima integração
É necessário confirmar o esquema oficial de arquivos JSON do TSE e CORS, ou implantar um adaptador confiável que publique JSON normalizado. O CSV consolidado por município do TSE também pode ser transformado em JSON com um script de ETL. O painel não estima vencedor nem inventa valores ausentes.
