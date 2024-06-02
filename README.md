# Evolução de Correlação com Python

Este texto é fruto da parceria entre a DIO e o Santander no evento "Santander 2024 — Fundamentos de IA para Devs". Como todos sabem, o Santander é um banco, e a DIO é uma escola de programação. Pensei em juntar essas duas forças para criar um breve artigo sobre a evolução da correlação entre ativos. Já publiquei um trabalho no Medium explicando detalhadamente o que é correlação e sua fundamentação matemática. O link para esse artigo estará disponível ao final deste texto.

---

# Principais prompts utilizados no ChatGPT. 

> Selecione as funções mais conhecidas para janelamento de série temporais.

> Selecione a função mais usada para calculo de correlação.

---

Link Artigo Dio

Link Artigo sobre Correlação medium

# Código 

Para iniciar precisamos importar algumas bibliotecas, então, vamos:

```
#importando bibliotecas
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import yfinance as yf
```

Escolher os ativos
> BDR da Apple

> ETF do Ibovespa
```
#tinkers dos ativos
tinkers  = ['BOVA11.SA','AAPL34.SA']
```

Seleção da janela de avaliação

```
# Janela de avaliação
inicio = "2018-01-02"
final = "2024-05-28"
```

```
#Download dos valores de fechamento ajustado dos ativos
dados = yf.download(tinkers, start= inicio, end=final )['Adj Close']
```

```
#Visualizando a base de dados
carteira=pd.DataFrame(dados)
carteira.head()
```

O valor de 252 é utilizado porque o sistema bancário adota um calendário de 252 dias úteis. A função rolling "desliza" a janela de tempo nesses 252 dias, enquanto a função corr calcula a correlação entre os dois ativos. A função plot() tem como único objetivo apresentar o gráfico resultante.



```
carteira['AAPL34.SA'].rolling(252).corr(carteira['BOVA11.SA']).plot()
```

Resultado


<div align="center">
<img src="https://github.com/andersoncsalles/Evolucao-correlacao/blob/main/imagens/download.png" width="700" height="500">
</div>
