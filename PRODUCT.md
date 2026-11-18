# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

- **Primary**: Comunidade técnica, contribuidores open-source e pares de engenharia (desenvolvedores mobile/Android, sistemas Linux/Rust, computação teórica e colegas de Ciência da Computação).
- **Situation**: Visitam o portfólio a partir do GitHub (`vimi-tt`), de links em READMEs (como Overview e Verso) ou de artigos técnicos do blog para avaliar a qualidade do código, o critério de design e a profundidade técnica dos projetos.

## Product Purpose

Apresentar o trabalho de engenharia de software e design de produto de José Vitor Diniz Miranda (`vimi-tt`), destacando projetos autorais reais com foco em software nativo Android (Kotlin/Compose), ferramentas de sistemas em Rust, teoria da computação em Haskell e aplicações web acadêmicas, além de notas técnicas no `/blog`.

## Positioning

Um portfólio de engenheiro que trata software como ofício completo — unindo rigor técnico (Android 60/120 Hz, chunked I/O, Rust memory-safe, Haskell funcional) com cuidado explícito de interface e experiência do usuário, sem depender de templates genéricos nem de clichês de terminal/hacker.

## Operating Context

- Site estático gerado em Astro 7 + Tailwind CSS v4, hospedado no GitHub Pages (`https://vimi-tt.github.io/`).
- Dados de repositórios públicos podem ser consultados da API do GitHub no build com fallbacks confiáveis.
- Sessão atual: remodelagem local para validação e testes locais, sem commits automáticos.

## Capabilities and Constraints

- **Stack existente**: Astro 7, Tailwind CSS v4, React, GSAP, Three.js (disponível se necessário), TypeScript.
- **Rotas**: `/` (página principal), `/blog` e `/blog/[...slug]` (coleção de artigos em `src/content/blog/`).
- **Curadoria confirmada**: Overview, Verso, Flicker, Automato-Playground e Guia de PPC - UFCG (sem Null:Gemini).
- **Idioma e tom**: Português (`pt-BR`), direto, técnico e profissional, reduzindo jargões artificiais de terminal (`SOCKET_ESTABLISHED`, `IT_WORKS_ON_MY_MACHINE`, etc.).
- **Restrição explícita**: Não inventar métricas, estrelas, downloads, usuários ou depoimentos; usar apenas dados reais dos repositórios e do perfil.

## Brand Commitments

- **Identidade**: José Vitor Diniz Miranda (`vimi` / `@vimi-tt`), graduando em Ciência da Computação pela UFCG (Campus Sede, Campina Grande - PB).
- **Contato confirmado**: `vitormirandacc@outlook.com` e `https://github.com/vimi-tt`.
- **Avatar**: `https://github.com/vimi-tt.png`.

## Evidence on Hand

- Repositório `vimi-tt/Overview`: Launcher Android moderno inspirado no GNOME 51 / libadwaita, Kotlin + Jetpack Compose, Android 12+ (API 31–35), GPL-3.0, grade 3x3–6x6, 6 estilos de relógio, gestos 60/120 Hz.
- Repositório `vimi-tt/verso`: Player de música Android em Kotlin + Compose (API 29+), streaming YouTube Music, downloads paralelos em chunks (`Range` HTTP), letras sincronizadas palavra por palavra, Last.fm scrobbling e Recap compartilhável.
- Repositório `vimi-tt/Flicker`: Criador de mídia USB bootável para Linux em Rust.
- Repositório `vimi-tt/Automato-Playground`: Simulador interativo de Autômatos Finitos (DFA/NFA) em Haskell.
- Projeto web externo: Guia de PPC - UFCG (`https://guiappc.vercel.app/`).
- Blog existente em `src/content/blog/SO.md`.

## Product Principles

1. **Software real na frente**: Projetos recentes (Overview e Verso) e sua arquitetura/experiência conduzem a primeira impressão.
2. **Clareza técnica sem teatro**: Tom profissional em `pt-BR`, substituindo enfeites de terminal por informações precisas de engenharia.
3. **Linguagem própria e memorável**: Superfície autoral com personalidade visual marcante, evitando o visual genérico de portfólio escuro com neon.
4. **Honestidade factual**: Nenhuma métrica, citação ou capacidade inventada; links e dados refletem exatamente o que existe no GitHub e no repositório local.
