# Dashboard eleitoral 2026 — integração TSE

## Instalação no repositório `eleicoes2026`
Envie **todos os arquivos e pastas** deste pacote para a raiz do repositório, substituindo `index.html`, `app.js` e `styles.css`. Preserve a pasta `.github/workflows` e `scripts`.

No GitHub, abra **Actions → Atualizar apuracao TSE → Run workflow** para iniciar a primeira coleta. Em **Settings → Actions → General → Workflow permissions**, habilite **Read and write permissions** se o workflow não conseguir publicar os dados. A rotina roda no máximo a cada cinco minutos, com eventuais atrasos do GitHub.

O painel consulta `data/turno1.json` e `data/turno2.json` a cada 20 segundos. A fonte é `resultados.tse.jus.br`, no formato EA20. A atualização de dados **não** é garantida a cada 20 segundos. Não há previsão de resultado eleitoral.

**Limite atual:** coleta Brasil e as 27 UFs. A seleção de município só funcionará se você importar um JSON normalizado com registros municipais; a coleta automática dos municípios ainda não está implementada. As observações históricas do gráfico começam quando o navegador está aberto. Percentuais de abstenção são referentes às seções totalizadas quando a apuração é parcial.

A coleta exige GitHub Actions habilitado e pode falhar por indisponibilidade do TSE, limites de acesso ou mudanças no esquema. Em caso de falha, o último arquivo válido permanece no repositório.
