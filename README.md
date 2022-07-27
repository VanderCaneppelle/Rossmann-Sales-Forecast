# Previsão de Vendas - Rossmann 

Repositório com arquivos do modelo de Regressão desenvolvido para prever as vendas da rede de drogarias europeia Rossmann.

<i>Nota: Esse é um projeto fictício, de qualquer forma muito semelhante ao real problema enfrentado pelas organizações diariamente.</i>
 
## Previsão de Vendas - Rossmann

<img src="img/forecast1.png" width="900" height="400">
   

# 1.0 Problema de negócio
A Rossmann é uma grande rede de drogarias que atua no continente europeu. Recentemente, o CFO solicitou aos gerentes de cada loja para realizarem a previsão de vendas das próximas 6 semanas de suas respectivas lojas. Ele planeja realizar a reforma das lojas e para isso o orçamento estará condicionado as suas respectivas vendas. Com milhares de gerentes individuais prevendo as vendas a precisão dos resultados poderia acabar comprometida. Dessa maneira, foi solicitado que nós como cientista de dados realizássemos essa tarefa.


# 2.0 Premissas
* Os dados foram extraídos da base de vendas interna da empresa dos últimos 30 meses.
* As vendas das lojas são influenciadas por diversos fatores, incluindo promoções, competição, feriados, sazonalidade e localidade.
* Proximidade da concorrência: Para os casos em que a distância era 0, o valor foi substituído por 100.000 metros (valor superior que a máxima distância entre lojas no conjunto de dados), pois causariam problemas na implementação dos modelos de ML.
* Variedade: Foi considerado que lojas que vendiam o sortimento de produtos C também vendiam A e B.
* Loja Aberta: Foram removidas as linhas em que as lojas estavam fechadas e consequentemente com vendas 0, pois causariam problemas na etapa de implementação dos modelos de ML.
 

## Detalhamento dos Dados:
* Id - um Id que representa uma (Store, Date) dentro do conjunto de teste.
* Store - um ID exclusivo para cada loja.
* Sales - o volume de negócios para um determinado dia (é o que você está prevendo).
* Customers - o número de clientes em um determinado dia.
* Open - um indicador para saber se a loja estava aberta: 0 = fechado, 1 = aberto.
* StateHoliday - indica um feriado estadual. Normalmente todas as lojas, com poucas exceções, estão fechadas nos feriados estaduais. Observe que todas as escolas estão fechadas nos feriados e fins de semana. a = feriado, b = feriado da páscoa, c = natal, 0 = nenhum.
* SchoolHoliday - indica se a (Store, Date) foi afetada pelo fechamento de escolas públicas.
* StoreType - diferencia entre 4 modelos de loja diferentes: a, b, c, d.
* Assortment - descreve um nível de sortimento: a = básico, b = extra, c = estendido.
* CompetitionDistance - distância em metros até a loja concorrente mais próxima.
* CompetitionOpenSince[Month/Year] - fornece o ano e o mês aproximados em que o concorrente mais próximo foi aberto.
* Promo - indica se uma loja está executando uma promoção naquele dia.
* Promo2 - Promo2 é uma promoção contínua e consecutiva para algumas lojas: 0 = a loja não está participando, 1 = a loja está participando.
* Promo2Since[Year/Week] - descreve o ano e a semana do calendário em que a loja começou a participar do Promo2.
* PromoInterval - descreve os intervalos consecutivos em que a Promo2 é iniciada, nomeando os meses em que a promoção é iniciada novamente. Por exemplo. "Fevereiro, maio, agosto, novembro" significa que cada rodada começa em fevereiro, maio, agosto, novembro de qualquer ano para essa loja.  
 

# 3.0 Planejamento da solução
## - Produto final:
<b>Resposta</b>: Construir modelo de ML para realizar previsões de vendas para as próximas 6 semanas por loja em tempo real.

<b>Formato da entrega:</b> Valor abosluto de vendas nas próximas 6 semanas.

<b>Local de entrega:</b> Bot no Telegram

## - Processo:
<b>Passo a passo:</b> Etapas do CRISP

<b>Definição do formato da entrega:</b> Resposta escrita

<b>Decisão do local de entrega:</b> Celular, Tablet ou PC.

## - Entrada:
<b>Fonte de dados:</b> recebimento de base de dados arquivo .csv

<b>Ferramentas utilizadas:</b> Python, Heroku, Telegram, VSCode, Jupyter Notebook

 

## 3.1 Metodologia de desenvolvimento do projeto
O método utilizado para o projeto será o CRISP que é um processo cíclico, flexível e ágil, capaz de lidar com problemas complexos envolvendo grande quantidade de dados.

![crisp](img/crispy.png)

# 4.0 Insights
Para a etapa que geralmente leva mais tempo em projetos de Data Science que é a de exploração dos dados ou também conhecida como feature engineering, foi desenvolvido um mapa de hipóteses com o objetivo de facilitar a criação, transformação e seleção das features para contribuição na geração de insights e entendimento do negócio.  
  
![Screenshot](img/MindMapHypotesis.png)

 <b> Sendo assim as principais hipóteses levantadas, foram:</b>

Lojas com maior sortimentos deveriam vender mais.

Lojas com competidores mais próximos deveriam vender menos.

Lojas com competidores à mais tempo deveriam vender mais.

Lojas com promoções ativas por mais tempo deveriam vender mais.

Lojas com mais dias de promoção deveriam vender mais.

Lojas com mais promoções consecutivas deveriam vender mais.

Lojas abertas durante o feriado de Natal deveriam vender mais.

Lojas deveriam vender mais ao longo dos anos.

Lojas deveriam vender mais no segundo semestre do ano.

Lojas deveriam vender mais depois do dia 10 de cada mês.

Lojas deveriam vender menos aos finais de semana.

Lojas deveriam vender menos durante os feriados escolares.  

Como resultado, 3 hipóteses foram confirmadas (tabela abaixo):

|Hipóteses | Conclusão | Relevância|
|----------|----------|------------|
|H1|    Falsa | Baixa|
|H2|	Falsa |	Media|
|H3|	Falsa |Media|
|H4|	Falsa |	Baixa|
|H5|	- |	-|
|H6|	Falsa |	Baixa|
|H7|	Falsa |	Media|
|H8|	Falsa |	Alta|
|H9|	Falsa |	Alta|
|H10|	Verdadeira |	Alta|
|H11|	Verdadeira |	Alta|
|H12|	Verdadeira |	Baixa|


# 5.0 Performance do modelo
Nessa etapa foram testados 04 algoritmos de Machine Learning, sendo eles: Linear Regression, Lasso Regression, Random Forest Regressor e o XGBoost Regressor. Também foi utilizada a técnica de validação cruzada em Time Series Split para treinar e validar os modelos. Podemos visualizar os resultados abaixo:

<b>Resultados dos Modelos de Machine Learning </b>

|       Model Name         |       MAE CV        |      MAPE CV   |        RMSE CV      |
| ------------------------ | ------------------- | -------------  | ------------------- |
|  Linear Regression       |  2081.73 +/- 295.63 |  0.3 +/- 0.02  |  2952.52 +/- 468.37 |
|  Lasso                   |  2116.38 +/- 341.5  |  0.29 +/- 0.01 |  3057.75 +/- 504.26 |
|  Random Forest Regressor |  836.61 +/- 217.1   |  0.12 +/- 0.02 |  1254.3 +/- 316.17  |
|  XGBoost                 |  1039.91 +/- 186.68 |  0.14 +/- 0.02 |  1496.16 +/- 258.53 |


Podemos notar que os dois modelos de regressão não tiveram boa performance se comparando aos modelos de Random Forest e XGBoost. O algoritmo de Random Forest foi o que apresentou a melhor performance no primeiro momento, mas optamos por seguir com o modelo XGBoost por ele ser mais performático e geralmente produzir resultados superiores utilizando menos recursos de computação em menor período de tempo.

# 6.0 Modelo Final

|    Model Name   |    MAE CV   |   MAPE CV   |     RMSE CV  |
| --------------- | ----------- |  ---------  | ------------ |
|  XGBoost        |  670.602101 |  0.098162   |  965.036319  |

Após processar novamente o modelo do XGBoost nessa etapa realizando o ajuste fino dos hiperparâmetros através da técnica de Random Search (escolha dessa técnica muito alinhada com o método CRISP de terminar o primeiro ciclo do projeto em menor tempo possível e já entregando valor para o negócio).

<b>MAE (Mean Absolute Error) - é o erro absoluto médio.</b>
Considerando o nosso modelo final, significa que o modelo pode errar em aproximadamente $ 670.6 para cima ou para baixo na previsão diária de cada loja.

<b>MAPE (Mean Absolute Percentual Error) - é o erro absoluto médio percentual.</b>
Considerando o nosso modelo final, significa que o modelo pode errar em aproximadamente 9.8% o que equivale aos $ 670.6.

<b> RMSE (Root Mean Squared Error) - é a raiz do erro quadrático médio. </b>
Considerando o nosso modelo final, significa que o modelo pode errar em 965 unids.

 <b>Abaixo a representação gráfica do resultado:</b>

![prediction](img/result_graph.png)

Resultados das Previsões

|   Scenario    |      Values       |
|---------------|-------------------|
|predictions	|  $ 283,796,832.00 |
|worst_scenario	|  $ 255,177,168.14 |
|best_scenario	|  $ 312,416,497.10 |

Por fim, a tabela acima apresenta a previsão das vendas nas próximas 6 semanas das lojas, além disso considera o melhor e o pior cenário também.

# 7.0 Produto Final
Como entrega final aos gestores, segue detalhe de ferramenta desenvolvida de BOT no Telegram já disponibilizada em produção (Heroku) para suporte a tomada de decisão.

![bot](img/instagram_bot.jpeg)

# 8.0 Conclusão
A metodologia de projetos CRISP gera enorme valor aos negócios, pois através do método cíclico de projetos já é possível entregar valor para a empresa em curto espaço de tempo, isso é muito relevante nos dias atuais, considerando a grande competição que existe no mercado independente do ramo de atividade da empresa.

Apenas evidenciado o valor da informação gerada nesse projeto, essa informação poderia facilmente ser utilizada, como apoio ao setor de Compras no gerenciamento de custo e estoque, para apoiar também o time de Marketing para desenvolvimento de campanhas, entre outros.

## Próximos passos

* Realizar novo ciclo do CRISP
* Apresentar novas features ao modelo
* Gerar mais insigths
* Testar outros modelos de ML
