<p align="justify"><h1><b>UMAP do jeito certo usando MNIST</b></h1></p>


<p align="justify"><h1>Análise de Redução de Dimensionalidade com UMAP no MNIST</h1></p>

<p align="justify">
Este relatório apresenta uma análise detalhada do comportamento do algoritmo <b>UMAP</b> aplicado ao dataset MNIST (784 dimensões), com foco na relação entre fidelidade global (Shepard Diagram) e preservação da estrutura local (Trustworthiness - TW e Continuity - CT). O objetivo central foi identificar os limites estruturais da projeção em 2D e entender os trade-offs envolvidos na escolha dos hiperparâmetros.
</p>



<p align="justify"><h2>1. Configuração Experimental</h2></p>

<p align="justify">
A configuração que atingiu o melhor desempenho em termos de correlação global (Shepard) foi:
</p>

```python
umap.UMAP(
    n_neighbors=200,
    min_dist=1.0,
    spread=1.5,
    metric='cosine',
    init='pca'
)
````



<p align="justify"><h2>2. Limite Estrutural do Shepard Diagram</h2></p>

```python
shepard_score = 0.508
```

<p align="justify">
Mesmo com grid search extensivo, esse valor representa um teto estrutural (~51% de correlação global).
</p>



<p align="justify"><h2>3. Trade-off: Global vs Local</h2></p>

```python
# Antes
TW = 0.880
CT = 0.911

# Melhor Shepard
TW = 0.861
CT = 0.869
```



<p align="justify"><h2>4. Estrutura dos Clusters</h2></p>

<p align="justify">
A sobreposição observada reflete propriedades reais do dataset. Abaixo, uma tabela resumindo os principais agrupamentos estruturais:
</p>

<table>
<thead>
<tr>
<th>Grupo de Dígitos</th>
<th>Característica Estrutural</th>
</tr>
</thead>
<tbody>
<tr>
<td>[4, 9, 7]</td>
<td>Traço vertical + curva no topo</td>
</tr>
<tr>
<td>[2, 5, 3]</td>
<td>Curvas abertas</td>
</tr>
<tr>
<td>[8, 3, 5]</td>
<td>Duas “barrigas” (loops parciais)</td>
</tr>
<tr>
<td>[0, 6, 8]</td>
<td>Loops fechados</td>
</tr>
<tr>
<td>[1, 7, 9]</td>
<td>Retas / traços inclinados</td>
</tr>
</tbody>
</table>

<p align="justify">
Esses agrupamentos explicam diretamente a sobreposição dos convex hulls no espaço 2D. O modelo está capturando ambiguidades reais da escrita manual.
</p>



<p align="justify"><h2>5. Impacto do <code>spread</code></h2></p>

<ul>
<li><b>1.0:</b> melhor estrutura local</li>
<li><b>1.5:</b> melhor distribuição global</li>
</ul>



<p align="justify"><h2>6. Convex Hull</h2></p>

```python
from scipy.spatial import ConvexHull
hull = ConvexHull(points)
```



<p align="justify"><h2>7. Aplicação Prática</h2></p>

```python
# Visual (cliente)
umap.UMAP(n_neighbors=30, min_dist=0.5, spread=1.0)
```





<hr>

<p align="justify"><h2><b>8. Conclusão</b></h2></p>

```python
n_neighbors=200
min_dist=1.0
spread=1.5
```

<p align="justify">
Em resumo, a calibração permite ajustar o UMAP para extrair a melhor interpretabilidade possível. Isso supera as limitações clássicas do t-SNE, entregando um mapa onde a geometria 2D comunica fielmente a relação técnica entre as classes de dados.

</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/rodfloripa/UMAP/main/umap.png ">
</p>
<p align="center">
O gráfico não está “ruim” — ele está <b>correto</b>. A sobreposição é a verdade do espaço original.
</p>
