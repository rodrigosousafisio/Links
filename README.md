# Rodrigo Andrade — Links

Site de Rodrigo Andrade, fisioterapeuta em São Luís, MA, com foco em reabilitação de joelho. Este repositório guarda a configuração e os arquivos da marca. O aplicativo, seus testes e o build ficam na central privada [WiltonV/central-links](https://github.com/WiltonV/central-links).

- `site.config.json`: perfil, links, cores, SEO, endereço e recursos.
- `public/`: foto, logos e demais arquivos exclusivos deste profissional.
- `central.config.json`: SHA completo da versão aprovada da central.

GitHub Pages: `https://rodrigosousafisio.github.io/links/`. O repositório deve se chamar `links` e o `site.basePath` deve ser `/links`, ambos em minúsculas.

A branch `site` contém somente os arquivos gerados para publicação. A central é acessível aos mantenedores autorizados.

## Desenvolvimento

Requer acesso autorizado à central privada, Node.js 20.19 ou superior, Git e Corepack/Yarn disponíveis (`corepack enable`). Não é necessário instalar dependências na raiz deste repositório. A autenticação HTTPS do Git deve permitir ler a central; também é possível usar um checkout local com `--source`.

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

A central consulta a versão estável e as configurações dos profissionais em um agendamento de 15 minutos, sujeito a atrasos do GitHub. Havendo uma versão nova, testa a candidata em ambiente privado antes de abrir o PR neste repositório.

**A troca da versão da central só acontece quando você aceita e faz o merge do PR na `main`.** A rotina nunca aprova ou faz merge por conta própria. Fechar um PR sem merge recusa aquela candidata; ela não será proposta novamente. Alterações de perfil, links ou imagens na `main` usam a revisão já aprovada da central.

Se o GitHub bloquear a abertura automática do PR, a central pode criar uma solicitação em Issues com a branch pronta e o link para criar o PR manualmente. Depois de aceitar ou recusar, feche a solicitação.

Para antecipar uma publicação, um mantenedor executa Actions → Distribute private central → Run workflow na central, selecionando este profissional e `sync`. O workflow público `Deploy generated site` recebe a notificação e publica os arquivos da branch `site`, sem acessar o código privado. Sua execução manual republica a última exportação disponível; ela não monta uma configuração recém-alterada.

Para voltar a uma versão anterior, altere `central.config.json.revision` para o SHA completo desejado e faça merge dessa alteração na `main`. A central valida essa revisão antes de distribuir os arquivos. Não altere o `id`, a origem ou o caminho do site para preservar os treinos locais e os endereços existentes.

Não faça alterações manuais na branch `site`: ela é gerada pela central. Os HTMLs, CSS, JavaScript compilado e assets são públicos; fontes originais, testes, ferramentas e credenciais de distribuição ficam na central privada.

## Identidade visual

A página inicial usa azul-marinho, dourado e branco. O Tabata usa a mesma paleta escura com destaque verde da Débora. As duas paletas continuam independentes e editáveis em `site.config.json`: `theme.home` controla a página inicial e `theme.timer` controla o cronômetro, suas telas e as cores do aplicativo instalado. As logos completas em `public/brand/` vieram dos arquivos originais da pasta RA e foram preservadas. O monograma SVG foi preparado a partir do vetor editável já existente em `Fotos/`; os ícones de instalação foram exportados desse vetor nos tamanhos 192 × 192 e 512 × 512, com margem para máscara. Os originais em `Fotos/` e os arquivos de fonte continuam locais e não são publicados.

O perfil usa o monograma porque não há foto de retrato nos materiais fornecidos. O Tabata está habilitado e seus dados ficam neste navegador, separados dos outros profissionais.

## Validação inicial — 18/11/2026

- 67 testes passaram com a configuração do Rodrigo e a versão fixada da central.
- Build de produção, checagem de tipos e validação da exportação passaram, incluindo 22 recursos no ambiente simulado de worker offline.
- Home, rodapé, contatos e Tabata foram conferidos no Chrome, incluindo a simulação de iPhone SE em 375 × 667. O timer indicou recursos preparados para uso offline. Essa revisão não equivale a um teste de áudio em segundo plano em um iPhone físico.
- A exportação foi verificada para não conter a identidade nem os contatos da Débora.
