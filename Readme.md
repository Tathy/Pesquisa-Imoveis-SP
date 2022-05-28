# Pesquisa sobre imóveis de São Paulo - SP :houses:

:open_book: Projeto desenvolvido na Imersão Dados da Alura

[Link pro Google Colab](https://colab.research.google.com/drive/1DSTwxmWOApYzRQGef0kJtMMSCyjZkHc_?usp=sharing)

## Aula 01 - Primeiro Colab com Python Pandas

Importação da base de dados e análises básicas de algumas características dos imóveis separados por bairro.

Os dados ainda precisam de tratamentos como: 
  - separar o nome da rua do número do imóvel (ou remover o número)
  - classificar imóveis entre venda ou aluguel
  - classificar imóveis por tipo de lote (chácara ou sítio)
  - converter o valor para um tipo numérico

## Aula 02 - Tratamento de dados e primeiros gráficos

As informações presentes na coluna de valores foram divididas entre moeda (reais), tipo de anúncio (venda e algueis anuais, mensais e diário), e o montante de dinheiro em valor numérico.

Seguem alguns gráficos e conclusões que merecem destaque.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/Hitograma_valor_imoveis.png?raw=true"/>
</div>

Usando um histograma, podemos observar a distribuição da quantidade de imóveis disponíveis em várias faixas de valores, quais faixas abrangem mais imóveis, e a tendência da relação quantidade de imóves x valor.

Neste caso, a quantidade de imóveis disponíveis no dataset tente a diminuir à medida que o valor de venda aumenta. Ainda não é possível afirmar que a maior parte dos imóveis vale menos que 2 milhões, mas grande parte se encaixaria nesta afirmação.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/Boxplot_precos_bairro.png?raw=true"/>
</div>

Essa visualização evidencia um grande problema que ainda está atrapalhando a plotagem de gráficos: os outliers. Alguns imóveis estão com preços muito acima média quando comparados aos seus semelhantes em vários aspectos, neste caso, na proximidade geográfica do bairro.

Dados assim podem ser reais, em que imóveis realmente estão superfaturados, ou podem ser ruídos gerados desde a coleta. É possível que hajam lotes vazios, sítios ou chácaras, que poderiam ter seus preços analisados separadamente, ou valores distorcidos por simples erros humanos no momento da inserção dos preços.

## Aula 03 - Gráficos, Time Series e Análise Exploratória

A aula começou com a sugestão de uma forma de resolver o Desafio 3 da aula anterior, em que foi pedido o preço do m² em cada bairro.

### 1) Gráfico gerado por mim

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula03_dest4.png?raw=true"/>
</div>

### 2) Resolução sugerida na aula

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula03_dest1.png?raw=true"/>
</div>

A diferença entre a solução acima (2) e a solução anterior (1) está no critério usado para selecionar quais bairros teriam seu valor por m² exibidos em gráfico.
- No gráfico (1), os bairros analisados estão ordenados por maior valor po m². ```sort_values```
- Já no gráfico (2), foram escolhidos os bairros com mais imóveis registrados no dataset. ```value_counts```

### Remoção básica de um outlier

Selecionamos os dez bairros com mais imóveis disponíveis no dataset e comparamos suas metragens utlizando boxplot.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula03_dest2.png?raw=true"/>
</div>

A visialização ficou totalmente distorcida por causa de um outlier, um imóvel do bairro Jardim Guedala com metragem muito acima dos outros. Ao filtrarmos os imóveis com menos de 30.000 de metragem, pudemos identificar outliers menos discrepantes.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula03_dest3.png?raw=true"/>
</div>

### Limpeza de dados para remoção de mais outliers

Executei alguns filtros a mais como parte de um dos desafios da aula. Foram retirados:

- imóveis com mais de 6 quartos
- imóveis com mais de 5 banheiros
- imóveis com mais de 5 vagas
- imóveis que continham "Sítio" ou "Chácara" presentes no nome do bairro

O gráfico abaixo pode ser comparado com o acima. Ainda há outliers, mas os preços mais altos estão menos discrepantes, mesmo não havendo nenhum filtro diretamente relacionado ao valor.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula03_dest5.png?raw=true"/>
</div>

## Aula 04 - Cruzando bases de dados

Nesta aula, usamos duas outras bases de dados para relacionarmos os imóveis disponíveis para venda e os dados do IBGE.

- a latitude e longitude dos imóveis foram encontradas com base nos nomes das ruas utilizando uma base de dados extra
- a longitude e latitude foram usadas para identificar os setores censitários utilizando cálculos com polígonos e uma segunda base de dados extra

Os tratamentos e mesclagens resultaram em uma base de dados com todas as informações relacionadas em uma única tabela, que será utilizada em análises posteriores.

Um exemplo de análise pode ser vista no gráfico abaixo. Observa-se que há uma tendência dos proprietários com maior renda residirem em imóveis de áreas com m² mais caro, mas os pontos ainda estão muito dispersos para uma conclusão satisfatória. Isto indica que esta análise pode não ser a melhor para precificação de imóveis.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula04_dest1.png?raw=true"/>
</div>

## Aula 05 - Machine Learning

### Correlações

Foram feitas algumas análises sobre a correlação entre as variáveis disponíveis nos dados de imóveis à venda e IBGE. 

Apesar de algumas parecerem promissoras, há algumas observações a serem feitas.
- Valor_mm e Valor_anuncio, com correlação 1, uma é diretamente derivada da outra
- As perguntas (V00x) tiveram alguns valores altos de correlação entre sim. Geralmente essas variáveis vinham em duplas, com uma medida seguida da sua variância.
- As perguntas V005, V007, V009 e V011 tiveram a correlação mais alta com os valores de anúncio, todas relacionadas à situções financeiras das famílias.
    - V005: Valor do rendimento nominal médio mensal das pessoas responsáveis por domicílios particulares permanentes (com e sem rendimento)
    - V007: Valor do rendimento nominal médio mensal das pessoas responsáveis por domicílios particulares permanentes (com rendimento)
    - V009: Valor do rendimento nominal médio mensal das pessoas de 10 anos ou mais de idade (com e sem rendimento)
    - V011: Valor do rendimento nominal médio mensal das pessoas de 10 anos ou mais de idade (com rendimento)
- Entretanto, as correlações com o valor do m² foram mais baixas

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula05_dest3.png?raw=true"/>
</div>

### Predições

#### Regressão Linear

Em seguida, foram feitas algumas predições utilizando Regressão Linear com um conjunto reduzido de variáveis. Os modelos foram avaliados via Erro Absoluto Médio (MAE) e Coeficiente de Determinação (r²).

Relacionando-se Metragem, número de quartos, banheiros, vagas de garagem, latitude, longitude e todo o conjunto de perguntas do IBGE, atingimos MAE = 1333549.33 e r² = 0.403. O modelo não foi considerado bom o suficiente para predizer valores de vendas de imóveis, prevendo, inclusive, valores negativos pro anúncio.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula05_dest1.png?raw=true"/>
</div>

#### Regressão Polinomial

Após algumas tentativas com outros modelos como desafio da aula, encontrei um resultado um pouco melhor utilizando Regressão Polinomial e um conjnto de variáveis menor (Metragem, número de quartos, banheiros, vagas e a pergunta V007 do IBGE, relacionada acima). Este modelo apresentou MAE = 1214326.04 e r² = 0.456, seus pontos ficaram um pouco menos dispersos e houveram menos sugestões de preços negativos.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/aula05_dest2.png?raw=true"/>
</div>

# Conclusões

Os modelos estudados não apresentaram predições satisfatórias. O baixo rendimento pode estar diretamente relacionado à base de dados pequena. Uma avaliação melhor sobre variáveis escolhidas também necessitaria de mais dados.

Talvez características socioeconômicas ajudem nessa predição. Fatores como segurança, proximidade a metrôs, pontos de ônibus, shoppings e comércio, disponibilidade de água e acesso facilitado a outros itens de necessidade básica costumam interferir na compra de imóveis.

🎉
