# A Palavra — Aprendendo as Escrituras

Aplicativo gratuito de leitura e estudo bíblico, com a Bíblia Livre N4 e recursos offline.

Projeto em desenvolvimento.

## Baseline técnica importada

A branch `baseline-v0.6-import` contém a baseline técnica do PWA: leitura da Bíblia Livre N4 local, busca, progresso, favoritos, anotações, backup, manifesto PWA e service worker.

Consulte `docs/IMPORTACAO_BASELINE_V0.6.md`, `STATUS.md` e `TESTES.md` para o estado real. A implementação da Regra dos 36 e os estudos certificados ainda não fazem parte desta baseline.

## Validação automática

A branch `stabilize-baseline` adiciona `36_criterios_canonicos.json`, um validador determinístico sem dependências externas e o workflow `.github/workflows/validate.yml`. Isso verifica a integridade básica da baseline e do contrato canônico; não significa que a auditoria editorial dos estudos já esteja implementada.
