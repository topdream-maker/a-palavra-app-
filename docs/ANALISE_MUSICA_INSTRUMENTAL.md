# Música instrumental ambiente — decisão de distribuição

## Decisão atual

A música ambiente **não deve ser adicionada ainda**. O aplicativo pode receber áudio, mas somente depois que a faixa escolhida tiver autor, página original, licença, autorização de redistribuição e comprovante arquivados no projeto.

A expressão “sem copyright” ou “royalty-free” não é suficiente. Ela pode significar apenas que o uso é gratuito dentro de determinadas condições, sem transferir todos os direitos.

## O que a pesquisa mostrou

O Pixabay permite usar conteúdo gratuitamente e, em regra, não exige atribuição. Entretanto, a própria licença proíbe distribuir o conteúdo em formato standalone, isto é, praticamente na mesma forma em que foi obtido. Como o PWA precisa carregar um arquivo de áudio dentro do pacote público, essa opção exige análise da faixa e dos termos completos; por isso não é a opção mais segura para a primeira versão. [1]

A Creative Commons informa que cada faixa precisa ser analisada pela licença específica. Licenças com `NC` podem impedir uso comercial ou situações que envolvam vantagem financeira; licenças com `ND` não permitem adaptações e sincronizações; e toda licença `BY` exige atribuição adequada. [2]

O Free Music Archive explica que a licença deve ser verificada na página da própria faixa, e que filtros por licença ajudam a separar CC0, CC BY e outras modalidades. Para o aplicativo, a escolha mais simples seria uma faixa CC0 ou uma faixa CC BY 4.0, desde que a atribuição fique visível dentro de “Recursos” ou “Sobre a música”. [3]

## Opções aceitáveis

A ordem de segurança recomendada é:

1. **Faixa original encomendada ou criada para o projeto**, com autorização escrita de uso, modificação e redistribuição.
2. **Faixa CC0 ou domínio público**, com registro da página, autor e data de obtenção.
3. **Faixa CC BY 4.0**, com crédito completo dentro do aplicativo e no repositório.
4. Licença comercial específica que permita distribuição dentro de aplicativos e uso offline.

Devem ser evitadas, nesta fase, faixas `NC`, `ND`, `SA` ou de sites que apenas afirmem “copyright free” sem licença individual clara. O risco é maior porque o projeto pode futuramente receber apoio voluntário, publicidade ou outra forma de sustentabilidade.

## Como a faixa será incorporada quando aprovada

O arquivo ficará em `assets/audio/` com nome estável. O projeto receberá um arquivo `docs/AUDIO_CREDITS.md` contendo título, autor, URL original, licença, data de download, hash SHA-256 e observações sobre edição. A tela de recursos exibirá os créditos e permitirá desligar a música.

A música deverá ser opcional, desligada por padrão, com volume baixo e persistência local da preferência. Isso evita iniciar áudio automaticamente e respeita o usuário, o navegador e o consumo de bateria.

## Conclusão

A decisão técnica correta neste momento é **não incluir uma faixa encontrada na internet sem rastreabilidade**. A estrutura do aplicativo já está preparada para receber o recurso depois; a pendência atual é documental, não de programação.

## Referências

[1]: https://pixabay.com/service/license-summary/ "Pixabay Content License Summary"
[2]: https://creativecommons.org/legalmusicforvideos/ "Creative Commons — Legal Music For Videos"
[3]: https://freemusicarchive.org/faq/ "Free Music Archive — FAQ e licenças"
