# Evidências de teste

## Passou

- Integridade do corpus: 66 livros, 1.189 capítulos e 31.102 versículos.
- SHA-256 dos 36 gates canônicos conforme contrato.
- `node --check app.js` e `node --check sw.js`.
- Validador determinístico `tests/validate-baseline.mjs`.
- Prévia HTTP responde com status 200.
- Imagens WebP da tela inicial, reflexão e quadro institucional respondem com status 200.
- Navegação visual verificada: tela inicial, temas, recursos, Sobre e Apoiar o projeto.
- Leitor bíblico atualizado com acesso rápido a capítulos, seletor de versículos e marcação colorida persistente.
- Cartões dos temas verificados com fundos visuais e texto legível na prévia.

## Pendente

- Instalação e uso offline em um Android físico.
- Verificação de atualização do service worker após nova versão.
- Publicação permanente em host estático.
- Auditoria editorial de estudos e explicações.
- Confirmação documental da licença do áudio ambiente.

## Observação

A tentativa anterior de automatizar Chromium diretamente contra o servidor local recebeu `net::ERR_BLOCKED_BY_ADMINISTRATOR`; a prévia navegável do sandbox foi usada para inspeção visual manual assistida.
