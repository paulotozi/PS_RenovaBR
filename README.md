# Análise de Banco de Dados

## Objetivo

O objetivo deste repósitório é analisar os padrões de votação no estado de São Paulo e seus municípios, utilizando as ferramentas SQL (PostgreSQL) e Python.

## Criação dos Databases

Para utilizarmos os arquivos .csv em PostgreSQL, temos que criar as Tables no ambiente Pgadmin 4 para ambos os arquivos; No mesmo ambiente utilizamos a query CREATE para ambas as Databases, com a coluna ANO_ELEICAO sendo a chave primária. No arquivo SP_turno_1 por não haver documentação das colunas, foi utilizado o seguinte comando no Microsoft PowerShell:  "get-content C:\Users\****\Documents\Desafio_Tec\resultados\SP_turno_1.csv | select -First 1", retornando assim o header do .csv

## Cópia dos arquivos

Para copiar o conteúdo de ambos arquivos .csv, utilizamos a query COPY para ambas as Databases, nota-se que a Database RESULTADO teve de ser tratada a parte pois na linha 1646722 o NM_VOTAVEL estava como "SOLANGE "EM DEFESA DOS ANIMAIS", contendo uma aspas dupla a mais, o que causa erro na execução da query. O código em Python foi usado no Colaboratory para pular as linhas com defeitos de escrita.

## Colunas utilizadas

As seguintes colunas serão utilizadas para análise, pois contêm informações pertinentes a análise:

Eleitorado: DS_GENERO, DS_ESTADO_CIVIL, DS_FAIXA_ETARIA, DS_GRAU_ESCOLARIDADE.

Resultado: NM_VOTAVEL, NM_MUNICIPIO, DS_CARGO_PERGUNTA.

## Colunas não-utilizadas

Todas as outras colunas contêm informação que não é pertinente a esta análise, portanto qualquer coluna que não está na seção anterior não será utilizada


## Queries

A análise se dados foi feita consultando alguns valores triviais, tipo quantos votos foram para prefeito e quantos foram para vereador, tendo assim uma noção de quantas pessoas votaram somente para vereador, no formato de uma lista dos 10 estados com mais votos para os mesmos. Uma outra análise realizada foi algumas características dos perfis dos eleitores em geral, tipo faixa etária, estado civil e grau de escolaridade.

## Conclusão

Por conta de problemas de pouca memória, as queries com INNER JOIN não puderam ser concluidas a tempo, pois o processamento podia durar dias depois da dia de entrega, mas a conclusão envolveria a análise do perfil dos eleitores para descobrir qual a faixa etária, gênero ou grau de escolaridade para por exemplo, criar uma campanha de conscientização do voto, já que estatisticas mostram que a cada eleição a quantidade de votos nulo e branco aumenta gradativamente, o que é demonstrado nas queries de voto sem brancos e nulos e nos votos com brancos e nulos, cuja diferença é maior nas tabelas de prefeito (aproximadamente 10% a 25%) do que as de vereador (menos que 5%). Podemos então concluir que mais pessoas votam branco e nulo para prefeito do que vereador.