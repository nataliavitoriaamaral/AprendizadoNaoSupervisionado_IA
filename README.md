# Análise Comparativa de Agrupamentos Não Supervisionados: K-Means e Single Linkage 

## Sobre o Projeto
Este projeto realiza uma avaliação comparativa entre dois algoritmos clássicos de aprendizado não supervisionado: **K-Means** e **Single Linkage** (Agglomerative Clustering). O objetivo principal é demonstrar que o sucesso destes algoritmos depende da geometria dos dados. A análise também investiga a confiabilidade do **Índice Rand** como métrica de validação externa para esses cenários.

A execução foi dividida em duas etapas para garantir uma avaliação mais justa:
1. Teste com o número de clusters ($K$) variável dentro de um intervalo lógico.
2. Testes com o valor de $K$ fixado na quantidade ideal e real de cada base de dados.

---

## Algoritmos Avaliados

### K-Means
O K-Means trabalha tentando agrupar os dados ao redor de um ponto central. 
* **Ponto Forte:** Excelente para delimitar grupos que já são naturalmente circulares e bem espaçados (como visto no dataset D31).
* **Limitação:** Por esperar sempre encontrar grupos redondos e bem concentrados, ele falha ao se deparar com dados que formam desenhos alongados, em anel ou irregulares, fazendo cortes retos e artificiais na figura.

### Single Linkage (Agrupamento Hierárquico)
O Single Linkage funciona ligando os pontos que estão mais próximos uns dos outros.
* **Ponto Forte:** Ajuda a capturar formatos irregulares que o K-Means não consegue.
* **Limitação:** Se houver pontos soltos formando uma "ponte" fina entre dois grupos que deveriam estar separados, o algoritmo se confunde e agrupa em um único grande grupo.

---

## Métrica de Avaliação: Índice Rand
O modelo foi avaliado utilizando o Índice Rand, cuja fórmula é:

$$Rand = \frac{(A+D)}{(A+B+C+D)}$$ 

Embora seus valores variem entre [0,1], onde valores altos indicam alta similaridade, **a análise provou que ele não é uma métrica totalmente confiável para avaliar os gráficos visualmente**. A fórmula valoriza muito os Verdadeiros Negativos ($D$). Como as bases possuem muitos pontos, algoritmos que dividem os dados acertam a maioria dos casos por pura estatística, mascarando erros visuais graves com notas altas.

---

## Principais Resultados por Dataset

* **Dataset Aggregation:** Apesar do Índice Rand alto (>0.93), ambos falharam geometricamente. O K-Means fatiou grupos largos, e o Single Linkage fundiu estruturas devido a trilhas de pontos soltos.
* **Dataset D31:** Cenário perfeito para o K-Means (grupos circulares), atingindo um Índice Rand muito próximo de 1.00. O Single Linkage falhou ao mesclar limites de vizinhos próximos.
* **Dataset Path-Based1:** O K-Means fez cortes retos ignorando o formato em arco dos dados. O Single Linkage uniu o arco aos grupos centrais através de uma "ponte" de pontos.
* **Dataset Flame:** O K-Means não conseguiu contornar a forma em "U" e fatiou a figura. O Single Linkage uniu quase tudo em um único grupo devido à proximidade contínua dos pontos.

---

## Tecnologias Utilizadas
* **Python**
* **Pandas** (Manipulação de dados)
* **Matplotlib** (Visualização gráfica)
* **Scikit-Learn** (K-Means, AgglomerativeClustering e rand_score)

---

## Como Executar
1. Clone o repositório.
2. Certifique-se de ter as bibliotecas pandas, matplotlib e scikit-learn instaladas.
3. Execute o script principal. O código faz o download automático dos datasets diretamente dos diretórios online.
---
