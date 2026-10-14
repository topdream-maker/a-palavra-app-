# Evidências de teste v0.6

- PASSOU: integridade do corpus (66 livros, 1.189 capítulos, 31.102 registros).
- PASSOU: SHA-256 do corpus idêntico à versão 0.5.
- PASSOU: `node --check app.js` e `node --check sw.js`.
- PASSOU: integridade do arquivo ZIP.
- BLOQUEADO: execução automatizada do navegador Chromium. A tentativa Playwright recebeu `net::ERR_BLOCKED_BY_ADMINISTRATOR` para o servidor local.
- NÃO EXECUTADO: teste de instalação e uso offline no Android físico.
- NÃO CERTIFICADO: qualidade editorial de explicações, pois não foram incluídas.
