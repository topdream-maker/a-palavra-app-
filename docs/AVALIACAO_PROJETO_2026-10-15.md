# Avaliação técnica — A Palavra

**Data:** 15 de outubro de 2026  
**Base avaliada:** branch `main`, commit `ac03182`  
**Escopo:** PWA estático, Bíblia N4, navegação, persistência local, identidade visual e preparação para publicação.

## Veredito executivo

O projeto é **viável e já possui uma base funcional demonstrável**. A leitura bíblica, a busca local, marcadores, jornada, anotações, backup local e navegação principal estão implementados. A identidade visual também já está coerente entre a tela inicial, reflexão, apoio institucional e temas.

Ele ainda não deve ser tratado como produto final por quatro motivos: **conteúdo temático não auditado**, **teste físico Android/offline pendente**, **publicação permanente ainda não habilitada** e **contrato editorial dos estudos ainda incompleto**.

## Classificação atual

| Área | Situação | Avaliação |
|---|---|---|
| Leitura da Bíblia N4 | Implementada | 66 livros, 1.189 capítulos e 31.102 versículos validados |
| Busca e navegação | Implementada | Busca local e navegação de capítulos presentes |
| Jornada, favoritos e anotações | Implementada | Persistência local e exportação/importação disponíveis |
| Identidade visual | Em evolução avançada | Tela inicial, reflexão, apoio e temas já possuem linguagem consistente |
| Offline/PWA | Implementado com risco corrigido nesta etapa | Cache e atualização precisam ser tratados com versionamento confiável |
| Conteúdo de estudos | Pendente | Não deve ser inventado nem apresentado como auditado |
| Direitos do áudio | Bloqueado | O arquivo não tinha licença/metadados suficientes e permanece fora da distribuição |
| Publicação permanente | Pendente | O GitHub Pages não pôde ser habilitado pelo escopo atual do token |
| Teste real em Android | Pendente | Precisa ser feito no aparelho antes de declarar pronto |

## Pontos fortes

1. O corpus bíblico tem integridade estrutural verificada automaticamente.
2. O projeto evita fabricar explicações religiosas e identifica o que ainda está em preparação.
3. A aplicação é estática, sem backend obrigatório, o que reduz custo operacional.
4. As imagens foram otimizadas para WebP e mantidas leves para um PWA.
5. O código possui workflow determinístico no GitHub Actions.
6. A baseline está preservada no GitHub e as mudanças estão em commits pequenos e rastreáveis.

## Riscos que podem causar problemas futuros

### Alto impacto

- **Conteúdo editorial:** os temas e explicações ainda não têm textos aprovados, fonte, revisão e rastreabilidade. A solução é criar um fluxo editorial antes de liberar estudos.
- **Distribuição:** sem hospedagem permanente, o link atual é apenas uma prévia temporária. É necessário habilitar GitHub Pages ou escolher outro host estático.
- **Offline em dispositivo real:** o comportamento em Android, instalação, atualização do service worker e armazenamento local ainda precisam de teste físico.

### Médio impacto

- **Atualização do cache:** parâmetros de versão no HTML podem fazer recursos novos não coincidirem com chaves antigas do Cache Storage. Esta etapa corrige a estratégia.
- **Crescimento do corpus:** carregar a Bíblia inteira no navegador é aceitável para a baseline, mas busca e memória devem ser medidas em celulares simples.
- **Privacidade:** anotações, favoritos e progresso são locais, mas isso precisa continuar explícito ao usuário; não há sincronização nem recuperação em outro aparelho.

### Baixo impacto

- O áudio ambiente continua ausente até existir licença verificável.
- Os quadros institucionais são visuais, não anúncios conectados a uma rede de publicidade.
- O código ainda está concentrado em poucos arquivos; uma refatoração só será necessária quando o conteúdo crescer.

## O que já é fácil fazer

- adicionar novos cartões e imagens leves;
- publicar a pasta como site estático;
- criar testes determinísticos de arquivos, corpus e referências;
- substituir ou reativar o áudio quando a licença for comprovada;
- criar temas como dados estruturados, desde que os textos sejam fornecidos e auditados.

## O que exige mais cuidado

- elaborar estudos bíblicos confiáveis;
- fazer revisão doutrinária/editorial;
- definir direitos autorais de textos, imagens, músicas e fontes;
- sincronizar dados entre dispositivos;
- habilitar autenticação, conta ou pagamentos;
- declarar o produto como pronto para uso amplo.

## Próximas prioridades recomendadas

1. Corrigir e testar atualização/offline do service worker.
2. Fazer teste manual no Android: instalar, abrir offline, ler Bíblia, salvar anotação, fechar e reabrir.
3. Escolher e habilitar uma hospedagem permanente.
4. Definir o contrato editorial de um único tema-piloto antes de escrever os demais.
5. Criar a matriz de fontes e revisão para cada conteúdo temático.
6. Só depois expandir publicidade, apoio financeiro ou sincronização.

## Conclusão

**É possível concluir o aplicativo.** A parte técnica atual é de dificuldade baixa a média; o maior risco não é programação, mas governança de conteúdo, direitos de distribuição, teste real e publicação permanente. O caminho recomendado é continuar incrementalmente, mantendo o app como leitura bíblica offline funcional enquanto os estudos são preparados com rastreabilidade.
