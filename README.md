# Calendário da B3 — Monitor de Ativos

Arquivo público com os dias **sem pregão** da B3, lido pelo app Monitor de Ativos.

- Endereço usado pelo app:
  `https://raw.githubusercontent.com/jeanbsouza-sys/calendar-b3-monitor-ativos/main/calendario-b3.json`
- O app consulta este arquivo uma vez por dia **a partir de 20/12** (procurando o ano seguinte) e sempre que o
  ano atual ainda não tiver sido importado. Quando encontra um ano novo e válido, importa e usa no lugar do
  calendário calculado (que continua como reserva, junto com a detecção automática de dia sem pregão).

## Como atualizar (quando a B3 divulgar o calendário do ano seguinte, normalmente em dezembro)
1. Ler o Ofício Circular da B3 "Calendário de feriados em AAAA" (b3.com.br › Notícias / Ofícios e Comunicados).
2. Em `anos`, acrescentar o ano novo **sem apagar os anteriores**:
   - `semPregao`: todos os dias **úteis** sem sessão de negociação no segmento Listado (data `AAAA-MM-DD` e nome).
     Feriados que caem em sábado/domingo podem ficar de fora. Feriados de São Paulo com pregão normal (25/01, 09/07)
     **não** entram.
   - `aberturaTardia`: dias com pregão mais tarde (ex.: Quarta-feira de Cinzas, `"abre": "13:00"`).
   - `fonte`: número do Ofício Circular.
3. Atualizar `atualizado` com a data de hoje.
4. Conferir que o arquivo continua um JSON válido (ex.: jsonlint.com) e salvar no ramo `main`.

O app rejeita um ano com menos de 8 dias, com datas fora do próprio ano ou com datas inválidas — nesse caso
continua usando o cálculo e registra o motivo no Diagnóstico.
