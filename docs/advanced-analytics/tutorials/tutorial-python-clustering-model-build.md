---
title: 'Esercitazione: Creare un modello di clustering in Python'
description: Nella terza parte di questa serie di esercitazioni in quattro parti, verrà compilato un modello K-means per eseguire il clustering in Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ce7f6cbd580afbdbf71065803af8d394323e5dc3
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211975"
---
# <a name="tutorial-build-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>Esercitazione: Creare un modello di clustering in Python con SQL Server Machine Learning Services

Nella terza parte di questa serie di esercitazioni in quattro parti, verrà compilato un modello K-means in Python per eseguire il clustering. Nella parte successiva di questa serie verrà distribuito questo modello in un database SQL con SQL Server Machine Learning Services.

L'articolo spiega come:

> [!div class="checklist"]
> * Definire il numero di cluster per un algoritmo K-means
> * Esecuzione del clustering
> * Analizzare i risultati

Nella [prima parte](tutorial-python-clustering-model.md), sono stati installati i prerequisiti e il database di esempio è stato importato.

Nella [seconda parte](tutorial-python-clustering-model-prepare-data.md)si è appreso come preparare i dati da un database SQL per eseguire il clustering.

Nella [quarta parte](tutorial-python-clustering-model-deploy.md)verrà illustrato come creare un stored procedure in un database SQL in grado di eseguire il clustering in Python in base ai nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* Nella terza parte di questa esercitazione si presuppone che siano stati soddisfatti i prerequisiti della [**parte 1**](tutorial-python-clustering-model.md)e che siano stati completati i passaggi della [**seconda parte**](tutorial-python-clustering-model-prepare-data.md).

## <a name="define-the-number-of-clusters"></a>Definire il numero di cluster

Per raggruppare i dati dei clienti, si userà l'algoritmo di clustering **K-means** , uno dei modi più semplici e noti per raggruppare i dati.
Per altre informazioni su K-means, vedere [la guida completa all'algoritmo di clustering k-means](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html).

L'algoritmo accetta due input: I dati stessi e un numero predefinito "*k*" che rappresenta il numero di cluster da generare.
L'output è un cluster *k* con i dati di input partizionati tra i cluster.

L'obiettivo di K-means consiste nel raggruppare gli elementi in cluster k, in modo che tutti gli elementi nello stesso cluster siano simili tra loro e in modo diverso dagli elementi di altri cluster, come possibile.

Per determinare il numero di cluster che l'algoritmo deve utilizzare, utilizzare un tracciato del all'interno dei gruppi somma dei quadrati, per numero di cluster estratti. Il numero appropriato di cluster da usare è alla curva o al "gomito" del tracciato.

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![Grafico a gomito](./media/python-tutorial-elbow-graph.png)

In base al grafico, sembra che *k = 4* sia un buon valore da provare. Il valore *k* raggruppa i clienti in quattro cluster.

## <a name="perform-clustering"></a>Esecuzione del clustering

Nello script Python seguente si userà la funzione KMeans dal pacchetto sklearn.

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>Analizzare i risultati

Ora che è stato eseguito il clustering con K-means, il passaggio successivo consiste nell'analizzare il risultato e verificare se è possibile trovare informazioni di utilità pratica.

Esaminare i valori medi per il clustering e le dimensioni del cluster stampate nello script precedente.

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

I quattro mezzi di cluster vengono forniti usando le variabili definite nella [parte 1](tutorial-python-clustering-model-prepare-data.md#separate-customers):

* *orderRatio* = rapporto ordine restituito (numero totale di ordini parzialmente o completamente restituiti rispetto al numero totale di ordini)
* *itemsRatio* = restituzione elemento ratio (numero totale di elementi restituiti rispetto al numero di elementi acquistati)
* *monetaryRatio* = rapporto quantità restituzione (quantità monetaria totale di elementi restituiti rispetto alla quantità acquistata)
* *Frequency* = frequenza di ritorno

Il data mining che utilizza K-means spesso richiede un'ulteriore analisi dei risultati e ulteriori passaggi per comprendere meglio ogni cluster, ma può fornire alcuni lead validi.
Ecco alcuni modi in cui è possibile interpretare i risultati:

* Il cluster 0 sembra essere un gruppo di clienti che non sono attivi (tutti i valori sono pari a zero).
* Il cluster 3 sembra essere un gruppo che si distingue in termini di comportamento di restituzione.

Il cluster 0 è un set di clienti che non sono chiaramente attivi. Forse è possibile indirizzare le attività di marketing verso questo gruppo per attivare un interesse per gli acquisti. Nel passaggio successivo verrà eseguita una query sul database per gli indirizzi di posta elettronica dei clienti nel cluster 0, in modo che sia possibile inviare un messaggio di posta elettronica di marketing.

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si intende continuare con questa esercitazione, eliminare il database tpcxbb_1gb da SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Nella terza parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Definire il numero di cluster per un algoritmo K-means
* Esecuzione del clustering
* Analizzare i risultati

Per distribuire il modello di Machine Learning creato, seguire la quarta parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione: Distribuire un modello di clustering in Python con SQL Server Machine Learning Services](tutorial-python-clustering-model-deploy.md)