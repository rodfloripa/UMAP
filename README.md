<p align="justify"><h1><b>UMAP do jeito certo usando MNIST</b></h1></p>

<p align="justify">
A transição do t-SNE para o <b>UMAP (Uniform Manifold Approximation and Projection)</b>, acompanhada de uma calibração rigorosa, é fundamental para análises de alta fidelidade. A vantagem da calibração é crucial para obter uma visualização de alta qualidade, especialmente em conjuntos de dados complexos como os dígitos do MNIST.
</p>

<hr>

<p align="justify"><h2><b>1. O Processo de Calibração e Otimização</b></h2></p>

<p align="justify"><h3><b>Otimização da Separação de Clusters</b></h3></p>
<p align="justify">
O UMAP possui parâmetros fundamentais como <b>n_neighbors</b> (que equilibra o foco entre estrutura local e global) e <b>min_dist</b> (que controla o quão próximos os pontos podem ficar). Ao iterarmos sobre essas combinações e avaliarmos cada resultado com o <b>silhouette_score</b>, buscamos a configuração que maximiza a coesão interna e a separação entre diferentes dígitos. Isso resulta na melhor distinção possível no gráfico 2D.
</p>



<p align="justify"><h3><b>Representação Mais Fiel e Estrutura Global</b></h3></p>
<p align="justify">
Diferente do t-SNE, o UMAP preserva melhor a topologia global dos dados. A calibração nos permite encontrar um equilíbrio ideal: ela garante que a distância entre os clusters no gráfico não seja arbitrária, mas sim uma representação proporcional à dissimilaridade real no espaço original de alta dimensão.
</p>

<p align="justify"><h3><b>Minimização de Clusters Fantasmas</b></h3></p>
<p align="justify">
Com uma calibração inadequada, há um risco de dividir clusters naturalmente contínuos em subgrupos artificiais (os "clusters fantasmas"). Ao otimizar os parâmetros, evitamos essas distorções e garantimos que os agrupamentos visíveis reflitam a estrutura real dos dados, superando limitações de escala e densidade.
</p>

<hr>

<p align="justify"><h2><b>2. Por que a calibração ainda é necessária?</b></h2></p>

<p align="justify">
Mesmo sendo mais robusto que o t-SNE, o analista deve utilizar a calibração para mitigar pontos que exigem interpretação cuidadosa:
</p>

<p align="justify">
<b>A. Validação da Topologia:</b> O UMAP assume que os dados estão em uma variedade (manifold) uniforme. Ajustar o número de vizinhos garante que essa premissa não seja violada por ruído, o que impediria a formação de clusters coesos.
</p>

<p align="justify">
<b>B. Consistência Multidimensional:</b> O uso de Grid Search assegura que a visualização final seja uma projeção estatisticamente validada pela métrica de silhueta, conferindo rigor científico ao trabalho de Ciência de Dados.
</p>



<hr>

<p align="justify"><h2><b>3. Conclusão</b></h2></p>

<p align="justify">
Em resumo, a calibração permite ajustar o UMAP para extrair a melhor interpretabilidade possível. Isso supera as limitações clássicas do t-SNE, entregando um mapa onde a geometria 2D comunica fielmente a relação técnica entre as classes de dados.

<img title="a title" alt="Alt text" src="https://raw.githubusercontent.com/rodfloripa/UMAP/main/download%20(2).png">
</p>

<p align="justify">
<i><b>Nota:</b> A utilização de <b>init='pca'</b> ou <b>init='spectral'</b>, aliada à nossa calibração, fornece um ponto de partida globalmente coerente que acelera a convergência para a estrutura correta.</i>
</p>
