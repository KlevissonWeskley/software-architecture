
# Arquitetura Leilão

Plataforma de leilão online construída como projeto de estudo de arquitetura de software, evoluindo por vários estilos arquiteturais. Cada decisão é registrada em ADRs e cada fase é marcada com uma tag git.

Baseado nos conceitos do livro *Fundamentos da Arquitetura de Software: Uma abordagem de engenharia* (Mark Richards e Neal Ford).

## Escopo

Vendedores cadastram itens com preço inicial e horário de término. Compradores dão lances e acompanham o lance atual em tempo real. Ao fim do tempo, o maior lance vence, o pagamento é processado e o item é liberado. Quando um comprador é superado, ele recebe uma notificação.

### Funcionalidades

- Cadastrar item e abrir leilão
- Dar lance e ver o lance atual em tempo real
- Encerrar leilão e definir o vencedor
- Pagamento simulado (serviço falso que falha de vez em quando)
- Notificar comprador superado

### Fora do escopo

- Login sofisticado, frete, disputas e painel administrativo
- Upload de várias imagens por item
- Multi-tenancy (possível extensão futura)

## Por que um leilão

O domínio tem tensões que exigem decisões arquiteturais reais:

| Característica                              | Problema arquitetural             |
| -------------------------------------------- | --------------------------------- |
| Pico de lances no último minuto             | Elasticidade e desempenho         |
| Lances quase simultâneos                    | Consistência                     |
| Lance aceito precisa avisar outros usuários | Eventos e notificações          |
| Vencedor, pagamento e liberação do item    | Transações distribuídas (saga) |
| Regras diferentes por tipo de leilão        | Extensibilidade (plug-ins)        |

## Fases

| Fase | Tag                     | Foco                                                       |
| ---- | ----------------------- | ---------------------------------------------------------- |
| 1    | `fase-1-fundamentos`  | Características arquiteturais, métricas e ADR-001        |
| 2    | `fase-2-monolito`     | Monolito modular em camadas com testes de arquitetura      |
| 3    | `fase-3-servicos`     | Extração do módulo de Lances como serviço próprio     |
| 4    | `fase-4-eventos`      | Arquitetura orientada a eventos e notificações           |
| 5    | `fase-5-picos`        | Cache e tratamento de picos de carga                       |
| 6    | `fase-6-sagas`        | Fluxo de pagamento com saga (coreografia e orquestração) |
| 7    | `fase-7-documentacao` | ADR final, diagramas C4 e risk storming                    |

## Estrutura do repositório

```
docs/adr         Registros de decisão de arquitetura (um por decisão)
docs/notes       Anotações por capítulo do livro
docs/diagrams    Diagramas C4 de cada fase
src              Código-fonte
```

## Como acompanhar

1. Leia os ADRs em ordem numérica para entender cada decisão e seus trade-offs.
2. Use as tags git para ver o sistema em cada fase.
3. As anotações em `docs/notes` mostram como cada conceito foi aplicado.

## Status

Fase 1 em andamento: leitura dos fundamentos e definição das características arquiteturais.
