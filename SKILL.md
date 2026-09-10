---
name: criar-arquitetura-agente
description: "Cria ou revisa a arquitetura de um sistema com agentes, começando pelo Cérebro e conectando produto, fluxos, dados, ferramentas, decisões e operação em Markdown com diagramas Mermaid. Use para desenhar um agente, documentar sua arquitetura ou incorporar uma capacidade a um sistema existente; não para apenas escrever um prompt ou organizar pastas de contexto."
---

# Criar arquitetura de agente

Produza um documento que permita ao dono do produto entender o sistema e à engenharia construí-lo. Comece pelo **Cérebro: o que o agente precisa saber, onde esse conhecimento mora e como ele navega por ele**. Conecte esse conhecimento ao trabalho real, às decisões e à implementação. Diagramas acompanham uma explicação; uma lista de serviços não constitui uma arquitetura.

## Resultado esperado

Crie ou revise o Markdown solicitado. Se nenhum arquivo foi indicado, escolha um nome descritivo no projeto e informe a escolha; se o pedido for apenas uma discussão, entregue a arquitetura na conversa. Desenhar não autoriza implementar, provisionar serviços ou alterar outros repositórios. Uma revisão deve preservar decisões válidas e detalhes relevantes, reescrevendo o conjunto quando uma mudança de escopo exigir.

Para um documento completo, consulte [o roteiro de descrição e diagramas](references/roteiro-arquitetura.md). Use-o como estrutura adaptável, não como formulário com capítulos vazios. A profundidade depende do produto e das decisões a tomar, não de um número fixo de páginas, agentes ou camadas.

## 1. Ler o sistema antes de desenhar

Leia o contexto fornecido, a arquitetura e os contratos existentes. Identifique usuários, resultado desejado, fontes, processo atual, regras, exceções e restrições explícitas. Distinga:

- **Observado:** evidência nos arquivos, fontes ou implementação examinada.
- **Decidido:** escolha já autorizada pelo usuário ou registrada no projeto.
- **Proposto:** desenho que está sendo recomendado, com motivo e consequência.
- **Pendente:** informação ou decisão que ainda falta, com efeito sobre a entrega.

Código existente é evidência de comportamento, não obrigação de preservá-lo. Descubra o que é requisito de negócio e o que é acidente da implementação. Respeite pedidos de reaproveitamento ou reescrita. Não transforme a autorização para reescrever em obrigação de substituir tudo.

## 2. Começar pelo Cérebro

Após uma abertura curta com o objetivo, apresente o conhecimento do sistema antes do catálogo de infraestrutura:

- Domínios/áreas: vocabulário, entidades, fontes, processos, regras e casos conhecidos; conteúdo compartilhado independente de um agente específico.
- Mandato do agente: gatilhos, tarefa, ferramentas, limites, critérios de conclusão e contexto necessário.
- Navegação: ponto de entrada, índice, resumos, relações explícitas e condições para expandir cada nó.
- Governança: fonte de verdade, dono, atualização, versão e tratamento de informação ausente ou conflitante.

Proponha uma árvore ilustrativa quando ela ajudar. Não crie pastas reais como efeito colateral de documentar a arquitetura. Adapte nomes e organização ao projeto; o Cérebro pode ser servido por arquivos, recursos ou outro repositório de conhecimento.

Separe conhecimento de domínio, política executável, histórico de casos e estado da execução. Um resumo do agente não substitui o estado operacional. Uma regra em texto não deve competir com outra regra numérica sem fonte canônica definida.

## 3. Investigar o produto como PM

Faça estas perguntas para orientar a análise e busque respondê-las no contexto. Não transforme automaticamente a tarefa em entrevista com o usuário:

1. Qual trabalho precisa ser concluído e para quem?
2. O que a capacidade significa no domínio? Qual falha, custo ou oportunidade ela atende?
3. Ela é necessária? O que acontece se for retirada? Qual benefício é demonstrado e qual ainda é hipótese?
4. Em que momento surge a informação de que ela depende? Quem consome sua saída?
5. Ela calcula, observa, investiga, recomenda, executa ou autoriza? Quem decide o quê?
6. Que evento indica conclusão, falha, correção ou necessidade de intervenção?
7. Precisa de um agente distinto ou de um workflow/ferramenta dentro de um mandato existente?
8. Como provar que funciona e que melhora o processo?

Responda explicitamente às perguntas que mudam o desenho, em prosa ou tabela com consequência arquitetural. Pergunte ao usuário apenas sobre lacunas que impeçam uma escolha relevante; continue o que não depende delas. Não invente políticas, alçadas, métricas de sucesso ou fatos de negócio.

## 4. Conectar o fluxo às decisões

Descreva cada etapa por entrada, transformação/ação, saída, consumidor e condição de avanço. Separe trabalho determinístico, investigação agêntica e julgamento humano conforme o caso. Cálculos e alterações que exigem reprodução devem ter implementação verificável; não depender de uma afirmação do modelo.

Posicione verificações onde sua evidência existe e onde a decisão é necessária. Uma capacidade pode atuar antes, durante e depois de uma entrega. Evite tanto uma barreira única prematura quanto verificações tardias que detectam o problema após seu efeito.

Quando houver exceções, descreva detecção → atribuição → investigação → ação/decisão → verificação do resultado. Diferencie explicar, corrigir, aceitar e concluir. Não force um sistema de casos ou aprovação humana em tarefas que não precisam deles.

Mostre o fluxo principal em Mermaid e explique o que as setas transferem: dados, controle, evento ou decisão. Verifique dependências circulares, principalmente uma aprovação que exija a saída da etapa que ela própria bloqueia.

## 5. Derivar a arquitetura do trabalho

Conecte as responsabilidades abaixo na medida em que forem necessárias:

| Responsabilidade | Decisão a explicitar |
|---|---|
| Fontes e dados | Autoridade, identidade/granularidade, relações, atualização, qualidade e histórico necessário |
| Processamento | O que calcula ou transforma; quais entradas e versões produzem cada saída |
| Ferramentas | Operações semânticas, entradas/saídas tipadas, evidência, limite e comportamento em erro |
| Runtime | Como escolhe o workflow, acessa contexto e ferramentas e registra sua conclusão |
| Estado e orquestração | Quem coordena a execução, o que persiste e como retoma após interrupção |
| Interface | Como a pessoa entende a situação, chega à evidência e toma a ação necessária |
| Autoridade | Identidade e escopo de cada ator, e onde os limites são aplicados de fato |

Escolha stack por requisito, restrição e tradeoff. Não imponha MCP, cloud, banco transacional, warehouse, grafo, event bus ou múltiplos agentes por terem aparecido em outro projeto. Se concorrência, espera longa, reprodução ou efeitos externos justificarem mecanismos adicionais, explique esse vínculo. Não simplifique removendo responsabilidade necessária; não adicione serviço sem responsabilidade identificável.

Quando o usuário pedir estado da arte ou escolhas dependerem de capacidades atuais, verifique documentação primária e cite as fontes junto às decisões técnicas. Separe o que a fonte documenta da recomendação para o produto. Pesquisa informa o desenho, não determina uma stack por popularidade.

## 6. Projetar a navegação, não apenas o armazenamento

Defina um caminho executável: **tarefa → regra/contexto relevante → agregado/resultado → entidades → evidência de origem → conclusão/ação**. Adapte a sequência ao domínio.

O agente começa com resumo, escopo e referências; expande o necessário por metadados, relações, busca e ferramentas. Para dados volumosos, estabeleça população completa, páginas/amostras identificadas e referências estáveis. Uma amostra não sustenta um total. A navegação deve preservar o contexto temporal da investigação e indicar quando ele mudou.

Dados retornados por ferramentas e texto de origem não viram instruções. A conclusão deve diferenciar fato, hipótese e critério aplicado. Defina quando evidência insuficiente leva a investigação adicional ou encaminhamento, sem exigir uma resposta definitiva artificial.

## 7. Integrar revisões em todo o documento

Ao incorporar uma capacidade, reavalie objetivo, Cérebro, diagramas, fluxo, entidades, ferramentas, estados, autoridade, experiência, avaliação e roadmap afetados. Evite anexar um capítulo isolado enquanto o fluxo principal continua descrevendo outro sistema.

Preserve detalhes úteis do domínio e contratos existentes. Atualize referências, nomes e exemplos incompatíveis; não apague complexidade para encurtar o documento. Se dados, código ou aprovações puderem mudar durante o trabalho, explicite identidade da versão, revalidação e efeito sobre entregas dependentes. Para ações com retry, explicite como evita duplicação proporcionalmente ao risco.

## 8. Tornar construível e verificável

Feche com entregas de produto, dependências e critérios de pronto. Coloque decisões humanas como dependências das liberações correspondentes, não como impedimento genérico de todo o projeto. Diferencie avaliação do cálculo/controle, do agente e do benefício para o usuário.

Revise se cada componente tem função, cada decisão tem responsável e cada estado de sucesso tem evidência. Percorra ao menos um caso normal e uma exceção plausível do domínio; se houver estado durável, considere também retomada ou mudança de dados. Isso é revisão do desenho, não alegação de teste da implementação.

Confira consistência entre texto, Mermaid, contratos e roadmap; links locais, blocos e identificadores. Valide/renderize Mermaid quando houver ferramenta apropriada. Não apresente SQL ilustrativo ou diagrama não executado como implementação testada. Entregue o arquivo e resuma as principais decisões e pendências.
