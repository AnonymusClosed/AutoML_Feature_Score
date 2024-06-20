# AutoML no Contexto de Malware Android: da Automatização e Desempenho à Transparência e XAI

## AutoML Feature Score


AutoML Feature Score combina conceitos de transparência e interpretabilidade propostos por diversos trabalhos na literatura [1][2][3][4][5]. O objetivo é aplicar esses conceitos de forma categórica destinado a avaliar quanto a transparência e interpretabilidade de frameworks de AutoML. A pontuação das perguntas é baseada no número de formas em que o framework atende a cada critério, variando de 0 a 2 pontos, dependendo do grau de cumprimento. Essa pontuação é então normalizada em uma escala de 0 a 100% para cada nível de avaliação, garantindo uma comparação justa e consistente entre diferentes frameworks. A abordagem considera tanto questões específicas, como a funcionalidade das etapas do pipeline, quanto aspectos mais amplos, como a análise estatística e a transparência algorítmica, proporcionando uma avaliação abrangente e detalhada dos frameworks examinados.



### Pontuação das perguntas
Seja:
-   $S$ a pontuação atribuída ao framework para uma determinada categoria.
-   $N$ o número de formas (ex,. métodos, algoritmos) nas quais o framework satisfaz a pergunta da categoria.

Então, a pontuação $S$ pode ser definida como:

$$
S = \begin{cases} 
0 & \text{se } N = 0 \\
1 & \text{se } N = 1 \\
2 & \text{se } N \geq 2 
\end{cases}
$$

Essa formulação matemática expressa claramente as condições de pontuação para cada pergunta: 

| "N"= Não se aplica       | "P"= Parcial            | "T"= Total               |
| ------------------------ | ----------------------- | ------------------------ |
| $0$ pontos quando $N=0$. | $1$ ponto quando $N=1$. | $2$ pontos quando $N≥2$. |


No caso em que o número de possibilidades de resposta é conhecido, como no exemplo das etapas do pipeline de um framework, as pontuações são atribuídas da seguinte forma:

-   "N" (Não se aplica) = 0 pontos
-   "P" (Parcial) = 1 ponto
-   "T" (Total) = 2 pontos

Porém, em situações em que a pergunta pode levar a um número indefinido de possibilidades de resposta, como no caso do framework oferecer modelos com interpretabilidade intrínseca, a pontuação é atribuída da seguinte maneira:

-   "N" (Não se aplica) = 0 pontos, se nenhum modelo intrínseco de interpretabilidade for utilizado.
-   "P" (Parcial) = 1 ponto, se pelo menos um modelo de interpretabilidade intrínseca for utilizado.
-   "T" (Total) = 2 pontos, se dois ou mais modelos de interpretabilidade intrínseca forem utilizados pelo framework.

Essa abordagem permite uma avaliação flexível, levando em consideração o contexto específico de cada pergunta e a possibilidade de múltiplas respostas, garantindo uma atribuição adequada de pontos com base nas características do framework em questão.

### Avaliação das categorias
A forma de pontuação proposta garante que a pontuação final de um framework para um determinado nível esteja normalizada em uma escala que varia de 0 a 100%. Isso é alcançado calculando-se a pontuação real obtida pelo framework para todas as perguntas do nível e dividindo essa soma pelo produto do número total de perguntas e da pontuação máxima atribuída por pergunta. Essa relação garante que a pontuação final possa variar de 0% a 100%, independentemente do número de perguntas em cada nível ou da escala de pontuação máxima. Assim, essa abordagem proporciona uma maneira justa e consistente de avaliar o desempenho dos frameworks, permitindo uma comparação direta entre eles, onde uma pontuação mais alta indica um maior cumprimento dos critérios de transparência e interpretabilidade.



Seja:
- $S$ a pontuação final normalizada do framework para a categoria.
- $P_i$ a pontuação obtida pelo framework para a i-ésima pergunta da categoria.
- $N$ o número total de perguntas nesta categoria.
- $W$ a pontuação máxima atribuída por pergunta.


Então, a fórmula pode ser formalizada como:

$$
S=\left( \frac{ {\sum_{i=1}^{N} P_i} }{{N\cdot W}}\right )\times 100
$$

Essa formulação expressa a pontuação final $S$ como a soma das pontuações obtidas para todas as perguntas dividida pelo produto do número total de perguntas e da pontuação máxima por pergunta, tudo isso multiplicado por 100 para obter a porcentagem final. Abaixo é apresentada a tabela modelo de avaliação proposta.

| Categoria               | Pergunta                                                                                           | Avaliação | Pontuação | Score |
|-------------------------|---------------------------------------------------------------------------------------------------|-----------|-----------|-------|
| Descrição Funcional     | É possível identificar quais são as etapas do pipeline?                                           | T         | 2         | 100   |
|                         | É possível identificar os componentes utilizados em cada etapa?                                   | T         | 2         |       |
|                         | Está claro quais são as entradas e saídas?                                                        | T         | 2         |       |
|                         | Está claro como o processo é executado na prática?                                                | T         | 2         |       |
| Análise Estatística     | As previsões do modelo são apresentadas para as classes (malwares e benignos)?                    | T         | 2         | 100   |
|                         | Mantém o histórico dos dados utilizados para treinar e testar o modelo?                           | T         | 2         |       |
|                         | Na seleção de características é informado ao usuário quais são as mais relevantes?                | T         | 2         |       |
|                         | As métricas de desempenho do modelo são apresentadas?                                             | T         | 2         |       |
|                         | Existem formas de visualizar os resultados (gráficos, tabelas)?                                    | T         | 2         |       |
| Transparência Algorítmica | É possível identificar quais modelos são utilizados?                                              | T         | 2         | 100   |
|                         | É possível identificar avisos, informações e erros registrados nos logs do sistema?               | T         | 2         |       |
|                         | É possível identificar os hiperparâmetros dos modelos gerados?                                    | T         | 2         |       |
|                         | É possível identificar se os dados são balanceados?                                               | T         | 2         |       |
| Interpretabilidade     | O motivo da redução da dimensionalidade é explicado? (Pré-Modelo)                                 | T         | 2         | 100   |
|                         | Existem técnicas específicas de redução de dimensionalidade para o domínio? (Pré-Modelo)         | T         | 2         |       |
|                         | Há métodos de interpretabilidade global disponíveis?                                               | T         | 2         |       |
|                         | O framework oferece modelos com interpretabilidade intrínseca? (In-Modelo)                         | T         | 2         |       |
|                         | É possível avaliar a diferença entre previsões e valores reais?                                    | T         | 2         |       |
|                         | Há métodos de interpretabilidade independentes do modelo? (Pós-Modelo)                            | T         | 2         |       |
| Análise Interna        | Existem métodos para visualizar a estrutura do modelo? (Pós-Modelo)                                | T         | 2         | 100   |


- **Descrição Funcional:**
  Tem como objetivo avaliar se os frameworks de AutoML cumprem suas funções de maneira clara e transparente para o usuário. Isso envolve a identificação das diferentes etapas do pipeline, a compreensão dos componentes utilizados em cada etapa, a clareza das entradas e saídas do sistema e a explicação detalhada de como o processo é executado na prática. Ao assegurar que todas essas informações estejam disponíveis e compreensíveis, a categoria "Descrição Funcional" garante que os usuários possam entender e confiar no funcionamento do framework, promovendo uma utilização mais eficiente e eficaz da ferramenta.

- **Análise Estatística:**
  Tem como objetivo avaliar a capacidade dos frameworks de AutoML em apresentar e explicar os resultados estatísticos e métricas de desempenho de maneira clara e detalhada. Esta categoria verifica se as previsões do modelo são devidamente apresentadas para diferentes classes, como malwares e benignos, e se o histórico dos dados utilizados para treinamento e teste é mantido. Além disso, avalia se os usuários são informados sobre as características mais relevantes durante a seleção de características, se as métricas de desempenho do modelo são claramente exibidas e se existem métodos visuais, como gráficos e tabelas, para a visualização dos resultados. Cumprindo esses critérios, a categoria "Análise Estatística" contribui para que os usuários possam entender e confiar na eficácia dos modelos gerados pelo framework, promovendo uma maior transparência e interpretabilidade na etapa de pré-Modelo.

- **Transparência Algorítmica:**
  A categoria tem como objetivo avaliar a clareza e a objetividade com que os frameworks de AutoML apresentam informações sobre os algoritmos utilizados. Esta categoria verifica se é possível identificar quais modelos são empregados em cada etapa do processo, se os avisos, informações e erros são registrados e acessíveis nos logs do sistema, se os hiperparâmetros dos modelos gerados são claramente apresentados, e se os dados são balanceados em termos de proporcionalidade das classes. Ao cumprir esses critérios, a categoria "Transparência Algorítmica" assegura que os usuários possam compreender detalhadamente os eventos do sistema, facilitando a análise e a interpretação dos modelos, além de garantir uma otimização eficiente e justa dos dados utilizados.

- **Interpretabilidade:**
  A categoria "Interpretabilidade" é crucial para garantir que os usuários compreendam não apenas os resultados, mas também os processos internos dos modelos gerados pelos frameworks de AutoML. Esta categoria está dividida em três subcategorias: pré-modelo, in-modelo e pós-modelo, cada uma abordando aspectos específicos da interpretabilidade. No estágio pré-modelo, é importante que o motivo da redução da dimensionalidade seja explicado e que existam técnicas específicas de redução de dimensionalidade para o domínio em questão. No estágio in-modelo, a ênfase está em oferecer modelos com interpretabilidade intrínseca, permitindo aos usuários entender como as previsões são geradas. Finalmente, no estágio pós-modelo, é fundamental avaliar a diferença entre previsões e valores reais e disponibilizar métodos de interpretabilidade independentes do modelo. Essas práticas asseguram que os usuários possam confiar nas decisões tomadas pelos modelos, promover uma melhor compreensão dos resultados e facilitar a identificação de possíveis melhorias no processo de modelagem.

- **Análise Interna:**
  Essa categoria foca na capacidade dos frameworks de AutoML em fornecer métodos para visualizar a estrutura interna dos modelos gerados. A visualização da estrutura do modelo é essencial para que os usuários compreendam como os dados são processados e como as decisões são tomadas dentro do modelo. Por exemplo, a visualização de uma árvore de decisão permite que os usuários vejam claramente as ramificações e critérios usados em cada nó para realizar uma previsão, facilitando a interpretação do processo de decisão. Este entendimento profundo permite não apenas uma melhor interpretação dos resultados, mas também facilita a identificação de possíveis problemas ou áreas de melhoria. Ao oferecer ferramentas de visualização da estrutura, os frameworks capacitam os usuários a realizar uma análise crítica e detalhada, promovendo a transparência e a confiança nos modelos desenvolvidos.


### Aplicação prática
A avaliação completa para cada ferramenta pode ser acessada [aqui](https://docs.google.com/spreadsheets/d/1B3uKCdwRsdOYjzJNuYtJmMN87GJ1njXr5GLsLm7hYws/edit?usp=sharing) :arrow_down:

### Tabela de Avaliação de Transparência e Interpretabilidade de Frameworks de AutoML

| **Categoria**               | **Ferramenta**  | **Pontuação Total** |
|-----------------------------|-----------------|---------------------|
| **Descrição Funcional**     | AutoGluon       | 100                 |
|                             | MH-AutoML       | 100                 |
|                             | Auto-Sklearn    | 100                 |
|                             | TPOT            | 100                 |
|                             | AutoPyTorch     | 100                 |
|                             | LightAutoML     | 100                 |
|                             | HyperGBM        | 100                 |
|                             | MLJar           | 100                 |
| **Análise Estatística**     | AutoGluon       | 80                  |
|                             | MH-AutoML       | 70                  |
|                             | Auto-Sklearn    | 60                  |
|                             | TPOT            | 60                  |
|                             | AutoPyTorch     | 60                  |
|                             | LightAutoML     | 60                  |
|                             | HyperGBM        | 80                  |
|                             | MLJar           | 100                 |
| **Transparência Algorítmica**| AutoGluon      | 75                  |
|                             | MH-AutoML       | 87.5                |
|                             | Auto-Sklearn    | 50                  |
|                             | TPOT            | 50                  |
|                             | AutoPyTorch     | 75                  |
|                             | LightAutoML     | 75                  |
|                             | HyperGBM        | 75                  |
|                             | MLJar           | 75                  |
| **Interpretabilidade**      | AutoGluon       | 41.6                |
|                             | MH-AutoML       | 41.6                |
|                             | Auto-Sklearn    | 25                  |
|                             | TPOT            | 8.33                |
|                             | AutoPyTorch     | 33.33               |
|                             | LightAutoML     | 41.6                |
|                             | HyperGBM        | 50                  |
|                             | MLJar           | 58.33               |
| **Análise Interna**         | AutoGluon       | 50                  |
|                             | MH-AutoML       | 0                   |
|                             | Auto-Sklearn    | 50                  |
|                             | TPOT            | 100                 |
|                             | AutoPyTorch     | 0                   |
|                             | LightAutoML     | 0                   |
|                             | HyperGBM        | 100                 |
|                             | MLJar           | 100                 |


![enter image description here](https://raw.githubusercontent.com/JonerMello/COVID19/master/IMG/AutoML_Feature_Score.png)

Na avaliação dos frameworks de AutoML a categoria de Descrição Funcional, todas as ferramentas, incluindo AutoGluon, MH-AutoML, Auto-Sklearn, TPOT, AutoPyTorch, LightAutoML, HyperGBM e MLJar, alcançaram a pontuação máxima de 100 pontos, indicando clareza e transparência de suas funções. Na Análise Estatística, MLJar liderou com 100 pontos, seguido por AutoGluon e HyperGBM, ambos com 80 pontos. LightAutoML, Auto-Sklearn, TPOT, MH-AutoML e AutoPyTorch tiveram um desempenho mediano entre 70 e 60 pontos. Esses resultados indicam que essas ferramentas não mantêm um histórico dos dados utilizados para treinar e testar o modelo e não apresentam, ou apresentam parcialmente, as características mais relevantes para o usuário. Em termos de Transparência Algorítmica, MH-AutoML destacou-se com 87,5 pontos. AutoGluon, AutoPyTorch, LightAutoML, HyperGBM e MLJar seguiram com 75 pontos cada. Auto-Sklearn e TPOT mostraram necessidade de melhorias, alcançando apenas 50 pontos cada. As principais deficiências dessas ferramentas estão relacionadas à falta de transparência quanto ao balanceamento de classes e nos logs do sistema.

Na categoria de Interpretabilidade, MLJar foi a melhor avaliada com 58,33 pontos, destacando-se por fornecer modelos e resultados facilmente compreensíveis. HyperGBM também obteve uma boa pontuação de 50 pontos. LightAutoML, AutoGluon e MH-AutoML alcançaram 41,6 pontos cada. AutoPyTorch teve uma pontuação mediana de 33,33 pontos, enquanto Auto-Sklearn obteve 25 pontos. TPOT teve a menor pontuação, com 8,33 pontos, indicando dificuldades significativas de interpretabilidade. As principais deficiências dessas ferramentas incluem a falta de opções para utilizar exclusivamente métodos de interpretabilidade intrínseca, métodos específicos para domínios particulares, explicações sobre a escolha de métodos de redução de dimensionalidade e a ausência de métodos de interpretabilidade independentes de modelo, como SHAP e LIME.

Finalmente, na Análise Interna, TPOT, HyperGBM e MLJar se destacaram com 100 pontos cada, evidenciando sua capacidade de apresentar detalhadamente a estrutura dos modelos utilizados, como árvores de decisão, por exemplo. AutoGluon e Auto-Sklearn receberam 50 pontos nesta categoria, indicando uma apresentação moderada da estrutura dos modelos. Por outro lado, MH-AutoML, AutoPyTorch e LightAutoML mostraram uma necessidade significativa de melhorias, alcançando 0 pontos, o que reflete a falta de detalhamento na apresentação da estrutura dos modelos utilizados.

Esta análise destaca que, apesar de algumas ferramentas apresentarem excelente desempenho em métricas como acurácia, recall, F1 score e precisão, é igualmente crucial considerar questões de interpretabilidade e transparência. Estes aspectos não só aumentam a confiança nos resultados, mas também tornam o entendimento das decisões mais sólido. É fundamental que as ferramentas de AutoML sejam transparentes e interpretáveis, além de apresentarem bom desempenho, especialmente no contexto da detecção de malwares em dispositivos Android.

Em resumo, as ferramentas de AutoML, de maneira geral, demonstram boa transparência em relação ao seu pipeline. No entanto, há uma lacuna significativa em termos de transparência e interpretabilidade dos resultados e dos artefatos gerados. Embora algumas ferramentas se destaquem pela clareza funcional, a habilidade de fornecer modelos compreensíveis e de visualizar a estrutura interna ainda requer melhorias substanciais. Estas melhorias são essenciais para aumentar a confiança nos resultados e facilitar a compreensão das decisões tomadas pelos modelos, especialmente em aplicações críticas como a detecção de malwares em dispositivos Android. Para abordar estas questões, as ferramentas poderiam adotar uma opção de interpretabilidade de modelos onde apenas modelos de aprendizado de máquina com interpretabilidade intrínseca, como KNN (K-Nearest Neighbors) e Árvores de Decisão fossem utilizados, tambem utilizar técnicas de interpretabilidade independentes de modelo, como SHAP (Shapley Additive Explanations) e LIME (Local Interpretable Model-agnostic Explanations), juntamente com logs de sistemas claros e objetivos. Essas abordagens ajudariam a tornar os modelos mais transparentes e as decisões mais compreensíveis para os usuários finais.

## Resultados dos testes com as ferramentas

A seguir temos os resultados da execução de todos os testes com as ferramentas de automl.

### Execução das ferramenta com ensemble (configuração padrão)

Os resultados a seguir se referem a Tabela 3 do artigo.


| Dataset              | Ferramenta   | Acurácia | Precisão | Recall | F1    | Tempo   |
|----------------------|--------------|----------|----------|--------|-------|---------|
| KronoDroid Emulator  | AutoGluon    | 0,9725   | 0,9713   | 0,9669 | 0,9691| 00:08:10|
|                      | Auto-Sklearn | 0,9711   | 0,9684   | 0,9665 | 0,9675| 00:59:55|
|                      | TPOT         | 0,9599   | 0,9531   | 0,9571 | 0,9551| 00:53:12|
|                      | AutoPyTorch  | 0,9754   | 0,9692   | 0,9671 | 0,9677| 00:59:56|
|                      | LightAutoML  | 0,9722   | 0,9707   | 0,9667 | 0,9687| 00:14:16|
|                      | HyperGBM     | 0,9688   | 0,9688   | 0,9688 | 0,9688| 00:05:33|
|                      | MLJar        | 0,9731   | 0,9691   | 0,9671 | 0,9677| 00:59:59|
| KronoDroid Real Devices  | AutoGluon    | 0,9744   | 0,9787   | 0,9757 | 0,993 | 00:06:54|
|                      | Auto-Sklearn | 0,9717   | 0,9748   | 0,9716 | 0,9732| 00:59:55|
|                      | TPOT         | 0,9689   | 0,9721   | 0,969  | 0,9705| 00:33:26|
|                      | AutoPyTorch  | 0,973    | 0,976    | 0,972  | 0,9713| 00:59:59|
|                      | LightAutoML  | 0,9753   | 0,9791   | 0,9741 | 0,9766| 00:14:10|
|                      | HyperGBM     | 0,9677   | 0,9677   | 0,9677 | 0,9677| 00:06:50|
|                      | MLJar        | 0,9719   | 0,975    | 0,9717 | 0,9735| 00:59:57|
| AndroCrawl           | AutoGluon    | 0,9866   | 0,9429   | 0,9286 | 0,9357| 00:04:13|
|                      | Auto-Sklearn | 0,9875   | 0,9471   | 0,9327 | 0,9399| 00:59:58|
|                      | TPOT         | 0,9869   | 0,9493   | 0,9246 | 0,9368| 01:02:42|
|                      | AutoPyTorch  | 0,973    | 0,976    | 0,972  | 0,9713| 00:59:59|
|                      | LightAutoML  | 0,9753   | 0,9791   | 0,9741 | 0,9766| 00:14:10|
|                      | HyperGBM     | 0,9677   | 0,9677   | 0,9677 | 0,9677| 00:06:50|
|                      | MLJar        | 0,9719   | 0,975    | 0,9717 | 0,9735| 00:59:57|
| Android Permissions  | AutoGluon    | 0,6726   | 0,6836   | 0,9426 | 0,7925| 00:01:28|
|                      | Auto-Sklearn | 0,6738   | 0,6788   | 0,9646 | 0,7968| 00:59:56|
|                      | TPOT         | 0,6733   | 0,6867   | 0,9333 | 0,7912| 00:40:01|
|                      | AutoPyTorch  | 0,6838   | 0,6799   | 0,9673 | 0,8003| 01:07:23|
|                      | LightAutoML  | 0,6749   | 0,6857   | 0,9415 | 0,7935| 00:07:07|
|                      | HyperGBM     | 0,6728   | 0,6497   | 0,6728 | 0,58  | 00:01:09|
|                      | MLJar        | 0,674    | 0,679    | 0,9649 | 0,7971| 00:59:57|
| DefenseDroid PRS     | AutoGluon    | 0,9301   | 0,9444   | 0,9173 | 0,9307| 00:04:47|
|                      | Auto-Sklearn | 0,9215   | 0,9349   | 0,9099 | 0,9222| 01:00:04|
|                      | TPOT         | 0,9228   | 0,9454   | 0,901  | 0,9227| 00:55:27|
|                      | AutoPyTorch  | 0,9226   | 0,9363   | 0,91   | 0,9231| 01:03:04|
|                      | LightAutoML  | 0,9289   | 0,956    | 0,9025 | 0,9285| 00:11:23|
|                      | HyperGBM     | 0,9238   | 0,9374   | 0,9119 | 0,9245| 00:02:55|
|                      | MLJar        | 0,922    | 0,9351   | 0,9099 | 0,9229| 01:00:05|
| DREBIN-215               | AutoGluon    | 0,9862   | 0,9846   | 0,9782 | 0,9814| 00:01:13|
|                      | Auto-Sklearn | 0,985    | 0,9872   | 0,9722 | 0,9797| 01:00:06|
|                      | TPOT         | 0,9817   | 0,9864   | 0,9841 | 0,9793| 00:44:24|
|                      | AutoPyTorch  | 0,9852   | 0,9876   | 0,9727 | 0,9801| 01:00:10|
|                      | LightAutoML  | 0,9867   | 0,9863   | 0,9777 | 0,982 | 00:11:14|
|                      | HyperGBM     | 0,9825   | 0,9825   | 0,9825 | 0,9824| 00:01:35|
|                      | MLJar        | 0,9852   | 0,9874   | 0,9723 | 0,9798| 01:00:07|
| ADROIT               | AutoGluon    | 0,9136   | 0,8964   | 0,7992 | 0,845 | 00:01:05|
|                      | Auto-Sklearn | 0,9197   | 0,9151   | 0,8019 | 0,8548| 01:00:05|
|                      | TPOT         | 0,9213   | 0,9242   | 0,7983 | 0,8567| 00:33:16|
|                      | AutoPyTorch  | 0,9199   | 0,917    | 0,8033 | 0,855 | 01:00:09|
|                      | LightAutoML  | 0,9176   | 0,9277   | 0,7814 | 0,8482| 00:03:04|
|                      | HyperGBM     | 0,9126   | 0,9139   | 0,9126 | 0,9098| 00:01:11|
|                      | MLJar        | 0,9199   | 0,9153   | 0,802  | 0,8549| 01:00:07|



### Execução das ferramentas sem ensemble

 Os resultados a seguir são das ferramentas que tinham a opção de desativação do ensemble em suas configurações.

| Dataset              | Ferramenta   | Acurácia | Precisão | Recall | F1    | Tempo   |
|----------------------|--------------|----------|----------|--------|-------|---------|
| KronoDroid Emulator  | AutoGluon    | 0,9699   | 0,9673   | 0,965  | 0,9662| 00:05:06|
|                      | Auto-Sklearn | 0,9678   | 0,9647   | 0,9629 | 0,9638| 00:59:58|
|                      | TPOT         | 0,9525   | 0,9542   | 0,9384 | 0,9462| 00:20:58|
|                      | AutoPyTorch  | 0,9709   | 0,9671   | 0,9652 | 0,9668| 00:59:04|
|                      | MLJar        | 0,9701   | 0,9684   | 0,9665 | 0,9674| 00:59:53|
| KronoDroid Real Devices      | AutoGluon    | 0,9755   | 0,9801   | 0,9733 | 0,9767| 00:06:52|
|                      | Auto-Sklearn | 0,9752   | 0,9776   | 0,9754 | 0,9765| 00:59:58|
|                      | TPOT         | 0,9646   | 0,9668   | 0,9661 | 0,9665| 00:17:20|
|                      | AutoPyTorch  | 0,97     | 0,9711   | 0,971  | 0,9701| 00:58:22|
|                      | MLJar        | 0,9715   | 0,9745   | 0,9711 | 0,9733| 00:59:53|
| AndroCrawl           | AutoGluon    | 0,9863   | 0,9375   | 0,9307 | 0,9341| 00:05:15|
|                      | Auto-Sklearn | 0,9859   | 0,9546   | 0,908  | 0,9307| 01:00:01|
|                      | TPOT         | 0,9858   | 0,9584   | 0,9037 | 0,9302| 00:17:49|
|                      | AutoPyTorch  | 0,9871   | 0,9469   | 0,9322 | 0,939 | 00:59:46|
|                      | MLJar        | 0,9872   | 0,9471   | 0,9325 | 0,9395| 00:59:55|
| Android Permissions  | AutoGluon    | 0,6712   | 0,6868   | 0,9277 | 0,7893| 00:00:52|
|                      | Auto-Sklearn | 0,6723   | 0,676    | 0,9723 | 0,7975| 00:59:57|
|                      | TPOT         | 0,678    | 0,6911   | 0,931  | 0,7933| 00:15:47|
|                      | AutoPyTorch  | 0,6733   | 0,6721   | 0,962  | 0,7949| 00:58:52|
|                      | MLJar        | 0,673    | 0,6786   | 0,9641 | 0,7963| 00:59:50|
| DefenseDroid PRS     | AutoGluon    | 0,924    | 0,9385   | 0,9127 | 0,9254| 00:02:20|
|                      | Auto-Sklearn | 0,92     | 0,95     | 0,8922 | 0,9203| 00:59:58|
|                      | TPOT         | 0,9198   | 0,949    | 0,8928 | 0,92  | 00:16:08|
|                      | AutoPyTorch  | 0,9127   | 0,9356   | 0,908  | 0,9231| 00:59:48|
|                      | MLJar        | 0,9212   | 0,9344   | 0,9093 | 0,9218| 01:00:00|
| DREBIN-215               | AutoGluon    | 0,986    | 0,9832   | 0,9791 | 0,9812| 00:01:06|
|                      | Auto-Sklearn | 0,9836   | 0,9819   | 0,9737 | 0,9778| 00:59:59|
|                      | TPOT         | 0,9867   | 0,985    | 0,9791 | 0,982 | 00:15:28|
|                      | AutoPyTorch  | 0,9821   | 0,9862   | 0,9711 | 0,9787| 01:00:01|
|                      | MLJar        | 0,9849   | 0,9871   | 0,972  | 0,9795| 01:00:03|
| ADROIT               | AutoGluon    | 0,9178   | 0,9174   | 0,7913 | 0,8497| 00:00:31|
|                      | Auto-Sklearn | 0,9158   | 0,9177   | 0,7834 | 0,8453| 00:59:57|
|                      | TPOT         | 0,9161   | 0,9169   | 0,7854 | 0,846 | 00:15:44|
|                      | AutoPyTorch  | 0,9195   | 0,915    | 0,8016 | 0,846 | 00:00:57|
|                      | MLJar        | 0,9196   | 0,915    | 0,802  | 0,8547| 01:00:01|


### Diferença das métricas com e sem ensemble (C. ensemble - S. ensemble)

| Dataset                | Ferramenta   | Acurácia | Precisão | Recall | F1  | Tempo   |
|------------------------|--------------|----------|----------|--------|-----|---------|
| KronoDroid Emulator    | AutoGluon    | 0,26%    | 0,40%    | 0,19%  | 0,29% | 00:03:04 |
|                        | Auto-Sklearn | 0,33%    | 0,37%    | 0,36%  | 0,37% | -00:00:03 |
|                        | TPOT         | 0,74%    | -0,11%   | 1,87%  | 0,89% | 00:32:14 |
|                        | AutoPyTorch  | 0,45%    | 0,21%    | 0,19%  | 0,09% | 00:00:52 |
|                        | MLJar        | 0,30%    | 0,07%    | 0,06%  | 0,03% | 00:00:06 |
| KronoDroid Real Devices        | AutoGluon    | -0,11%   | -0,14%   | 0,24%  | 1,63% | 00:00:02 |
|                        | Auto-Sklearn | -0,35%   | -0,28%   | -0,38% | -0,33% | -00:00:03 |
|                        | TPOT         | 0,43%    | 0,53%    | 0,29%  | 0,40% | 00:16:06 |
|                        | AutoPyTorch  | 0,30%    | 0,49%    | 0,10%  | 0,12% | 00:01:37 |
|                        | MLJar        | 0,04%    | 0,05%    | 0,06%  | 0,02% | 00:00:04 |
| AndroCrawl             | AutoGluon    | 0,03%    | 0,54%    | -0,21% | 0,16% | -00:01:02 |
|                        | Auto-Sklearn | 0,16%    | -0,75%   | 2,47%  | 0,92% | -00:00:03 |
|                        | TPOT         | 0,11%    | -0,91%   | 2,09%  | 0,66% | 00:44:53 |
|                        | AutoPyTorch  | -1,41%   | 2,91%    | 3,98%  | 3,23% | 00:00:13 |
|                        | MLJar        | -1,53%   | 2,79%    | 3,92%  | 3,40% | 00:00:02 |
| Android Permissions    | AutoGluon    | 0,14%    | -0,32%   | 1,49%  | 0,32% | 00:00:36 |
|                        | Auto-Sklearn | 0,15%    | 0,28%    | -0,77% | -0,07% | -00:00:01 |
|                        | TPOT         | -0,47%   | -0,44%   | 0,23%  | -0,21% | 00:24:14 |
|                        | AutoPyTorch  | 1,05%    | 0,78%    | 0,53%  | 0,54% | 00:08:31 |
|                        | MLJar        | 0,10%    | 0,04%    | 0,08%  | 0,08% | 00:00:07 |
| DefenseDroid PRS       | AutoGluon    | 0,61%    | 0,59%    | 0,46%  | 0,53% | 00:02:27 |
|                        | Auto-Sklearn | 0,15%    | -1,52%   | 1,77%  | 0,19% | 00:00:06 |
|                        | TPOT         | 0,30%    | -0,36%   | 0,82%  | 0,27% | 00:39:19 |
|                        | AutoPyTorch  | 0,99%    | 0,07%    | 0,20%  | 0,00% | 00:03:16 |
|                        | MLJar        | 0,08%    | 0,07%    | 0,06%  | 0,11% | 00:00:05 |
| DREBIN-215                 | AutoGluon    | 0,02%    | 0,14%    | -0,09% | 0,02% | 00:00:07 |
|                        | Auto-Sklearn | 0,14%    | 0,53%    | -0,15% | 0,19% | 00:00:07 |
|                        | TPOT         | -0,50%   | 0,14%    | 0,50%  | -0,27% | 00:28:56 |
|                        | AutoPyTorch  | 0,31%    | 0,14%    | 0,16%  | 0,14% | 00:00:09 |
|                        | MLJar        | 0,03%    | 0,03%    | 0,03%  | 0,03% | 00:00:04 |
| ADROIT                 | AutoGluon    | -0,42%   | -2,10%   | 0,79%  | -0,47% | 00:00:34 |
|                        | Auto-Sklearn | 0,39%    | -0,26%   | 1,85%  | 0,95% | 00:00:08 |
|                        | TPOT         | 0,52%    | 0,73%    | 1,29%  | 1,07% | 00:17:32 |
|                        | AutoPyTorch  | 0,04%    | 0,20%    | 0,17%  | 0,90% | 00:59:12 |
|                        | MLJar        | 0,03%    | 0,03%    | 0,00%  | 0,02% | 00:00:06 |


### Resultados da execução do AutoGluon com e sem otimização

| Dataset                    | Acurácia | Precisão | Recall | F1 | Tempo | Acurácia | Precisão | Recall | F1 | Tempo |
|----------------------------|----------------|----------------|--------------|----------|--------------|----------------|----------------|--------------|----------|--------------|
| **Com Otimização**         |                |                |              |          |              | **Sem Otimização** |                |              |          |              |
| ADROIT                     | 0,9179         | 0,9176         | 0,9179       | 0,9162   | 00:04:04     | 0,9136         | 0,8964         | 0,7992       | 0,845    | 00:01:05     |
| DREBIN-215                  | 0,9853         | 0,9853         | 0,9853       | 0,9853   | 00:13:23     | 0,9862         | 0,9846         | 0,9782       | 0,9814   | 00:01:13     |
| KronoDroid Real Devices     | 0,9761         | 0,9761         | 0,9761       | 0,9761   | 01:12:52     | 0,9744         | 0,9787         | 0,9757       | 0,993    | 00:06:54     |
| AndroCrawl                 | 0,9876         | 0,9875         | 0,9876       | 0,9875   | 00:03:54     | 0,9866         | 0,9429         | 0,9286       | 0,9357   | 00:04:13     |
| Android Permissions        | 0,6758         | 0,6583         | 0,6758       | 0,5866   | 00:03:49     | 0,6726         | 0,6836         | 0,9426       | 0,7925   | 00:01:28     |
| KronoDroid Emulator        | 0,9716         | 0,9716         | 0,9716       | 0,9716   | 00:44:06     | 0,9725         | 0,9713         | 0,9669       | 0,9691   | 00:08:10     |
| DefenseDroid PRS           | 0,9266         | 0,9270         | 0,9266       | 0,9266   | 00:07:46     | 0,9301         | 0,9444         | 0,9173       | 0,9307   | 00:04:47     |




## **Referências:**

1. Arrieta, A. B., Díaz-Rodríguez, N., Del Ser, J., Bennetot, A., Tabik, S., Barbado, A., ... & Benjamins, R. (2020). Explainable Artificial Intelligence (XAI): Concepts, taxonomies, opportunities and challenges toward responsible AI. *Information fusion*, 58, 82-115. [Link](https://doi.org/10.1016/j.inffus.2019.12.012)

2. Love, P. E., Fang, W., Matthews, J., Porter, S., Luo, H., & Ding, L. (2023). Explainable artificial intelligence (XAI): Precepts, models, and opportunities for research in construction. *Advanced Engineering Informatics*, 57, 102024. [Link](https://doi.org/10.1016/j.aei.2021.102024)

3. Mi, J. X., Li, A. D., & Zhou, L. F. (2020). Review study of interpretation methods for future interpretable machine learning. *IEEE Access*, 8, 191969-191985. [Link](https://doi.org/10.1109/ACCESS.2020.3033626)

4. Carvalho, D. V., Pereira, E. M., & Cardoso, J. S. (2019). Machine learning interpretability: A survey on methods and metrics. *Electronics*, 8(8), 832. [Link](https://doi.org/10.3390/electronics8080832)

5. Brännström, M. (2023). Transparency of Complex Systems: The Semantic Transparency Framework. [Link](https://www.semanticscholar.org/paper/Transparency-of-Complex-Systems%3A-The-Semantic-Br%C3%A4nnstr%C3%B6m/efb398a4e1b5716729de562a47fae081d517943c)
