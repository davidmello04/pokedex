# Pokédex

Aplicação web responsiva que apresenta os 151 Pokémon da primeira geração com dados consumidos da [PokéAPI](https://pokeapi.co/). O projeto permite pesquisar Pokémon, consultar tipos, habilidades e estatísticas e alternar a visualização do sprite.

[![Vue.js](https://img.shields.io/badge/Vue.js-3-4FC08D?logo=vuedotjs&logoColor=white)](https://vuejs.org/)
[![Vite](https://img.shields.io/badge/Vite-4-646CFF?logo=vite&logoColor=white)](https://vite.dev/)
[![Bulma](https://img.shields.io/badge/Bulma-0.9-00D1B2?logo=bulma&logoColor=white)](https://bulma.io/)

## Demonstração

**[Acessar a aplicação](https://glittery-narwhal-098581.netlify.app/)**

> Deploy verificado em 17 de setembro de 2026.

## Funcionalidades

- listagem dos 151 Pokémon da primeira geração;
- pesquisa por nome;
- exibição de tipo, habilidades e estatísticas;
- alternância entre sprites frontal e traseiro;
- interface responsiva para diferentes tamanhos de tela;
- consumo de dados externos com Axios.

## Tecnologias

- Vue.js 3
- JavaScript
- Vite
- Axios
- Bulma
- PokéAPI

## Capturas de tela

### Listagem de Pokémon

![Listagem de Pokémon](https://github.com/davidmello04/dragonballz-memory-game/assets/102268159/61ddc2b4-15a1-4cea-9686-9c725a6a5527)

### Pesquisa

![Pesquisa de Pokémon](https://github.com/davidmello04/dragonballz-memory-game/assets/102268159/eb23f8b0-a7e6-4304-8ce6-109cf044095a)

### Detalhes e estatísticas

![Detalhes e estatísticas de um Pokémon](https://github.com/davidmello04/dragonballz-memory-game/assets/102268159/67a7fd27-6db1-4fa5-929e-6b36eeed4671)

## Como executar localmente

### Pré-requisitos

- Node.js 18 ou superior
- npm

```bash
git clone https://github.com/davidmello04/pokedex.git
cd pokedex
npm install
npm run dev
```

A aplicação ficará disponível no endereço exibido pelo Vite, normalmente `http://localhost:5173`.

## Scripts

```bash
npm run dev      # inicia o ambiente de desenvolvimento
npm run build    # gera a versão de produção
npm run preview  # executa a versão de produção localmente
npm run lint     # verifica e corrige problemas de lint
npm run format   # formata os arquivos da pasta src
```

## Fonte dos dados

Os dados e sprites dos Pokémon são fornecidos pela [PokéAPI](https://pokeapi.co/).

## Autor

Desenvolvido por [David Melo](https://github.com/davidmello04).

[LinkedIn](https://www.linkedin.com/in/david-melo-/)
