# Rodrigo Andrade — Links

Site de Rodrigo Andrade, fisioterapeuta em São Luís, MA, com foco em reabilitação de joelho. Este repositório guarda a configuração e os arquivos da marca. O aplicativo e seus testes ficam em [WiltonV/central-links](https://github.com/WiltonV/central-links).

- `site.config.json`: perfil, links, cores, SEO, endereço e recursos.
- `public/`: foto, logos e demais arquivos exclusivos deste profissional.
- `central.config.json`: SHA completo da versão aprovada da central.

GitHub Pages: `https://rodrigosousafisio.github.io/Links/`. O caminho `/Links` diferencia maiúsculas de minúsculas.

## Desenvolvimento

Requer Node.js 20.19 ou superior, Git e Corepack/Yarn disponíveis (`corepack enable`). Não é necessário instalar dependências na raiz deste repositório.

```sh
npm run dev
```

O comando busca a revisão aprovada da central, combina com a configuração local em `.site/`, instala as dependências desse aplicativo gerado e inicia o Next.js. O endereço usa o `site.basePath` da configuração.

Para testar uma alteração ainda local da central:

```sh
npm run dev -- --source ../central-links
npm run build -- --source ../central-links
```

Esse parâmetro afeta apenas a execução local. Ele não altera a versão aprovada nem publica o site. A mesma opção funciona com `test`, `typecheck`, `check:config` e `check:site-export`.

```sh
npm test
npm run typecheck
npm run build
npm run check:site-export
npm start
```

`npm start` serve a última exportação de `.site/out/`. `.site/` e `.central-links/` são diretórios gerados e ignorados pelo Git.

## Aprovar atualizações

A rotina `Check central updates` consulta a versão estável diariamente e também pode ser iniciada por `Run workflow`. Havendo uma versão nova, ela testa a candidata com os dados deste profissional antes de propor a atualização.

**A publicação só acontece quando você aceita e faz o merge do PR na `main`.** A rotina nunca aprova ou faz merge por conta própria. Fechar um PR sem merge recusa aquela candidata; ela não será proposta novamente.

Se a política do repositório bloquear PRs criados pelo GitHub Actions, a rotina abre uma solicitação em Issues com a branch pronta e o link para criar o PR manualmente. Depois de aceitar ou recusar, feche a solicitação. Não é necessário conceder novas credenciais para esse fluxo.

O GitHub pode atrasar agendamentos e desativá-los em repositórios públicos sem atividade por 60 dias. Nesse caso, reative `Check central updates` em Actions; a execução manual também fica disponível.

Para voltar a uma versão anterior, altere `central.config.json.revision` para o SHA completo que deseja e publique essa alteração pela `main`. O workflow valida a versão antes do deploy. Não altere o `id` do profissional para manter seus treinos salvos.

Os workflows usam o controlador versionado `@v1` da central. Uma mudança futura no contrato desses workflows poderá exigir atualizar essa referência; atualizações normais do aplicativo são propostas pelo campo `revision`.

## Identidade visual

A página inicial usa azul-marinho, dourado e branco. O Tabata usa a mesma paleta escura com destaque verde da Débora. As duas paletas continuam independentes e editáveis em `site.config.json`: `theme.home` controla a página inicial e `theme.timer` controla o cronômetro, suas telas e as cores do aplicativo instalado. As logos completas em `public/brand/` vieram dos arquivos originais da pasta RA e foram preservadas. O monograma SVG foi preparado a partir do vetor editável já existente em `Fotos/`; os ícones de instalação foram exportados desse vetor nos tamanhos 192 × 192 e 512 × 512, com margem para máscara. Os originais em `Fotos/` e os arquivos de fonte continuam locais e não são publicados.

O perfil usa o monograma porque não há foto de retrato nos materiais fornecidos. O Tabata está habilitado e seus dados ficam neste navegador, separados dos outros profissionais.

## Validação inicial — 18/11/2026

- 67 testes passaram com a configuração do Rodrigo e a versão fixada da central.
- Build de produção, checagem de tipos e validação da exportação passaram, incluindo 22 recursos no ambiente simulado de worker offline.
- Home, rodapé, contatos e Tabata foram conferidos no Chrome, incluindo a simulação de iPhone SE em 375 × 667. O timer indicou recursos preparados para uso offline. Essa revisão não equivale a um teste de áudio em segundo plano em um iPhone físico.
- A exportação foi verificada para não conter a identidade nem os contatos da Débora.
