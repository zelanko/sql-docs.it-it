---
title: Configurare le distribuzioni
titleSuffix: SQL Server big data clusters
description: Informazioni su come personalizzare la distribuzione di un cluster Big Data con file di configurazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0b76b6645e6be35f04b1a83670a99e529dcb84d6
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745448"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>Configurare le impostazioni di distribuzione per i servizi e le risorse del cluster

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Partendo da un set predefinito di profili di configurazione incorporati nello strumento di gestione di azdata, è possibile modificare facilmente le impostazioni predefinite per soddisfare al meglio i requisiti del carico di lavoro di integrazione applicativa dei dati. A partire dalla versione finale candidata, la struttura dei file di configurazione è stata aggiornata per consentire di aggiornare in modo granulare le impostazioni per ogni servizio della risorsa. 

È anche possibile impostare le configurazioni a livello di risorsa o aggiornare le configurazioni per tutti i servizi in una risorsa. Di seguito è riportato un riepilogo della struttura per **BDC. JSON**:

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

Per aggiornare le configurazioni a livello di risorsa, ad esempio le istanze in un pool, è necessario aggiornare la specifica della risorsa. Ad esempio, per aggiornare il numero di istanze nel pool di calcolo, si modificherà questa sezione nel file di configurazione **BDC. JSON** :
```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

Analogamente, per modificare le impostazioni di un singolo servizio all'interno di una risorsa specifica. Ad esempio, se si vuole modificare le impostazioni della memoria di Spark solo per il componente Spark nel pool di archiviazione, è necessario aggiornare la risorsa **storage-0** con una sezione **delle impostazioni** per il servizio **Spark** nel file di configurazione **BDC. JSON** .
```json
"resources":{
    ...
     "storage-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "settings": {
                "spark": {
                    "driverMemory": "2g",
                    "driverCores": "1",
                    "executorInstances": "3",
                    "executorMemory": "1536m",
                    "executorCores": "1"
                }
            }
        }
    }
    ...
}
```

Se si desidera applicare le stesse configurazioni per un servizio associato a più risorse, verranno aggiornate le **Impostazioni** corrispondenti nella sezione **Servizi** . Ad esempio, se si desidera impostare le stesse impostazioni per Spark in entrambi i pool di archiviazione e i pool Spark, è necessario aggiornare la sezione **Impostazioni** nella sezione servizio **Spark** del file di configurazione **BDC. JSON** .

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "driverMemory": "2g",
            "driverCores": "1",
            "executorInstances": "3",
            "executorMemory": "1536m",
            "executorCores": "1"
        }
    }
    ...
}
```


Per personalizzare i file di configurazione della distribuzione del cluster, è possibile usare qualsiasi editor in formato JSON, ad esempio VSCode. Per la creazione di script per queste modifiche a scopo di automazione, usare il comando **azdata bdc config**. Questo articolo descrive come configurare le distribuzioni di cluster Big Data modificando i file di configurazione della distribuzione. Fornisce anche alcuni esempi su come modificare la configurazione per diversi scenari. Per altre informazioni sull'uso di file di configurazione nelle distribuzioni, vedere le [linee guida per la distribuzione](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisiti

- [Installare azdata](deploy-install-azdata.md).

- Ognuno degli esempi in questa sezione presuppone che sia stata creata una copia di una delle configurazioni standard. Per altre informazioni, vedere [Creare una pubblicazione](deployment-guidance.md#customconfig). Ad esempio, il comando seguente crea una directory denominata `custom` che contiene due file di configurazione della distribuzione JSON, **BDC. JSON** e **Control. JSON**, basati sulla configurazione predefinita **AKS-dev-test** :

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Modificare il nome del cluster

Il nome del cluster è sia il nome del cluster Big Data sia lo spazio dei nomi Kubernetes che verrà creato durante la distribuzione. Viene specificato nella parte seguente del file di configurazione della distribuzione di **BDC. JSON** :

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

Il comando seguente invia una coppia chiave-valore al parametro **--json-values** per modificare il nome del cluster Big Data in **test-cluster**:

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> Il nome del cluster Big Data deve contenere solo caratteri alfanumerici minuscoli, senza spazi. Tutti gli elementi Kubernetes (contenitori, pod, set con stato, servizi) per il cluster verranno creati in uno spazio dei nomi con lo stesso nome del nome del cluster specificato.

## <a id="ports"></a> Aggiornare le porte degli endpoint

Gli endpoint vengono definiti per il controller nel file **Control. JSON** e per il gateway e l'istanza di SQL Server Master nelle sezioni corrispondenti in **BDC. JSON**. La parte seguente del file di configurazione **control.json** mostra le definizioni degli endpoint per il controller:

```json
{
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
}
```

L'esempio seguente usa il formato JSON inline per modificare la porta per l'endpoint **controller**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurare repliche dei pool

Le configurazioni di ogni risorsa, ad esempio il pool di archiviazione, vengono definite nel file di configurazione **BDC. JSON** . Ad esempio, la parte seguente di **BDC. JSON** Mostra una definizione di risorsa **storage-0** :

```json
"storage-0": {
    "metadata": {
        "kind": "Pool",
        "name": "default"
    },
    "spec": {
        "type": "Storage",
        "replicas": 2,
        "settings": {
            "spark": {
                "driverMemory": "2g",
                "driverCores": "1",
                "executorInstances": "3",
                "executorMemory": "1536m",
                "executorCores": "1"
            }
        }
    }
}
```

È possibile configurare il numero di istanze in un pool modificando il valore **replicas** per ogni pool. L'esempio seguente usa il formato JSON inline per modificare questi valori per i pool di archiviazione e di dati rispettivamente in `10` e `4`:

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

## <a id="storage"></a> Configurare l'archiviazione

È anche possibile modificare la classe di archiviazione e le caratteristiche usate per ogni pool. Nell'esempio seguente viene assegnata una classe di archiviazione personalizzata ai pool di archiviazione e di dati e viene aggiornata la dimensione dell'attestazione del volume permanente per l'archiviazione dei dati in 500 GB per HDFS (pool di archiviazione) e 100 GB per il pool di dati. Creare prima di tutto un file patch.json come indicato di seguito, che include la nuova sezione *storage*, oltre a *type* e *replicas*

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "500Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

È quindi possibile usare il comando **azdata BDC config patch** per aggiornare il file di configurazione **BDC. JSON** .
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json
```

> [!NOTE]
> Un file di configurazione basato su **kubeadm-dev-test** non include una definizione di archiviazione per ogni pool, ma è possibile usare il processo precedente per aggiungerle, se necessario.

Per altre informazioni sulla configurazione dell'archiviazione, vedere [Salvataggio permanente dei dati con un cluster Big Data di SQL Server in Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configurare il pool di archiviazione senza Spark

È anche possibile configurare i pool di archiviazione per l'esecuzione senza Spark e creare un pool Spark separato. In questo modo, è possibile ridimensionare la potenza di calcolo di Spark indipendentemente dall'archiviazione. Per informazioni su come configurare il pool Spark, vedere l'[esempio di file di patch JSON](#jsonpatch) alla fine di questo articolo.


Per impostazione predefinita, l'impostazione **includeSpark** per la risorsa pool di archiviazione è impostata su true, pertanto è necessario modificare il campo **includeSpark** nella configurazione dell'archiviazione per apportare modifiche. Il comando seguente mostra come modificare questo valore usando JSON inline.

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="podplacement"></a> Configurare la posizione dei pod tramite etichette Kubernetes

È possibile controllare la posizione dei pod in nodi Kubernetes che includono risorse specifiche per soddisfare i vari tipi di requisiti relativi ai carichi di lavoro. Ad esempio, è possibile assicurarsi che i pod delle risorse del pool di archiviazione vengano posizionati in nodi con più spazio di archiviazione o SQL Server istanze master vengano posizionate su nodi con risorse di CPU e memoria più elevate. In questo caso, si creerà prima di tutto un cluster Kubernetes eterogeneo con diversi tipi di hardware e quindi si [assegneranno le etichette dei nodi](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) di conseguenza. Al momento della distribuzione del cluster Big Data, è possibile specificare le stesse etichette a livello di pool nel file di configurazione della distribuzione del cluster. Kubernetes si occuperà quindi dell'impostazione dell'affinità dei pod e dei nodi che corrispondono a etichette specifiche. La chiave dell'etichetta specifica che deve essere aggiunta ai nodi nel cluster kubernetes è **MSSQL-cluster-Wide**. Il valore di questa etichetta può essere qualsiasi stringa scelta.

Nell'esempio seguente viene illustrato come modificare un file di configurazione personalizzato per includere un'impostazione dell'etichetta del nodo per l'istanza master SQL Server, il pool di calcolo, il pool di dati & pool di archiviazione. Non esiste alcuna chiave di *nodeLabel* nelle configurazioni predefinite, quindi è necessario modificare manualmente un file di configurazione personalizzato oppure creare un file di patch e applicarlo al file di configurazione personalizzato. Il Pod dell'istanza master di SQL Server verrà distribuito in un nodo che contiene un'etichetta **MSSQL-cluster-Wide** con valore **BDC-Master**. Il pool di calcolo e i pod del pool di dati verranno distribuiti nei nodi che contengono un'etichetta **MSSQL-cluster-Wide** con valore **BDC-SQL**. I pod del pool di archiviazione verranno distribuiti nei nodi che contengono un'etichetta **MSSQL-cluster-Wide** con valore **BDC-storage**.

Creare un file denominato **patch.json** nella directory corrente con il contenuto seguente:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.master.spec",
      "value": {
        "type": "Master",
        "replicas": 1,
        "endpoints": [
          {
            "name": "Master",
            "serviceType": "NodePort",
            "port": 31433
          }
        ],
        "settings": {
          "sql": {
            "hadr.enabled": "false"
          }
        },
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.compute-0.spec",
      "value": {
        "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage",
        "settings": {
          "spark": {
            "includeSpark": "true"
          }
        }
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
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

- Aggiorna le impostazioni di archiviazione del pool per il pool di archiviazione in **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- Aggiorna le impostazioni di Spark per il pool di archiviazione in **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
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

- Consente di creare un pool Spark con 2 istanze in **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.resources.spark-0",
      "value": {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        }
      }
    },
    {
      "op": "add",
      "path": "spec.services.spark.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.hdfs.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.spark.settings",
      "value": {
        "DriverMemory": "2g",
        "DriverCores": "1",
        "ExecutorInstances": "2",
        "ExecutorMemory": "2g",
        "ExecutorCores": "1"
      }
    }
  ]
}
```

> [!TIP]
> Per altre informazioni sulla struttura e sulle opzioni per modificare un file di configurazione della distribuzione, vedere [Informazioni di riferimento sul file di configurazione della distribuzione per cluster Big Data](reference-deployment-config.md).

Usare il comando **azdata bdc config** per applicare le modifiche nel file di patch JSON. L'esempio seguente applica il file **patch. JSON** a un file di configurazione della distribuzione di destinazione **Custom/BDC. JSON**.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>Disabilitare ElasticSearch per l'esecuzione in modalità privilegiata
Per impostazione predefinita, il contenitore ElasticSearch viene eseguito in modalità Privilege nel cluster Big Data. Ciò consente di assicurarsi che al momento dell'inizializzazione del contenitore il contenitore disponga di autorizzazioni sufficienti per aggiornare un'impostazione nell'host obbligatorie quando ElasticSearch elabora una quantità maggiore di log. Altre informazioni su questo argomento sono disponibili in [questo articolo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html). 

Per disabilitare il contenitore che esegue ElasticSearch per l'esecuzione in modalità privilegiata, è necessario aggiornare la sezione **Settings** nel file **Control. JSON** e specificare il valore di **VM. max _map_count** su **-1**. Di seguito è riportato un esempio di come questa sezione avrà un aspetto simile al seguente:
```json
"settings": {
    "ElasticSearch": {
        "vm.max_map_count": "-1"
      }
}
```

È possibile manualmente modificare il file **Control. JSON** e aggiungere la sezione precedente alla **specifica**. in alternativa, è possibile creare un file di patch **elasticsearch-patch. JSON** come riportato di seguito e usare l'interfaccia della riga di comando di **azdata** per applicare patch al file **config. JSON** :

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec",
      "value": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-RC1-ubuntu",
            "imagePullPolicy": "Always"
        },
        "storage": {
            "data": {
                "className": "default",
                "accessMode": "ReadWriteOnce",
                "size": "15Gi"
            },
            "logs": {
                "className": "default",
                "accessMode": "ReadWriteOnce",
                "size": "10Gi"
            }
        },
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
        ],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
             }
        }
       }
    }
  ]
}
```

Eseguire questo comando per applicare patch al file di configurazione:
```
azdata bdc config patch --config-file control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> È consigliabile come procedura consigliata aggiornare manualmente l'impostazione di **max_map_count** in ogni host del cluster Kubernetes in base alle istruzioni riportate in [questo articolo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html).
## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo dei file di configurazione nelle distribuzioni Big Data cluster, vedere [How [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] to deploy on Kubernetes](deployment-guidance.md#configfile).
