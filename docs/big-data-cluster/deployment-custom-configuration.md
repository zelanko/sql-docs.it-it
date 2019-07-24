---
title: Configurare le distribuzioni
titleSuffix: SQL Server big data clusters
description: Informazioni su come personalizzare una distribuzione di cluster di Big Data con i file di configurazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7559ecf9c7b17ca21c088ed531a347f88e89ee2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419442"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Configurare le impostazioni di distribuzione per i cluster di Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Per personalizzare i file di configurazione della distribuzione del cluster, è possibile usare qualsiasi editor di formato JSON, ad esempio VSCode. Per la creazione di script per queste modifiche a scopo di automazione, usare il comando **azdata BDC config** . Questo articolo illustra come configurare le distribuzioni di Big Data cluster modificando i file di configurazione della distribuzione. Fornisce esempi su come modificare la configurazione per diversi scenari. Per ulteriori informazioni sulla modalità di utilizzo dei file di configurazione nelle distribuzioni, vedere la [Guida alla distribuzione](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisiti

- [Installare azdata](deploy-install-azdata.md).

- Ognuno degli esempi in questa sezione presuppone che sia stata creata una copia di una delle configurazioni standard. Per altre informazioni, vedere [creare una configurazione personalizzata](deployment-guidance.md#customconfig). Ad esempio, il comando seguente crea una directory denominata `custom` che contiene due file di configurazione della distribuzione JSON, **cluster. JSON** e **Control. JSON**, basati sulla configurazione predefinita **AKS-dev-test** :

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a>Modificare il nome del cluster

Il nome del cluster è il nome del cluster Big Data e lo spazio dei nomi Kubernetes che verrà creato durante la distribuzione. Viene specificato nella parte seguente del file di configurazione della distribuzione **cluster. JSON** :

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

Il comando seguente invia una coppia chiave-valore al parametro **--JSON-values** per modificare il nome del cluster Big data in **test-cluster**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> Il nome del cluster Big Data deve contenere solo caratteri alfanumerici minuscoli, senza spazi. Tutti gli elementi Kubernetes (contenitori, Pod, set di prive, servizi) per il cluster verranno creati in uno spazio dei nomi con lo stesso nome del nome del cluster specificato.

## <a id="ports"></a>Aggiorna porte endpoint

Gli endpoint vengono definiti per il controller nel file **Control. JSON** e per il gateway e l'istanza di SQL Server Master nelle sezioni corrispondenti in **cluster. JSON**. La parte seguente del file di configurazione **Control. JSON** Mostra le definizioni degli endpoint per il controller:

```json
"endpoints": [
    {
        "name": "Controller",
        "serviceType": "LoadBalancer",
        "port": 30080
    },
    {
        "name": "ServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30777
    }
]
```

Nell'esempio seguente viene usato il formato JSON inline per modificare la porta per l'endpoint **controller** :

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a>Configurare le repliche del pool

Le caratteristiche di ogni pool, ad esempio il pool di archiviazione, vengono definite nel file di configurazione **cluster. JSON** . Ad esempio, la parte seguente del file **cluster. JSON** Mostra una definizione del pool di archiviazione:

```json
"pools": [
   {
       "metadata": {
           "kind": "Pool",
           "name": "default"
       },
       "spec": {
           "type": "Storage",
           "replicas": 2
       }
   }
]
```

È possibile configurare il numero di istanze in un pool modificando il  valore delle repliche per ogni pool. Nell'esempio seguente viene usato il formato JSON inline per modificare questi valori per i pool di `10` archiviazione `4` e di dati in e rispettivamente:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a>Configurare l'archiviazione

È anche possibile modificare la classe di archiviazione e le caratteristiche usate per ogni pool. Nell'esempio seguente viene assegnata una classe di archiviazione personalizzata al pool di archiviazione e viene aggiornata la dimensione dell'attestazione del volume permanente per l'archiviazione dei dati a 100 GB. Creare prima di tutto un file patch. JSON come riportato di seguito, che include la nuova sezione *storage* , oltre al *tipo* e alle *repliche*

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "storage":{
        "data":{
                "size": "100Gi",
                "className": "myStorageClass",
                "accessMode":"ReadWriteOnce"
                },
        "logs":{
                "size":"32Gi",
                "className":"myStorageClass",
                "accessMode":"ReadWriteOnce"
                }
                },
        "type":"Storage",
        "replicas":2
      }
    }
  ]
}
```

È quindi possibile usare il comando **azdata BDC config patch** per aggiornare il file di configurazione **cluster. JSON** .
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> Un file di configurazione basato su **kubeadm-dev-test** non dispone di una definizione di archiviazione per ogni pool, ma è possibile usare il processo precedente per aggiungere, se necessario.

Per ulteriori informazioni sulla configurazione dell'archiviazione, vedere [persistenza dei dati con SQL Server cluster Big data in Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a>Configurare il pool di archiviazione senza Spark

È anche possibile configurare i pool di archiviazione per l'esecuzione senza Spark e creare un pool di Spark separato. Questo consente di ridimensionare la potenza di calcolo di Spark indipendentemente dall'archiviazione. Per informazioni su come configurare il pool Spark, vedere l' [esempio di file di patch JSON](#jsonpatch) alla fine di questo articolo.



Per impostazione predefinita, l'impostazione **includeSpark** per il pool di archiviazione è impostata su true, pertanto è necessario aggiungere il campo **includeSpark** nella configurazione dell'archiviazione per apportare modifiche. Il file di patch JSON seguente mostra come aggiungere questa.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "includeSpark":false
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

## <a id="podplacement"></a>Configurare la posizione di pod usando le etichette Kubernetes

È possibile controllare la posizione dei Pod nei nodi Kubernetes che dispongono di risorse specifiche per soddisfare i vari tipi di requisiti del carico di lavoro. Ad esempio, è possibile assicurarsi che i pod del pool di archiviazione siano posizionati in nodi con più spazio di archiviazione o SQL Server istanze master vengano posizionate su nodi con risorse di CPU e memoria più elevate. In questo caso, si creerà prima di tutto un cluster Kubernetes eterogeneo con diversi tipi di hardware e quindi si assegnerà le [etichette dei nodi](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) di conseguenza. Al momento della distribuzione di Big Data cluster, è possibile specificare le stesse etichette a livello di pool nel file di configurazione della distribuzione del cluster. Kubernetes eseguirà quindi il affinità fra dei Pod nei nodi che corrispondono alle etichette specificate.

Nell'esempio seguente viene illustrato come modificare un file di configurazione personalizzato per includere un'impostazione dell'etichetta del nodo per l'istanza di SQL Server master. Si noti che non è presente alcuna chiave *nodeLabel* nelle configurazioni predefinite, pertanto sarà necessario modificare manualmente un file di configurazione personalizzato oppure creare un file di patch e applicarlo al file di configurazione personalizzato.

Creare un file denominato **patch. JSON** nella directory corrente con il contenuto seguente:

```json
{
  "patch": [
     {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
           "type": "Master",
         "replicas": 1,
         "hadrEnabled": false,
         "endpoints": [
            {
             "name": "Master",
             "serviceType": "NodePort",
             "port": 31433
            }
          ],
         "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a>File patch JSON

I file di patch JSON configurano più impostazioni contemporaneamente. Per altre informazioni sulle patch JSON, vedere [patch JSON in Python](https://github.com/stefankoegl/python-json-patch) e l' [analizzatore online JSONPath](https://jsonpath.com/).

Il file **patch. JSON** seguente esegue le modifiche seguenti:

- Aggiorna la porta di un singolo endpoint in **Control. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.endpoints[?(@.name=='Controller')].port",
          "value": 30000
        }   
      ]
    }
    ```

- Aggiorna tutti gli endpoint (**porta** e **serviceType**) in **Control. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.endpoints",
          "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "ServiceProxy"
        }
          ]
        }
      ]
    }
    ```

- Aggiorna le impostazioni di archiviazione del controller in **Control. JSON**. Queste impostazioni sono applicabili a tutti i componenti del cluster, a meno che non vengano sottoposte a override a livello di pool.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage",
          "value": {
          "data": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
        }   
      ]
    }
    ```

- Aggiorna il nome della classe di archiviazione in **Control. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage.data.className",
          "value": "managed-premium"
        }   
      ]
    }
    ```

- Aggiorna le impostazioni di archiviazione del pool per il pool di archiviazione in **cluster. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
          "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
        "data":{
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode":"ReadWriteOnce"
            },
        "logs":{
            "size":"32Gi",
            "className":"myStorageClass",
            "accessMode":"ReadWriteOnce"
            }
            }
         }
        }
      ]
    }
    ```

- Aggiorna le impostazioni di Spark per il pool di archiviazione in **cluster. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
          "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
          }
        }   
      ]
    }
    ```

- Consente di creare un pool Spark con 2 istanze in **cluster. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "add",
          "path": "spec.pools/-",
          "value":
          {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": 12288,
              "vcores": 6
            },
            "schedulerMax": {
              "memory": 12288,
              "vcores": 6
            },
            "capacityScheduler": {
              "maxAmPercent": 0.3
            }
          },
          "spark": {
            "driverMemory": "2g",
            "driverCores": 1,
            "executorInstances": 2,
            "executorMemory": "2g",
            "executorCores": 1
          }
        }
          }
        } 
      ]
    }
    ```



> [!TIP]
> Per altre informazioni sulla struttura e sulle opzioni per la modifica di un file di configurazione della distribuzione, vedere informazioni di [riferimento sui file di configurazione della distribuzione per i cluster Big Data](reference-deployment-config.md).

Usare i comandi di **configurazione di integrazione applicativa** dei dati di azdata per applicare le modifiche nel file di patch JSON. L'esempio seguente applica il file **patch. JSON** a un file di configurazione della distribuzione di destinazione **Custom/cluster. JSON**.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo dei file di configurazione nelle distribuzioni Big Data cluster, vedere [How to deploy SQL Server Big Data Clusters on Kubernetes](deployment-guidance.md#configfile).
