# Cortes Pó de Pólen no Vercel

Estrutura desta pasta (já pronta). O arquivo `index.html` e a pasta `api` precisam ficar no nível mais alto do repositório do GitHub, e não dentro de outra pasta:

- `index.html`: a página (fica na raiz, ao lado da pasta `api`).
- `api/analisar.js`: a função que guarda a chave da Anthropic.

## Antes de começar

1. Crie uma chave de API no console da Anthropic (console.anthropic.com) e defina lá um limite mensal de gasto.
2. Invente um código de acesso (uma senha simples). É o que você vai passar para quem for usar a ferramenta.
3. Tenha uma conta no Vercel (vercel.com).

## Caminho 1: pelo site do Vercel, com o GitHub

1. Crie um repositório no GitHub e envie o conteúdo desta pasta (`index.html`, a pasta `api` e este arquivo), direto na raiz do repositório.
2. No Vercel, clique em Add New > Project e escolha esse repositório.
3. Em Framework Preset, deixe "Other". Não precisa de comando de build.
4. Antes de clicar em Deploy, abra Environment Variables e crie duas variáveis:
   - `ANTHROPIC_API_KEY`: a chave do passo 1.
   - `ACCESS_CODE`: o código do passo 2.
5. Clique em Deploy. O Vercel entrega um endereço como `nome.vercel.app`.

## Caminho 2: pelo terminal, sem GitHub

Com o Node instalado, dentro desta pasta:

```
npm i -g vercel
vercel
vercel env add ANTHROPIC_API_KEY
vercel env add ACCESS_CODE
vercel --prod
```

O comando `vercel` pergunta algumas coisas na primeira vez (aceite os padrões). As variáveis só valem para os deploys feitos depois de criadas, por isso o último comando.

## Endereço próprio

No projeto, abra Settings > Domains, adicione por exemplo `cortes.nektardesign.com.br` e siga a instrução para criar o registro DNS no lugar onde o domínio `nektardesign.com.br` é gerenciado.

## Testar

Abra o endereço, clique em "Carregar exemplo", digite o código de acesso e clique em Analisar. Se aparecer "Acesso negado", confira o código; se a análise ficar sem resposta, veja os logs da função no painel do Vercel.

## Pontos de atenção

- **Tempo de execução.** A análise de um episódio inteiro pode levar de 1 a 2 minutos. A função responde em streaming, o que costuma ajudar, mas o limite de duração depende do seu plano do Vercel. Se a análise cair no meio, veja o limite no painel e, se precisar, divida a transcrição em blocos de uns 20 minutos.
- **Plano gratuito.** O plano gratuito do Vercel é voltado a uso pessoal. Confira nos termos se ele cobre o uso da Néktar.
- **Controle de uso.** Não há limite por pessoa. Se o código vazar, troque `ACCESS_CODE` no painel e faça um novo deploy.
- **Modelo.** O nome `claude-sonnet-5-5` está em `api/analisar.js` e em `CONFIG.model` no HTML. Confira na documentação da Anthropic se ainda é válido.
