# Colaboracao entre Agentes

Mantenha sua equipe de suporte sincronizada com indicadores de presenca em tempo real e notas internas fixadas. Sem necessidade de ferramentas externas.

## Deteccao de colisao

Quando varios agentes abrem o mesmo ticket, cada agente ve um indicador de avatar mostrando quem mais esta visualizando. Isso evita respostas duplicadas e esforco desperdicado.

- Pilha de avatares com iniciais dos outros visualizadores
- Tooltip "Tambem visualizando" ao passar o mouse
- Verificacao a cada 30 segundos -- leve, baseado em cache (nenhuma tabela de banco de dados necessaria)

## Indicadores de digitacao

Agentes podem transmitir o estado de digitacao ativa enquanto compoem respostas para que colegas evitem respostas sobrepostas.

- Estado de digitacao em tempo real por ticket
- Complementa a deteccao de colisao para transferencias mais rapidas

## Notas internas fixadas

Notas internas importantes podem ser fixadas no topo da visualizacao de detalhe do ticket. Notas fixadas sao destacadas em um card ambar acima da thread de conversa, para que os agentes nao percam contexto critico.

- Fixar ou desfixar qualquer nota interna com um clique
- Notas fixadas sao exibidas no topo do ticket, sempre visiveis
- Apenas notas internas podem ser fixadas -- respostas publicas nao podem

## Painel de conhecimento

A barra lateral do ticket inclui um painel de conhecimento contextual para que os agentes possam consultar conteudo de ajuda relacionado sem sair da visualizacao do ticket.
