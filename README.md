# Análise de dados e IA Generativa — Alura + FIAP & Santander (2026)

Mini-curso de algoritmos de clusterização voltado para profissionais de TI do Santander Brasil.

**Instrutor:** [Rafael Monteiro](https://rafael-a-monteiro-math.github.io/) (ou [Linkedin](https://www.linkedin.com/in/rafael-a-monteiro-appliedmath/))

---

## Lab — Clusterização e a Maldição da Dimensionalidade

Este laboratório aborda o tema de **aprendizado não supervisionado**: ao contrário de problemas de regressão ou classificação, aqui não existem rótulos — o objetivo é descobrir padrões e estruturas nos próprios dados.

### Conteúdo

#### 1. Introdução à Clusterização
Motivação e intuição por trás de algoritmos que agrupam pontos por similaridade, identificando regiões de acumulação em um conjunto de dados.

#### 2. K-Means
Talvez o algoritmo de clusterização mais famoso. O funcionamento consiste em:
1. inicializar `k` centróides aleatoriamente;
2. associar cada ponto ao centróide mais próximo;
3. recalcular cada centróide como a média de seu grupo;
4. repetir até convergência.

Subtópicos abordados:
- **Método do cotovelo** (*elbow method*): técnica para escolher o número adequado de clusters com base na inércia do modelo.
- **Limitações do K-Means**: o algoritmo pressupõe clusters esféricos e compactos, falhando em dados com formatos arbitrários (ex.: `make_moons`).
- **Problema de inicialização**: más inicializações podem impedir a convergência. O hiperparâmetro `n_init` controla o número de tentativas aleatórias.
- **K-Means++**: estratégia de inicialização (proposta em 2006) que distribui os centróides o mais distante possível uns dos outros, melhorando a convergência.
- **Mini-batch K-Means**: variante que usa subamostras aleatórias a cada iteração, reduzindo drasticamente o tempo de processamento (até ~14× mais rápido em experimentos do lab) com pequena perda de qualidade.

#### 3. DBSCAN
*Density-Based Spatial Clustering of Applications with Noise* — algoritmo baseado em densidade com duas grandes vantagens sobre o K-Means:
- **Não exige** a definição prévia do número de clusters.
- **Detecta outliers** (pontos de ruído), tornando-o útil para **detecção de anomalias**.

Hiperparâmetros principais: `eps` (raio de vizinhança) e `min_samples` (número mínimo de pontos para definir um *core point*).

#### 4. Gaussian Mixture Model (GMM)
Modelo probabilístico que assume que os dados foram gerados por uma mistura de distribuições gaussianas com diferentes médias e matrizes de covariância. Permite capturar clusters elípticos ou alongados que o K-Means não consegue representar bem.
- **Seleção de clusters**: uso dos critérios **BIC** (*Bayesian Information Criterion*) e **AIC** (*Akaike Information Criterion*) no lugar da inércia.
- **Detecção de anomalias**: pontos em regiões de baixa densidade de probabilidade são candidatos a anomalias; um limiar baseado em percentis permite classificá-los automaticamente.

#### 5. Memória e Escalabilidade
Discussão sobre a complexidade $O(N^2)$ no cálculo de distâncias entre $N$ pontos e como isso limita a aplicabilidade de certos algoritmos em grandes volumes de dados. Motivação para métodos como o Mini-batch K-Means e o BIRCH.

#### 6. BIRCH
*Balanced Iterative Reducing and Clustering using Hierarchies* — algoritmo de clusterização hierárquica com baixo consumo de memória e suporte a processamento **online** (sem necessidade de carregar todos os dados de uma vez). Funciona bem para bases de dados muito grandes, embora seu desempenho caia em dimensões muito altas.

#### 7. Aplicação: Segmentação de Imagens
Uso do K-Means e Mini-batch K-Means para comprimir imagens RGB, agrupando pixels em `k` cores representativas. O experimento evidencia a diferença de velocidade entre os dois algoritmos.

#### 9. Maldição da Dimensionalidade (*Curse of Dimensionality*)
À medida que a dimensão cresce, a fração do volume de um hipercubo próxima à sua superfície tende a 100%, tornando o "interior" cada vez mais esparso. Isso quebra intuições geométricas baseadas em dimensões baixas e afeta diretamente a qualidade dos algoritmos de clusterização baseados em distância.

#### 10. Comentários Finais
Não existe um algoritmo de clusterização universalmente melhor. A escolha depende do formato dos dados, da escala, da presença de ruído, da dimensionalidade e do objetivo de negócio. Pré-processamento, avaliação crítica das métricas e conhecimento de domínio são tão importantes quanto a escolha do algoritmo.

---

### Ferramentas utilizadas

- **Python**: NumPy, Matplotlib
- **Scikit-learn**: `KMeans`, `MiniBatchKMeans`, `DBSCAN`, `GaussianMixture`, `Birch`, `make_blobs`, `make_moons`, `make_circles`

### Referências
- Géron, A. *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow*, 3ª ed. — capítulos 9 e 3.
- [Scikit-learn: Comparing clustering algorithms](https://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_comparison.html)
- [Curso Alura: Clusterização de dados — segmentação de clientes](https://cursos.alura.com.br/course/clusterizacao-dados-segmentacao-clientes)
