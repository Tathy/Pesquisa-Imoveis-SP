# Pesquisa sobre imóveis de São Paulo - SP :houses:

:open_book: Projeto desenvolvido na Imersão Dados da Alura

[Link pro Google Colab](https://colab.research.google.com/drive/1DSTwxmWOApYzRQGef0kJtMMSCyjZkHc_?usp=sharing) (possivelmente mais atualizado)

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
  <img margin=50px src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/Hitograma_valor_imoveis.png?raw=true"/>
</div>


Usando um histograma, podemos observar a distribuição da quantidade de imóveis disponíveis em várias faixas de valores, quais faixas abrangem mais imóveis, e a tendência da relação quantidade de imóves x valor.

Neste caso, a quantidade de imóveis disponíveis no dataset tente a diminuir à medida que o valor de vena aumenta. Ainda não é possível afirmar que a maior parte dos imóveis vale menos que 2 milhões, mas grande parte se encaixaria nesta afirmação.


<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-Imoveis-SP/blob/main/imagens/Boxplot_precos_bairro.png?raw=true"/>
</div>

Essa visualização evidencia um grande problema que ainda está atrapalhando a plotagem de gráficos: os outliers. Alguns imóveis estão com preços muito acima média quando comparados aos seus semelhantes em vários aspectos, neste caso, na proximidade geográfica do bairro.

Dados assim podem ser reais, em que imóveis realmente estão superfaturados, ou podem ser ruídos gerados desde a coleta. É possível que hajam lotes vazios, sítios ou chácaras, que poderiam ter seus preços analisados separadamente, ou valores distorcidos por simples erros humanos no momento da inserção dos preços.
