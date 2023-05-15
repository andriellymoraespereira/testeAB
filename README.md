<h2>✅ Project Done!</h2>

<span style="color: yellow;"><strong>Disclaimer:</strong> O projeto a seguir tem como base um projeto da Empresa <a href="https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing">Kaggle</a>.</span>

Para obter uma visão mais abrangente e detalhada da análise exploratória de dados, consulte o seguinte notebook Jupyter.

[![EXPLORATORY DATA ANALYSIS - Jupyter](https://img.shields.io/badge/Exploratory%20Data%20Analysis-Jupyter-orange?style=for-the-badge&logo=Jupyter)](https://github.com/andriellymoraespereira/testeAB)

# Teste A/B de marketing

<img src="https://github.com/andriellymoraespereira/testeAB/img/projeto.png" alt="">

# 1.0. About
Neste projeto, uma empresa de marketing deseja executar campanhas de sucesso, mas o mercado é complexo e várias opções podem funcionar. Então, normalmente eles realizam testes A/B, que é um processo de experimentação aleatória em que duas ou mais versões de uma variável (página da web, elemento de página, banner, etc.) são mostradas para diferentes segmentos de pessoas ao mesmo tempo para determinar qual versão deixa o máximo impacto e impulsiona as métricas de negócios.

A empresa está interessadas em responder a duas perguntas:

A campanha teria sucesso?
Se a campanha foi bem-sucedida, quanto desse sucesso pode ser atribuído aos anúncios?
Com a segunda pergunta em mente, normalmente fazemos um teste A/B. A maioria das pessoas será exposta a anúncios (o grupo experimental). E uma pequena parte das pessoas (o grupo de controle) veria um anúncio de serviço público (PSA) (ou nada) no tamanho exato e no local em que o anúncio normalmente estaria.

A ideia do conjunto de dados é analisar os grupos, descobrir se os anúncios foram bem-sucedidos, quanto a empresa pode ganhar com os anúncios e se a diferença entre os grupos é estatisticamente significativa. 



<p align="center">
 <a href="#About">About</a> •
 <a href="#O Que São Testes A/B?">O Que São Testes A/B?</a> •
 <a href="#Fonte de dados">Fonte de dados</a> • 
 <a href="#Como Analisar Testes A/B?">Como Analisar Testes A/B?</a> •
 <a href="#conclusions">Conclusions</a> •  
 <a href="#technologies">Technologies</a>  
</p>


# 2.0. O Que São Testes A/B?

As análises de Testes A/B são comumente realizadas por Analistas e Cientistas de dados.

​
Para este projeto vamos compreender os resultados de um Teste A/B executado por uma Campanha de marketing. Sua meta é ajudar a empresa a descobrir se os anúncios foram bem-sucedidos, quanto a empresa pode ganhar com os anúncios e se a diferença entre os grupos é estatisticamente significativa..
​
Conjunto de dados básico sobre uma campanha de marketing com um teste A/B.

# 3.0.  Fonte de dados

**Teste A/B de marketing**: https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing

## 3.1 Conjunto de Dados 
| Columns              | Description |
| ---------------------| --------- |
| index	               | Índice de linha      |  
| id_usuario           | ID do usuário (único)      |  
| grupo                | "ad" a pessoa viu o anúncio ou "psa" viu apenas o anúncio de serviço público|  
| grupo                | "psa" viu apenas o anúncio de serviço público     |  
| converte	           | Se uma pessoa comprou o produto, então é Verdadeiro, caso contrário é Falso  |
| total_anuncios       | Quantidade de anúncios vistos por pessoa       |  
| dia	               | Dia em que a pessoa viu a maior quantidade de anúncios    |
| hora                 | Hora do dia em que a pessoa viu a maior quantidade de anúncios     |


# 4.0. Como Analisar Testes A/B?

Em geral, realizamos esses 5 passos para analisar um Teste A/B:

1. Configuramos o experimento.

2. Executamos o teste de hipóteses e registramos a taxa de sucesso de cada grupo.

3. Criamos o Plot da distribuição da diferença entre as duas amostras.

4. Calculamos o poder estatístico.

5. Avaliamos como o tamanho das amostras afeta os Testes A/B.

## 4.1. Tarefa 1 - Configurando o Experimento

Se a campanha foi bem-sucedida, quanto desse sucesso pode ser atribuído aos anúncios?

Variante psa: viu apenas o anúncio de serviço público

Variante ad: viu o anúncio

Observe que, devido ao registro de data e hora associado a cada evento, você pode tecnicamente executar um teste de hipótese continuamente à medida que cada evento é observado.

No entanto, a questão difícil é saber quando parar assim que uma variante for considerada significativamente melhor do que outra ou isso precisa acontecer de forma consistente por um determinado período de tempo? Quanto tempo até você decidir que nenhuma variante é melhor que a outra? Converse com a área de negócio para definir a melhor abordagem para o teste e apresentaremos algumas dicas durante este trabalho.

Essas questões são as partes mais difíceis associadas aos Testes A/B e a análise em geral.

Por enquanto, considere que você precisa tomar uma decisão apenas com base nos dados fornecidos. Se você quiser assumir que a variante psa é melhor, a menos que a nova variante prove ser definitivamente melhor em uma taxa de erro Tipo I de 5%, quais deveriam ser suas hipóteses nula e alternativa?

Você pode definir suas hipóteses em termos de palavras ou em notação como  P𝑝𝑠𝑎 e  P𝑎𝑑, que são as probabilidades de conversão para as variantes nova e antiga.

H0: Pad - Ppsa = 0
H1: Pad - Ppsa > 0

H0 nos diz que a diferença de probabilidade dos dois grupos é igual a zero.

H1 nos diz que a diferença de probabilidade dos dois grupos é maior do que zero.

### 4.1.1 Criação do Baseline

Vamos criar um baseline (linha base) da taxa de conversão antes de executar o teste de hipótese. Assim, saberemos a taxa de conversão base e o aumento desejado em compras que gostaríamos de testar.

**psa** será o grupo de controle
**ad**  será o grupo de teste

| Variantes   | Conversão  | Taxa  | Total   |
| ----------  | ---------  | ----- | -----   |    
| psa         |     55     |  3490 | 0.016   |
| ad          |   1963     | 77418 | 0.025   |

Taxa de conversão da linha de base (Baseline conversion rate)
Igual a  𝑝 no contexto de uma distribuição binomial e  𝑝 é a probabilidade de sucesso.
Ou seja, a Taxa de psa é ígual a taxa de e conversão base, aproximadamente 0,016.

Efeito mínimo detectável (Minimum Detectable Effect).
o efeito mínimo detectável = Taxa(ad) - Taxa(psa)
o efeito mínimo detectável é igual a 0.009597



## 4.2. Tarefa 2 - Execução do Teste de Hipóteses

Executamos o teste de hipóteses e registramos a taxa de sucesso de cada grupo.

Poder estatístico ou sensibilidade.

Igual a 1 -  𝛽.
 

Normalmente 80% é usado para a maioria das análises. É a probabilidade de rejeitar a hipótese nula quando a hipótese nula é de fato falsa.

Parâmetros que usaremos para executar o teste:

1- Alfa (Nível de significância)  𝛼: normalmente 5%; probabilidade de rejeitar a hipótese nula quando a hipótese nula for verdadeira

2- Beta  𝛽: probabilidade de aceitar a hipótese nula quando a hipótese nula é realmente falsa.

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t.png" alt="">
 
## 4.3. Tarefa 3 - Plot da Distribuição
Criamos o Plot da distribuição da diferença entre as duas amostras e comparamos os resultados.
Podemos comparar os dois grupos traçando a distribuição do grupo de controle e calculando a  probabilidade de obter o resultado de nosso grupo de teste.


<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t3.png" alt="">

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t4.png" alt="">

Podemos ver que o grupo de teste converteu mais usuários do que o grupo de controle. Também podemos ver que o pico dos resultados do grupo de teste é inferior ao do grupo de controle.

Mas como interpretamos a diferença no pico da probabilidade?

Devemos nos concentrar, em vez disso, na taxa de conversão para que tenhamos uma comparação de termos equivalentes. Para calcular isso, precisamos padronizar os dados e comparar a probabilidade de sucesso, p, para cada grupo

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t5.png" alt="">

igual à diferença média entre o grupo de controle e teste.

Variância da Soma

Lembre-se de que a hipótese nula afirma que a diferença de probabilidade entre os dois grupos é zero. Portanto, a média para essa distribuição normal será zero. A outra propriedade de que precisaremos para a distribuição normal é o desvio padrão ou a variância.

Observação: a variância é o desvio padrão ao quadrado. A variância da diferença dependerá das variâncias da probabilidade para ambos os grupos.



### 4.3.1. Plot da Distribuição de Probabilidade

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t6.png" alt="">

Visualmente, o gráfico para as hipóteses nula e alternativa é muito semelhante aos outros gráficos acima. Felizmente, as duas curvas têm formato idêntico, portanto, podemos apenas comparar a distância entre as médias das duas distribuições. Podemos ver que a curva de hipótese alternativa sugere que o grupo de teste tem uma taxa de conversão maior do que o grupo de controle. Este gráfico também pode ser usado para determinar diretamente o poder estatístico.


## 4.4. Tarefa 4 - Calculando o Poder Estatístico¶
Poder Estatístico e Nível de Significância

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t6.png" alt="">

A área sombreada em verde representa o poder estatístico e o valor calculado para o poder também é exibido no gráfico. As linhas tracejadas em cinza no gráfico acima representam o intervalo de confiança (95% para o gráfico acima) para a hipótese nula. O poder estatístico é calculado encontrando a área sob a distribuição de hipótese alternativa e fora do intervalo de confiança da hipótese nula.

Depois de executar nosso experimento, obtemos uma taxa de conversão resultante para ambos os grupos. Se calcularmos a diferença entre as taxas de conversão, acabamos com um resultado, a diferença ou o efeito de uma pessoa assistir ao anúncio. Nossa tarefa é determinar de qual população esse resultado veio, a hipótese nula ou a hipótese alternativa.

A área sob a curva da hipótese alternativa é igual a 1. Se os anúncios foram bem-sucedidos, o poder é a probabilidade de aceitarmos a hipótese alternativa e rejeitarmos a hipótese nula e é igual à área sombreada em verde (verdadeiro positivo). A área oposta sob a curva alternativa é a probabilidade de não rejeitarmos a hipótese nula e rejeitarmos a hipótese alternativa (falso negativo). Isso é conhecido como beta no teste A/B ou teste de hipótese e é mostrado abaixo.

Se a hipótese nula for verdadeira e realmente não houver diferença entre os grupos de controle e teste, o nível de significância é a probabilidade de rejeitarmos a hipótese nula e aceitarmos a hipótese alternativa (falso positivo). Um falso positivo é quando concluímos erroneamente que os anúncios foram bem-sucedidos. Este valor é baixo porque queremos limitar essa probabilidade.

Muitas vezes, um problema será fornecido com um nível de confiança desejado em vez do nível de significância. Um nível de confiança típico de 95% para um teste A / B corresponde a um nível de significância de 0,05.

Os experimentos são normalmente configurados para uma potência mínima desejada de 80%. Se os anúncios foram bem-sucedidos, queremos que nosso experimento mostre que há pelo menos 80% de probabilidade de que esse seja o caso. Sabemos que, se aumentarmos o tamanho da amostra para cada grupo, diminuiremos a variância combinada para nossa hipótese nula e alternativa. Isso tornará nossas distribuições muito mais estreitas e pode aumentar o poder estatístico. Vamos dar uma olhada em como o tamanho da amostra afetará diretamente nossos resultados.

## 4.5. Tarefa 5 - Influência do Tamanho da Amostra no Teste A/B
Nossas curvas para a hipótese nula e alternativa tornaram-se mais estreitas e mais da área sob a curva alternativa está localizada à direita da linha tracejada cinza. O resultado para potência é maior que 0,80 e atende a nossa referência de potência estatística. Agora podemos dizer que nossos resultados são estatisticamente significativos.

O próximo problema que devemos encontrar é determinar o tamanho mínimo da amostra de que precisaremos para o experimento. E isso é útil saber porque está diretamente relacionado à rapidez com que podemos concluir os experimentos e fornecer resultados estatisticamente significativos para a área de negócio.

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t7.png" alt="">

<img src="https://github.com/andriellymoraespereira/testeAB/imgagens/t8.png" alt="">

O tamanho mínimo necessário para a amostra.

<img src="https://github.com/andriellymoraespereira/testeAB/t9.png" alt="">

# 5.0. Conclusions

O poder calculado para este tamanho de amostra foi de aproximadamente 0,80. Portanto, para afirmar que assistir ao anúncio realmente aumentou a taxa de conversão precisamos de pelos menos 3432 amostras.


# 6.0. Technologies

The following tools, libraries and IDE were used in building the project:

- [Python](https://www.python.org/)
- [Jupyter Notebook](https://jupyter.org/)
- [Pandas](https://pandas.pydata.org/)
- [Numpy](https://numpy.org/)
- [Maptplot Lib](https://matplotlib.org/)
- [scipy.stats](https://docs.scipy.org/doc/scipy/reference/stats.html)
- [Requests API](https://requests.readthedocs.io/en/latest/)
- [Visual Studio Code](https://code.visualstudio.com/)

# 8.0. Author

[@andriellymoraespereira](https://www.linkedin.com/in/andriellymoraespereira/)
