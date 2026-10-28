# Power Automate flows / Fluxos de Power Automate

Blueprints reconstructed from the production flows, with identifiers and destinations removed.
Planos reconstruídos a partir dos fluxos de produção, sem identificadores nem destinos.

## Flow 1 – Daily sales digest (runs every morning, local time)

1. **Refresh** the sales semantic model, then **wait** for it to finish.
2. In parallel, run **DAX queries** against the model: daily billing, monthly billing, unbilled balance, billing by marketplace, goods rejected.
3. **Parse** each JSON result, **format** values and dates, build HTML/table blocks (balance table, marketplace table, rejected-goods table).
4. **Post** a message and an adaptive **card** to the sales channel, with short delays between posts to keep order.
5. A second business unit gets its own daily and monthly query and card.
6. **Error handling** – if the daily/monthly queries fail, time out or are skipped, a message is posted to the channel instead of silent failure.

## Flow 2 – Customer-service file refresh (runs every morning)

1. Run **DAX queries** against the service model for: protocols of the last 7 days, protocols of yesterday, deadline list and cancellations.
2. **Format** each result (SKU and protocol lists).
3. A **condition** checks that all four results succeeded.
4. **Wait** 45 minutes, so that downstream files are ready, then **read** the generated file content.

## Patterns worth reusing

- *Refresh, wait, query* – the message is built from fresh data.
- *Query the model, not the source* – numbers in Teams equal numbers in the report.
- *Fail loudly* – every critical branch has a failure notification.
