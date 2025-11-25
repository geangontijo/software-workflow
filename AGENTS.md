# AGENTS.md

Este arquivo contém instruções para o Code Agent sobre como alterar o arquivo de fluxograma `diagrams/Diagrama sem nome.drawio`.

## Contexto
O arquivo `diagrams/Diagrama sem nome.drawio` é um fluxograma de decisão sobre o processo de desenvolvimento de software. Ele serve para responder dúvidas como "Como fazer um pré-review?" ou "O que fazer ao identificar um problema de requisitos?".

## Estrutura do Arquivo
O arquivo é um XML compatível com o draw.io (`mxfile`). A estrutura básica envolve `<mxGraphModel>`, `<root>`, e múltiplos `<mxCell>`.

### Tipos de Nós

1.  **Pergunta (Decisão)**
    *   Representada por um losango (`rhombus`).
    *   Deve conter uma pergunta clara que leve a uma decisão (Sim/Não ou outras opções).
    *   **Sintaxe XML**:
        ```xml
        <mxCell id="UNIQUE_ID" value="Sua Pergunta Aqui?" style="rhombus;whiteSpace=wrap;html=1;" vertex="1" parent="1">
          <mxGeometry x="COORD_X" y="COORD_Y" width="130" height="130" as="geometry" />
        </mxCell>
        ```

2.  **Afirmação (Processo/Ação)**
    *   Representada por um retângulo (`rounded=0`).
    *   Deve conter uma instrução, ação ou conclusão.
    *   **Sintaxe XML**:
        ```xml
        <mxCell id="UNIQUE_ID" value="Sua Instrução ou Ação." style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
          <mxGeometry x="COORD_X" y="COORD_Y" width="120" height="60" as="geometry" />
        </mxCell>
        ```

3.  **Resposta (Conexão/Aresta)**
    *   Representada por uma linha que conecta dois nós.
    *   Geralmente possui um rótulo (ex: "Sim", "Não", "Júnior", "Sênior").
    *   **Sintaxe XML**:
        ```xml
        <mxCell id="UNIQUE_ID" value="Sim" style="edgeStyle=orthogonalEdgeStyle;rounded=0;html=1;" edge="1" parent="1" source="SOURCE_ID" target="TARGET_ID">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        ```

## Regras de Edição

1.  **IDs Únicos**: Cada `mxCell` deve ter um `id` único. Você pode gerar strings aleatórias ou usar um padrão sequencial não conflitante.
2.  **Geometria**:
    *   Certifique-se de definir `x`, `y`, `width` e `height` em `mxGeometry` para nós (`vertex="1"`).
    *   Para arestas (`edge="1"`), a geometria é relativa, mas certifique-se de definir `source` e `target` com os IDs corretos dos nós conectados.
3.  **Parent**: Mantenha `parent="1"` para elementos que fazem parte do fluxo principal (assumindo que o layer principal tem id="1").
4.  **Estilo**: Mantenha a consistência visual usando os estilos definidos acima (`rhombus` para perguntas, `rounded=0` para ações).

## Fluxo de Trabalho para Alterações

1.  **Identificar Ponto de Inserção**: Encontre o nó existente onde o novo fluxo deve começar ou se conectar.
2.  **Criar Novos Nós**: Adicione os XMLs para as novas perguntas ou ações.
3.  **Conectar**: Crie as arestas (`edge`) ligando o nó anterior ao novo, e do novo para os próximos passos.
4.  **Verificar IDs**: Garanta que não há duplicidade de IDs.

## Exemplo de Inserção

Se você precisa adicionar uma verificação "O código foi testado?" após uma ação "Finalizar tarefa":

1.  Localize o ID da ação "Finalizar tarefa".
2.  Crie o nó losango "O código foi testado?".
3.  Altere a aresta que saía de "Finalizar tarefa" para apontar para o novo losango (ou crie uma nova).
4.  Crie as arestas de saída do losango para "Sim" e "Não".
