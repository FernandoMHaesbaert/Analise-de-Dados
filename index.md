## Bem vindo ao site do Prof. Dr. Fernando Machado Haesbaert
Curso de Agronomia - UFT Campus de Gurupi-TO



```markdown
---
title: "Normalização x Padronização de dados"
author: "Prof. Dr. Fernando Machado Haesbaert"
date: "25/06/2021"
output:
  pdf_document: default
  html_document: default
e-mail: fernandomh@uft.edu.br
---
  A modificação da estrutura dos dados é uma etapa muito importante em difeços tipos de processos de análise de dados, muitos algoritmos de Machine Learning, por exemplo, necessitam que os dados de entrada sejam valores padronizados. 
Devido as diversas formas possíveis de se modificar a estrutura dos dados sugem terminologia diferentes, como: "Transformação de dados", "Padronização de dados", "Normalização de dados", etc.
O objetivo dessas tecnicas quase sempre é o mesmo: transformar todas as variáveis na mesma ordem de grandeza, ou seja, trazer os valores para a mesma escala de valores. No entanto, dependendo da técnica utilizada, algumas características precisam ser observadas, tais como, o intervalo dos valores resultantes e se o padrão de simetria/assimetria dos dados originais se mante ou não.

A padronização (por meio do Score Z, da distribuição Normal Padrão) obtemos como resultado dados centralizados em uma média igual a 0 e desvio padrão igual a 1. Já a normalização de dados, o nosso resultado se encontra em um intevalo de 0 a 1, já se tivermos números negativos o intervalo será de -1 a 1.


## Dados Normalmente distribuídos
```{r}
x <- rnorm(1000, 100, 10) # 1000 valores, com média 100 e desvio padrão 10.
plot(x)
hist(x)
moments::skewness(x)
```

### Normalização de dados - devolve valores entre 0 e 1.
```{r}
normalizacao = (x - min(x)) / (max(x) - min(x))
head(normalizacao)
plot(normalizacao)
hist(normalizacao)
moments::skewness(normalizacao)
```
Observe que o coeficiente de assimetria se mantem.
  
### Padronização de dados -> média = 0 e desvio padrão = 1 (Normal Padrão).
```{r}
padronizacao = (x - mean(x))/sd(x)
head(padronizacao)
plot(padronizacao)
hist(padronizacao)
moments::skewness(padronizacao)
```
Observe que o coeficiente de assimetria se mantem.
  
Usando a função `scale` para obter os valores padronizados 
```{r}
score_z = scale(x, center = T)
head(score_z)
hist(score_z)
moments::skewness(score_z)
```
Observe que o coeficiente de assimetria se mantem.
  
## Dados Assimetricamente distribuídos
```{r}
y <- rchisq(1000,10) #1000 valores da distribuição Qui-Quadrado. 
hist(y)
moments::skewness(y)
```

### Normalização de dados - devolve valores entre 0 e 1.
```{r}
normalizacao = (y - min(y)) / (max(y) - min(y))
hist(normalizacao)
moments::skewness(normalizacao)
```
Observe que o coeficiente de assimetria NÃO se mantem.
  
### Padronização de dados -> média = 0 e desvio padrão = 1 (Normal Padrão).
```{r}
padronizacao = (y - mean(y))/sd(y)
hist(padronizacao)
moments::skewness(padronizacao)
```
Observe que o coeficiente de assimetria se mantem.
  
## Dados Negativos e Positivos no mesmo banco de dados
```{r}
w <- rnorm(1000,-2, 10) #1000 valores normalmente distribuídos. 
hist(w)
moments::skewness(w)
```
### Normalização de dados
Neste caso, com valores negativos, a normalização devolve valores entre -1 e 1.
```{r}
# Função para valores negativos
normalizacao_neg <- ((w - ((max(w) + min(w)) / 2)) / ((max(w) - min(w)) / 2))
hist(normalizacao_neg)
moments::skewness(normalizacao_neg)
```

### Padronização de dados -> média = 0 e desvio padrão = 1 (Normal Padrão).
```{r}
padronizacao = (w - mean(w))/sd(w)
hist(padronizacao)
moments::skewness(padronizacao)
```
Sendo os dados simétricos, o coeficiente de assimetria se mantem.
  
## Transformação Raiz Quadrada
```{r}
z <- rchisq(1000,10)
hist(z)
moments::skewness(z)
norm_log <- log(z)
hist(norm_log)
moments::skewness(norm_log)
```
Observe que alé do coeficiente de assimetria NÃO se manter, ele inverte o comportamento.


```
