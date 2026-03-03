# Tickets

Tickets sao o nucleo do Escalated. Cada ticket e uma maquina de estados de longa duracao com historico completo de conversas, niveis de prioridade, rastreamento de atribuicao e monitoramento de SLA.

> **Nota:** Cada ticket recebe uma referencia unica (ex.: `ESC-00001`) e suporta status personalizados, niveis de prioridade, atribuicao de departamento, tags, rastreamento de SLA e conversas ricas com anexos de arquivos. Todos os dados ficam no seu banco de dados.

## Fluxos avancados de tickets

- Fluxo de mesclagem de tickets para combinar duplicatas preservando o historico
- Tickets vinculados para fluxos de trabalho de incidente/problema relacionados
- Conversas paralelas para coordenacao interna/externa em paralelo
- Suporte a light-agent para funcoes operacionais restritas
- Formularios de campos personalizados com regras condicionais baseadas no contexto do ticket
