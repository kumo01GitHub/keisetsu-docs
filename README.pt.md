# keisetsu Documentação

Este é o hub de documentação para a intenção de design e política operacional geral do keisetsu.

`keisetsu-docs` é um local central para gerenciar especificações, regras operacionais e procedimentos de atualização entre todos os repositórios do keisetsu (publisher / database / mobile).

- Esclarece as responsabilidades de cada repositório
- Documenta os fluxos de distribuição e validação independentemente da implementação
- Mantém critérios comuns para mudanças de especificação

## Conceito

keisetsu é um aplicativo de flashcards de código aberto que torna público o armazenamento de dados de aprendizagem e as rotas de distribuição, permitindo que os usuários possuam e usem seus próprios materiais de aprendizagem.

- Objetivo
  - Criar um ambiente onde qualquer pessoa possa aprender apenas com um smartphone
- Motivação
  - Resolver problemas existentes como dados privados, dependência online e rotas de atualização pouco claras
- Vantagens
  - Todas as especificações, dados e fluxos de distribuição são públicos e transparentes
  - OSS: qualquer pessoa pode atualizar e usar os dados gratuitamente
- Abordagem
  - Separar criação (publisher), distribuição (database) e uso (mobile) para facilitar atualizações e reutilização
  - Usar um esquema público para estrutura de dados, um catálogo público para rotas de distribuição e um app offline para aprendizagem

## Guia do usuário

### Como usar o app móvel keisetsu

1. Instale o app Expo Go no seu smartphone.
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. Escaneie o código QR para iniciar o app keisetsu.

![Expo QR](assets/eas-update.svg)

Você pode começar a usar o app keisetsu imediatamente.

### Como usar o editor web de baralhos keisetsu

1. Acesse a [página pública do keisetsu-publisher](https://keisetsu-publisher.vercel.app)
2. Crie um novo baralho ou importe um CSV / kdb existente
3. Edite as cartas e as informações do baralho (ID, título, idioma, etc.)
4. Baixe o arquivo ZIP
5. Extraia o ZIP baixado e coloque os arquivos gerados em keisetsu-database, depois [envie uma solicitação de adição/edição](https://github.com/kumo01GitHub/keisetsu-database/issues)

### Idiomas suportados

- Inglês (`en`)
- Japonês (`ja`)
- Espanhol (`es`)
- Português (`pt`)
- Chinês (`zh`)
- Coreano (`ko`)

## Guia do desenvolvedor

Para informações detalhadas sobre a estrutura do repositório, regras operacionais e informações técnicas, veja [DEVELOPER.md](./DEVELOPER.md).
