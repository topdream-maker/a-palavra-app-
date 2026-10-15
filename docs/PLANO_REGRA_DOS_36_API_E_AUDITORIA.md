# Regra dos 36 — geração, auditoria e publicação

## Resposta direta

O aplicativo pode funcionar em modo estático, mas a aprovação da Regra dos 36 não acontece automaticamente dentro do navegador. O modo estático é adequado para **entregar e executar** conteúdo já aprovado. A geração e a auditoria devem acontecer antes da publicação, em uma pipeline separada.

A API não é obrigatória para a primeira prova de conceito. Ela se torna recomendável quando houver muitos estudos para gerar, repetir, comparar e auditar. Sem API, o processo pode ser feito manualmente em Manus ou outra IA, mas ficará menos automatizado e menos reprodutível.

## O que o contrato atual prova

`36_criterios_canonicos.json` é o contrato dos gates. Ele identifica os 36 critérios, preserva a ordem canônica e possui SHA-256 verificado pelo teste do GitHub.

Isso prova que o contrato não foi alterado acidentalmente. Ainda não prova que um estudo específico foi aprovado nos 36 critérios. Para isso, será necessário um resultado de auditoria por conteúdo.

## Pipeline correta

### 1. Definição do alvo

Para cada estudo, registrar passagem-alvo, tradução utilizada, intervalo de contexto, tipo de conteúdo e objetivo. O sistema não deve permitir que a IA escolha livremente uma passagem sem registro.

### 2. Geração

A IA produz um rascunho estruturado, por exemplo:

```json
{
  "id": "marcos-01-estudo-001",
  "reference": "Marcos 1:1-8",
  "explanation": "...",
  "application": "...",
  "summary": "...",
  "prayer": "..."
}
```

A geração deve guardar modelo, versão, data, prompt ou instruções, passagem de entrada e hash do resultado. Uma API facilita repetir esse processo em lote, mas a geração também pode ser feita manualmente por uma IA com os mesmos registros.

### 3. Auditoria automática

Um validador determinístico verifica formato, campos obrigatórios, referências, citações, limites de tamanho, ausência de chamadas proibidas e existência dos 36 resultados. Um auditor de linguagem pode auxiliar, mas não deve ser a única prova.

O resultado esperado por estudo é algo como:

```json
{
  "study_id": "marcos-01-estudo-001",
  "status": "pending_human_review",
  "gates": {
    "TARGET_FIDELITY": {"status": "pass", "evidence": "..."},
    "CONTEXT_FIDELITY": {"status": "review", "evidence": "..."}
  }
}
```

Nenhum estudo deve ir para o aplicativo se algum gate estiver `fail`, `unknown` ou `review` sem decisão humana registrada.

### 4. Revisão humana/editorial

Os critérios de fidelidade, escopo doutrinário e segurança pastoral não devem ser “aprovados” apenas por uma chamada de API. Uma pessoa responsável precisa revisar o estudo e registrar nome ou identificador do revisor, data, decisão, observações e versão revisada.

A aprovação humana não significa que o texto seja a única interpretação possível. Significa que ele passou pelo padrão editorial definido para este aplicativo.

### 5. Empacotamento estático

Somente estudos com auditoria completa e decisão humana `approved` entram em um arquivo público, por exemplo:

```text
content/studies-approved.json
content/studies-manifest.json
evidence/studies/<study-id>.json
```

O PWA continua estático. Ele não precisa chamar a API para exibir o estudo aprovado. O navegador apenas carrega o JSON aprovado e o service worker o armazena offline.

### 6. Validação no GitHub

O workflow deve bloquear o merge quando:

- o estudo não tiver todos os 36 gates;
- algum gate estiver diferente de `pass`;
- não existir revisão humana;
- o hash do conteúdo não coincidir com o manifesto;
- a referência bíblica não existir no corpus;
- o arquivo aprovado não corresponder ao relatório de auditoria.

## Três níveis de comprovação

### Integridade técnica

Comprovada por hashes, schema JSON, testes e workflow. Demonstra que o arquivo publicado é o arquivo auditado e que o corpus não mudou.

### Qualidade de aderência

Comprovada pelo relatório dos 36 gates, com evidência específica para cada critério e referência textual. Um simples `true` ou `pass` sem justificativa não é suficiente.

### Responsabilidade editorial

Comprovada pela revisão humana registrada. API, modelo de IA e teste automático ajudam, mas não substituem essa decisão.

## Onde a API entra

A API pode executar um serviço de geração/auditoria fora do PWA:

```text
passagem + instruções
        ↓
API de geração
        ↓
rascunho estruturado
        ↓
API ou script de auditoria
        ↓
relatório dos 36 gates
        ↓
revisão humana
        ↓
commit do conteúdo aprovado
        ↓
PWA estático/offline
```

A API deve ficar em um script, servidor ou CI protegido. A chave nunca deve ser enviada ao navegador nem gravada no repositório público.

## Decisão para este projeto

Hoje, o projeto ainda não possui estudos auditados nem o motor de auditoria dos 36 critérios. Portanto, a afirmação correta é: **o contrato dos 36 critérios está preservado e validado; a aprovação de conteúdos ainda não foi executada**.

Criar uma conta de API pode ser útil agora para preparar a pipeline, mas não é necessário para manter o leitor bíblico funcionando. A próxima implementação de alto valor seria um estudo-piloto, um schema de conteúdo e um relatório de auditoria de exemplo antes de gerar dezenas de estudos.
