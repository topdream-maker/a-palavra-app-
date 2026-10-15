# A Palavra — Manual de continuidade para outra IA

**Última atualização:** 15 de outubro de 2026  
**Branch de trabalho:** `main`  
**Repositório:** https://github.com/topdream-maker/a-palavra-app-  
**Último commit:** `2cbbd54` — separa os itens Sobre e Apoiar no menu

## Regra principal

Este projeto deve avançar de forma incremental. Não substituir o corpus bíblico, não inventar estudos temáticos e não declarar conteúdo como auditado sem fonte, revisão e registro. Antes de alterar o comportamento, ler `STATUS.md`, `TESTES.md` e este documento.

## Como abrir e validar

```bash
git clone https://github.com/topdream-maker/a-palavra-app-.git
cd a-palavra-app-
node --check app.js
node --check sw.js
node tests/validate-baseline.mjs
```

Para uma prévia local simples:

```bash
python3 -m http.server 8000 --bind 0.0.0.0
```

A aplicação precisa ser servida por HTTP ou HTTPS. Abrir `index.html` diretamente com `file://` não representa o comportamento real do PWA e impede o service worker.

## O que existe hoje

O aplicativo é um PWA estático em HTML, CSS e JavaScript, sem framework e sem backend obrigatório. O conteúdo bíblico fica em JSON local. O estado do usuário fica em `localStorage`.

Já estão implementados: Bíblia Livre N4 completa, busca local, seleção de livro e capítulo, acesso rápido aos capítulos, salto para versículo, resultados de busca que apontam para versículo, favoritos de capítulo, progresso do plano de Marcos, anotações, exportação/importação de backup, preferências, navegação offline e identidade visual com imagens WebP.

O leitor também possui marcação colorida por versículo. As marcações usam a chave local `ap-bible-highlights-v1` e não são sincronizadas entre dispositivos.

## Estrutura dos arquivos

- `index.html`: shell do PWA, cabeçalho, navegação inferior e menu lateral.
- `app.js`: renderização das telas, navegação, leitor bíblico, busca e persistência local.
- `styles.css`: identidade visual, responsividade, leitor, cartões e marcações.
- `sw.js`: instalação, atualização e cache offline.
- `manifest.webmanifest`: metadados de instalação.
- `data/biblia-livre-n4.json`: corpus completo usado pelo leitor.
- `data/marcos-n4.json`: corpus usado no plano de leitura de Marcos.
- `data/biblia-livre-n4-origem.json`: manifesto de origem do corpus.
- `36_criterios_canonicos.json`: contrato dos 36 gates canônicos.
- `tests/validate-baseline.mjs`: validação determinística sem dependências externas.
- `.github/workflows/validate.yml`: validação automática no GitHub Actions.
- `docs/AVALIACAO_PROJETO_2026-10-15.md`: diagnóstico técnico e riscos.
- `docs/ANALISE_MUSICA_INSTRUMENTAL.md`: decisão de licenciamento do áudio.

## Estado editorial

Os estudos temáticos ainda estão em preparação. Os temas atuais são apenas cartões de navegação visual. Não adicionar explicações religiosas, devocionais ou doutrinárias como se fossem conteúdo aprovado sem que o proprietário forneça ou aprove uma fonte e um fluxo editorial.

A Bíblia Livre N4 deve continuar com seus créditos e licença conforme já documentado no aplicativo e no manifesto de origem. Não misturar texto bíblico, conteúdo autoral novo e referências editoriais sem deixar a origem clara.

## Estado visual

A tela inicial usa `assets/hero-paz-piloto.webp`. A tela de reflexão usa `assets/reflexao-paz-piloto.webp`. O apoio institucional usa `assets/quadro-institucional-piloto.webp`. Os cartões de temas reutilizam essas imagens com gradientes; não gerar novas imagens sem necessidade, pois a cota de geração foi limitada anteriormente.

## Música ambiente

Não há áudio distribuído atualmente. O arquivo anterior foi removido porque não havia comprovação suficiente de autorização de redistribuição.

A música só pode entrar depois de registrar título, autor, URL original, licença, data de obtenção, hash SHA-256 e autorização compatível com distribuição dentro de um aplicativo. Ver `docs/ANALISE_MUSICA_INSTRUMENTAL.md`.

O recurso deve ser opcional, desligado por padrão, sem autoplay e com volume baixo. Não baixar uma faixa chamada apenas “copyright free” sem conferir a licença individual.

## GitHub e publicação

O remoto atual é `https://github.com/topdream-maker/a-palavra-app-.git`. A branch `main` está limpa e os commits recentes já foram enviados. O workflow de validação tem permissão somente de leitura e está passando.

A prévia do sandbox é temporária:

https://8000-i3in7xqq4s50aal1hmxei-34172223.us4.manus.computer/?v=2cbbd54

Ela não deve ser tratada como endereço permanente de produção. GitHub Pages ainda não foi habilitado por falta do escopo necessário na integração utilizada anteriormente. A publicação permanente pode ser feita pelo proprietário no GitHub Pages ou em outro host estático.

## API: decisão para continuidade

O aplicativo não precisa de API hoje. Ele funciona como site estático e offline.

Uma conta ou chave de API só faz sentido se o projeto passar a ter, por exemplo, sincronização de anotações, contas de usuário, painel administrativo, geração de estudos, automações ou integração com Manus. Para uma integração própria com Manus, a documentação atual orienta usar API v2, o endereço `https://api.manus.ai` e a chave no header `x-manus-api-key`. A chave deve ficar no servidor ou em variável de ambiente, nunca no `app.js`, `index.html`, localStorage ou repositório público.

É permitido criar a conta de API agora, mas não é necessário nem recomendável gerar uma chave apenas por precaução. Primeiro definir a função que consumirá a API, o local seguro do backend e o orçamento/limite de uso. Se a API for criada, registrar apenas o nome do serviço e a finalidade no projeto; nunca registrar a chave.

## Próximos passos recomendados

1. Testar no Android a instalação, leitura offline, marcações, anotações e reabertura.
2. Escolher hospedagem permanente.
3. Testar atualização do service worker em duas versões consecutivas.
4. Definir um único tema-piloto com fonte e revisão antes de escrever os demais.
5. Se a música for desejada, obter uma faixa com licença documentada ou encomendar uma faixa original.
6. Só criar backend/API quando uma dessas funções realmente for aprovada.

## Critérios de aceite antes de declarar pronto

A nova versão deve passar `node --check app.js`, `node --check sw.js`, `node tests/validate-baseline.mjs` e o workflow do GitHub. No navegador, deve abrir Bíblia, trocar livro, trocar capítulo, saltar para versículo, marcar e desmarcar um versículo, pesquisar uma palavra, abrir o resultado direto, navegar para Sobre e Apoiar o projeto separadamente.

No Android, deve ser possível instalar, abrir sem rede, ler o corpus, marcar versículos, salvar anotação, fechar e reabrir sem perda dos dados locais.

## O que não fazer

Não colocar chaves de API no frontend. Não reintroduzir o áudio sem licença. Não substituir o corpus por uma tradução sem verificar licença. Não usar publicidade ou Pix dentro da tela Sobre. Não apagar dados locais do usuário em uma atualização. Não transformar os cartões “Em preparação” em estudos inventados.
