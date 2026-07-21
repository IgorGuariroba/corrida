# Plano de jogo — Corrida do Caos

## Visão

**Corrida do Caos** é um jogo web de corrida com obstáculos, rápido, colorido e rejogável. O jogador controla um competidor em uma pista vertical de três faixas, desvia de perigos, supera obstáculos, coleta moedas e power-ups e tenta chegar à linha de chegada com a maior pontuação possível.

A experiência deve funcionar em desktop e celular, sem login e sem backend. Uma partida dura aproximadamente 2–4 minutos. O jogo deve ser fácil de aprender, mas oferecer decisões de rota, evolução permanente e objetivos que incentivem novas partidas.

## Público e pilares

- Público casual, a partir de 8 anos.
- Controles simples e resposta imediata.
- Humor visual e situações caóticas, sem violência realista.
- Escolhas frequentes: segurança, recompensa ou velocidade.
- Progressão perceptível sem compras reais ou mecânicas predatórias.
- Regras determinísticas e testáveis, separadas da renderização.

## Plataforma e acessibilidade

- Aplicação web responsiva e instalável futuramente como PWA.
- Teclado: setas ou WASD; `Espaço` para pular; `P`/`Esc` para pausar.
- Toque: botões grandes para esquerda, direita e pulo; gestos são opcionais.
- Suporte a redução de movimento, alto contraste e volume independente para música e efeitos.
- Não depender apenas de cor para comunicar perigo ou raridade.
- Canvas escalável com HUD e menus em HTML semântico.

## Loop principal

1. Na tela inicial, o jogador escolhe corredor, dificuldade e um entre três equipamentos desbloqueados.
2. A contagem regressiva inicia a prova.
3. Durante a corrida, o cenário avança automaticamente e o jogador troca de faixa e pula.
4. O jogador evita obstáculos, coleta moedas e ativa power-ups.
5. Portões de rota oferecem uma escolha entre risco e recompensa.
6. A dificuldade aumenta por trechos até a chegada ou até o fim das vidas.
7. O resultado concede estrelas, moedas e progresso de missões.
8. O jogador compra upgrades, troca cosméticos e tenta novamente.

## Corrida e controles

### Estado do corredor

- Três faixas horizontais.
- Troca de faixa com pequeno tempo de transição e fila de no máximo um comando.
- Pulo com duração fixa e janela clara de invulnerabilidade contra obstáculos baixos.
- Três corações no modo normal; colisões removem um coração e concedem breve invulnerabilidade.
- A corrida termina ao perder todos os corações ou cruzar a chegada.
- Pausar congela relógio, física, spawns e combos.

### Obstáculos

- **Cone:** deve ser evitado trocando de faixa.
- **Poça de lama:** reduz temporariamente a velocidade e encerra combo.
- **Barreira baixa:** deve ser pulada.
- **Barreira alta:** força troca de faixa.
- **Caixote móvel:** cruza faixas com trajetória sinalizada.
- **Martelo inflável:** obstáculo temporizado, indicado por sombra/aviso.

A geração deve respeitar regras de segurança: sempre existir ao menos uma solução possível, nenhum dano inevitável após uma troca de trecho e sinalização mínima antes de obstáculos móveis.

### Trechos e rotas

Uma prova é composta por trechos com temas e padrões crescentes. Em pontos definidos surgem portões:

- **Rota segura:** menos obstáculos, multiplicador normal.
- **Rota veloz:** mais obstáculos móveis e bônus de tempo.
- **Rota do tesouro:** mais moedas, porém com largura útil reduzida.

A escolha deve alterar os próximos padrões, recompensas e parte do cenário, não apenas um texto no HUD.

## Coletáveis e power-ups

- **Moedas:** usadas para upgrades e cosméticos.
- **Estrela:** aumenta bastante a pontuação e o medidor de combo.
- **Escudo:** absorve uma colisão por duração limitada.
- **Ímã:** atrai moedas próximas.
- **Turbo:** aumenta velocidade e pontuação; quebra obstáculos leves, mas exige reação mais rápida.
- **Relógio:** desacelera obstáculos, sem alterar a resposta dos controles.

Somente um power-up temporal principal fica ativo; coletar outro substitui o anterior. Escudo é uma carga separada. Durações e efeitos devem aparecer no HUD.

## Pontuação e combo

Pontuação base vem de distância, chegada, moedas, estrelas e obstáculos superados. Passar perto de um obstáculo ou superar barreira sem colisão aumenta o combo.

- Multiplicador começa em `x1` e cresce até `x5`.
- Colisão ou lama zera o combo.
- Dificuldades maiores aplicam bônus de pontuação.
- Resultado detalha distância, tempo, coletáveis, maior combo e bônus de chegada.
- A fórmula deve ficar no núcleo determinístico e ser exibida de forma compreensível.

## Dificuldade

- **Passeio:** velocidade menor, cinco corações, mais avisos e sem perda total de moedas da prova.
- **Normal:** experiência padrão com três corações.
- **Caos:** velocidade e densidade maiores, dois corações e melhor multiplicador.

A curva dentro da prova aumenta por distância, com limite explícito. Dificuldade nunca deve criar padrões impossíveis.

## Progressão e upgrades

O progresso é salvo localmente com versão de schema e recuperação segura para dados inválidos.

### Upgrades funcionais

Cada upgrade possui três níveis, custo crescente e efeito com limite definido:

- **Tênis de mola:** aumenta a janela útil do pulo.
- **Colete reforçado:** inicia a prova com uma carga de escudo no nível máximo.
- **Ímã de bolso:** aumenta alcance e duração do ímã.
- **Cofrinho:** concede bônus de moedas ao concluir a corrida.
- **Motor turbo:** aumenta duração do turbo, sem elevar sua velocidade máxima.

Antes da corrida, o jogador equipa apenas um upgrade funcional, evitando acúmulo excessivo de vantagem.

### Cosméticos

- Corredores e trilhas visuais desbloqueáveis com moedas.
- Cosméticos não alteram regras ou hitboxes.
- Itens têm nome, prévia, preço e estado: bloqueado, disponível, comprado ou equipado.

## Gamificação

### Estrelas por prova

Cada corrida concede até três estrelas:

1. chegar ao fim;
2. atingir uma meta de pontuação;
3. cumprir um desafio da prova, como terminar sem perder coração.

### Missões

Três missões locais são oferecidas e renovadas deterministicamente por data:

- coletar uma quantidade de moedas;
- pular obstáculos;
- alcançar combo específico;
- concluir uma rota;
- usar determinado power-up.

Cada missão tem progresso visível, recompensa única e estado resgatado persistente. Não usar contadores regressivos manipulativos nem exigir conexão diária.

### Conquistas

Marcos permanentes, como primeira vitória, combo `x5`, corrida sem dano e compra do primeiro upgrade. Desbloqueios geram um toast discreto e ficam numa galeria.

### Recordes

- Melhor pontuação por dificuldade.
- Melhor tempo de conclusão.
- Maior combo.
- Histórico das cinco últimas corridas.

Sem ranking online no MVP.

## Telas e experiência

1. **Início:** jogar, upgrades, cosméticos, missões, conquistas e configurações.
2. **Preparação:** dificuldade, corredor e equipamento; resumo dos modificadores.
3. **Corrida:** pista, corredor, obstáculos e HUD com vidas, pontuação, combo, moedas, distância e power-up.
4. **Pausa:** continuar, reiniciar, configurações e sair.
5. **Resultado:** vitória/derrota, estatísticas, estrelas, recompensas, recordes e ações de jogar novamente ou voltar.
6. **Loja/garagem:** upgrades e cosméticos com confirmação clara de compra/equipamento.

O primeiro acesso apresenta tutorial curto em cartões e dicas contextuais. O tutorial pode ser reaberto e não bloqueia jogadores recorrentes.

## Direção visual e sonora

- Estética de festival esportivo cartunesco, com formas arredondadas e cores vibrantes.
- Pista legível, contraste forte entre corredor, coletáveis e perigos.
- Temas de trechos: parque, feira maluca e cais ensolarado.
- Animações curtas para troca de faixa, pulo, colisão, coleta e chegada.
- Feedback por partículas, squash-and-stretch leve, áudio e texto; respeitar redução de movimento.
- Sons sintéticos curtos e música em loop opcional; o jogo deve funcionar completamente mudo.

## Arquitetura técnica

- TypeScript estrito, Vite e HTML/CSS.
- Renderização da corrida em Canvas 2D; menus e HUD em DOM.
- Núcleo funcional sem DOM: estado, comandos, colisões, spawns, pontuação, progressão e RNG com seed.
- Loop de passo fixo, interpolação apenas visual e relógio injetável.
- Adaptadores separados para teclado/toque, áudio e `localStorage`.
- Testes unitários para regras e progressão; testes de integração para fluxo de telas; E2E para uma corrida completa.
- Scripts obrigatórios: `npm run typecheck`, `npm test` e `npm run build`.

## Escopo do MVP

Inclui uma prova completa, três dificuldades, seis obstáculos, três rotas, cinco power-ups, moedas, combo, pontuação, três upgrades funcionais, seis cosméticos, missões, conquistas, recordes, tutorial, configurações e persistência local.

Fora do MVP: multiplayer, contas, backend, ranking online, pagamentos, editor de pistas e conteúdo gerado por usuários.

## Critérios globais de pronto

- É possível iniciar e terminar uma corrida usando teclado e controles de toque.
- Nenhum padrão gerado exige colisão; RNG pode ser reproduzido por seed.
- Menus e HUD permanecem utilizáveis em 360×640 e desktop.
- Progresso persiste após recarregar e dados corrompidos não quebram o jogo.
- Todas as opções de acessibilidade alteram a experiência conforme descrito.
- Não há erros no console durante o fluxo principal.
- Typecheck, testes e build passam.
