# Código em Linguagem M
Este repositório contém um exemplo genérico de código em Linguagem M usado no Power Query.  
**Destaques**:
- Estrutura de transformação de dados.
- Uso de tipos de dados genéricos.  

**Como Usar**:
Substitua os valores genéricos pelas informações do seu projeto.

    // SUBSTITUINDO VALOR
    #"VALOR SUBSTITUIDO" = Table.ReplaceValue(#"TIPO ALTERADO", "?", "45", Replacer.ReplaceText, {"COLUNA2"}),

    // AJUSTANDO O TIPO DA VARIÁVEL
    #"TIPO AJUSTADO" = Table.TransformColumnTypes(#"VALOR SUBSTITUIDO", {{"COLUNA2", Int64.Type}}),

    // REMOVENDO COLUNA
    #"COLUNA REMOVIDA" = Table.RemoveColumns(#"TIPO AJUSTADO", {"COLUNA5"}),

    // ADICIONANDO COLUNA
    #"COLUNA ADICIONADA" = Table.AddColumn(#"COLUNA REMOVIDA", "VALOR_FINAL", each [COLUNA9] - [COLUNA8]),

    // DIVIDINDO COLUNA
    #"DIVIDIR COLUNA PELA POSIÇÃO" = Table.SplitColumn(#"COLUNA ADICIONADA", "COLUNA1", Splitter.SplitTextByPositions({0, 4}, false), {"PARTE1", "PARTE2"}),
    #"COLUNA DIVIDIDA" = Table.TransformColumnTypes(#"DIVIDIR COLUNA PELA POSIÇÃO", {{"PARTE1", type text}, {"PARTE2", Int64.Type}}),

    // AJUSTANDO NOME DE COLUNA
    #"COLUNAS RENOMEADAS" = Table.RenameColumns(#"COLUNA DIVIDIDA", {{"PARTE1", "CODIGO"}, {"PARTE2", "ID"}}),

    // COLUNA CONDICIONAL
    #"COLUNA CONDICIONAL ADICIONADA" = Table.AddColumn(#"COLUNAS RENOMEADAS", "DESCONTO_ESPECIAL", each if [COLUNA10] = "BRONZE" then 5 else if [COLUNA10] = "PRATA" then 10 else if [COLUNA10] = "OURO" then 15 else if [COLUNA10] = "DIAMANTE" then 20 else 0),

    // AJUSTANDO A ESCALA DA COLUNA COM TRANSFORMAÇÃO LOGARÍTMICA
    #"LOGARITMO DE BASE 10 CALCULADO" = Table.TransformColumns(#"COLUNA CONDICIONAL ADICIONADA", {{"COLUNA7", Number.Log10, type number}})
in
    #"LOGARITMO DE BASE 10 CALCULADO"
