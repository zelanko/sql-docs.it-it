---
title: Configurare le distribuzioni
titleSuffix: SQL Server big data clusters
description: Informazioni su come personalizzare la distribuzione di un cluster Big Data con file di configurazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cae2c216245fdb6483b3ad07a88b3517c38550bd
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470747"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Configurare le impostazioni di distribuzione per cluster Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Per personalizzare i file di configurazione della distribuzione del cluster, è possibile usare qualsiasi editor in formato JSON, ad esempio VSCode. Per la creazione di script per queste modifiche a scopo di automazione, usare il comando **azdata bdc config**. Questo articolo descrive come configurare le distribuzioni di cluster Big Data modificando i file di configurazione della distribuzione. Fornisce anche alcuni esempi su come modificare la configurazione per diversi scenari. Per altre informazioni sull'uso di file di configurazione nelle distribuzioni, vedere le [linee guida per la distribuzione](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisiti

- [Installare azdata](deploy-install-azdata.md).

- Ognuno degli esempi in questa sezione presuppone che sia stata creata una copia di una delle configurazioni standard. Per altre informazioni, vedere [Creare una pubblicazione](deployment-guidance.md#customconfig). Ad esempio, il comando seguente crea una directory denominata `custom` che contiene due file di configurazione della distribuzione JSON, **cluster.json** e **control.json**, in base alla configurazione **aks-dev-test** predefinita:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Modificare il nome del cluster

Il nome del cluster è sia il nome del cluster Big Data sia lo spazio dei nomi Kubernetes che verrà creato durante la distribuzione. Viene specificato nella parte seguente del file di configurazione della distribuzione **cluster.json**:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

Il comando seguente invia una coppia chiave-valore al parametro **--json-values** per modificare il nome del cluster Big Data in **test-cluster**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> Il nome del cluster Big Data deve contenere solo caratteri alfanumerici minuscoli, senza spazi. Tutti gli elementi Kubernetes (contenitori, pod, set con stato, servizi) per il cluster verranno creati in uno spazio dei nomi con lo stesso nome del nome del cluster specificato.

## <a id="ports"></a> Aggiornare le porte degli endpoint

Gli endpoint vengono definiti per il controller in **control.json** e per il gateway e l'istanza master di SQL Server nelle sezioni corrispondenti in **cluster.json**. La parte seguente del file di configurazione **control.json** mostra le definizioni degli endpoint per il controller:

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

L'esempio seguente usa il formato JSON inline per modificare la porta per l'endpoint **controller**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurare repliche dei pool

Le caratteristiche di ogni pool, ad esempio il pool di archiviazione, vengono definite nel file di configurazione **cluster.json**. Ad esempio, la parte seguente del file **cluster.json** mostra una definizione del pool di archiviazione:

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

È possibile configurare il numero di istanze in un pool modificando il valore **replicas** per ogni pool. L'esempio seguente usa il formato JSON inline per modificare questi valori per i pool di archiviazione e di dati rispettivamente in `10` e `4`:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> Configurare l'archiviazione

È anche possibile modificare la classe di archiviazione e le caratteristiche usate per ogni pool. L'esempio seguente assegna una classe di archiviazione personalizzata al pool di archiviazione e aggiorna la dimensione dell'attestazione di volume permanente per l'archiviazione dei dati a 100 GB. Creare prima di tutto un file patch.json come indicato di seguito, che include la nuova sezione *storage*, oltre a *type* e *replicas*

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

È quindi possibile usare il comando **azdata bdc config patch** per aggiornare il file di configurazione **cluster.json**.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> Un file di configurazione basato su **kubeadm-dev-test** non include una definizione di archiviazione per ogni pool, ma è possibile usare il processo precedente per aggiungerle, se necessario.

Per altre informazioni sulla configurazione dell'archiviazione, vedere [Salvataggio permanente dei dati con un cluster Big Data di SQL Server in Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configurare il pool di archiviazione senza Spark

È anche possibile configurare i pool di archiviazione per l'esecuzione senza Spark e creare un pool Spark separato. In questo modo, è possibile ridimensionare la potenza di calcolo di Spark indipendentemente dall'archiviazione. Per informazioni su come configurare il pool Spark, vedere l'[esempio di file di patch JSON](#jsonpatch) alla fine di questo articolo.



Poiché per impostazione predefinita il valore di **includeSpark** per il pool di archiviazione è impostato su true, è necessario aggiungere il campo **includeSpark** nella configurazione dell'archiviazione per poter apportare modifiche. Il file di patch JSON seguente mostra come aggiungere questo campo.

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

## <a id="podplacement"></a> Configurare la posizione dei pod tramite etichette Kubernetes

È possibile controllare la posizione dei pod in nodi Kubernetes che includono risorse specifiche per soddisfare i vari tipi di requisiti relativi ai carichi di lavoro. Ad esempio, può essere necessario fare in modo che i pod del pool di archiviazione siano posizionati in nodi con più archiviazione o che le istanze master di SQL Server si trovino in nodi con risorse di CPU e memoria più elevate. In questo caso, si creerà prima di tutto un cluster Kubernetes eterogeneo con diversi tipi di hardware e quindi si [assegneranno le etichette dei nodi](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) di conseguenza. Al momento della distribuzione del cluster Big Data, è possibile specificare le stesse etichette a livello di pool nel file di configurazione della distribuzione del cluster. Kubernetes si occuperà quindi dell'impostazione dell'affinità dei pod e dei nodi che corrispondono a etichette specifiche.

L'esempio seguente mostra come modificare un file di configurazione personalizzato in modo da includere un'impostazione per le etichette dei nodi per l'istanza master di SQL Server. Si noti che non è presente alcuna chiave *nodeLabel* nelle configurazioni predefinite e di conseguenza è necessario modificare un file di configurazione personalizzato manualmente oppure creare un file di patch e applicarlo al file di configurazione personalizzato.

Creare un file denominato **patch.json** nella directory corrente con il contenuto seguente:

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

## <a id="jsonpatch"></a> File di patch JSON

I file di patch JSON configurano più impostazioni contemporaneamente. Per altre informazioni sulle patch JSON, vedere [Patch JSON in Python](https://github.com/stefankoegl/python-json-patch) e [JSONPath Online Evaluator](https://jsonpath.com/).

Il file **patch.json** seguente esegue queste modifiche:

- Aggiorna la porta di un singolo endpoint in **control.json**.
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

- Aggiorna tutti gli endpoint (**port** e **serviceType**) in **control.json**.
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

- Aggiorna le impostazioni di archiviazione del controller in **control.json**. Queste impostazioni sono applicabili a tutti i componenti del cluster, a meno che non vengano sostituite a livello di pool.
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

- Aggiorna il nome della classe di archiviazione in **control.json**.
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

- Aggiorna le impostazioni di archiviazione per il pool di archiviazione in **cluster.json**.
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

- Aggiorna le impostazioni di Spark per il pool di archiviazione in **cluster.json**.
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

- Crea un pool Spark con 2 istanze in **cluster.json**.
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
> Per altre informazioni sulla struttura e sulle opzioni per modificare un file di configurazione della distribuzione, vedere [Informazioni di riferimento sul file di configurazione della distribuzione per cluster Big Data](reference-deployment-config.md).

Usare il comando **azdata bdc config** per applicare le modifiche nel file di patch JSON. L'esempio seguente applica il file **patch.json** a un file di configurazione della distribuzione di destinazione **custom/cluster.json**.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'uso di file di configurazione in distribuzioni di cluster Big Data, vedere [Come distribuire cluster Big Data di SQL Server in Kubernetes](deployment-guidance.md#configfile).
