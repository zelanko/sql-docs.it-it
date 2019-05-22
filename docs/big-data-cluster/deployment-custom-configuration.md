---
title: Configurare le distribuzioni
titleSuffix: SQL Server big data clusters
description: Informazioni su come personalizzare una distribuzione cluster con i big data con i file di configurazione.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed86e7d293ba72eb178c65b53865b62ca419a6d2
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993993"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Configurare le impostazioni di distribuzione per i cluster di big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Per personalizzare il file di configurazione di distribuzione del cluster, è possibile usare qualsiasi editor di formato json, ad esempio Visual Studio code. Per queste modifiche per scopi di automazione di script, è disponibile un' **sezione di configurazione del cluster mssqlctl** comando. Questo articolo illustra come configurare le distribuzioni di cluster di big data, modificando i file di configurazione di distribuzione. Fornisce esempi su come modificare la configurazione per scenari diversi. Per altre informazioni sulle modalità di utilizzo file di configurazione nelle distribuzioni, vedere la [Guida alla distribuzione](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisiti

- [Installare mssqlctl](deploy-install-mssqlctl.md).

- Ognuno degli esempi in questa sezione si presuppone di aver creato una copia di uno dei file di configurazione standard. Per altre informazioni, vedere [creare un file di configurazione personalizzato](deployment-guidance.md#customconfig). Ad esempio, il comando seguente crea una **custom.json** file basato su quello predefinito **aks-dev-test.json** configurazione:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

## <a id="clustername"></a> Modifica nome cluster

Il nome del cluster è sia il nome del cluster di big data e lo spazio dei nomi Kubernetes che verrà creato nella distribuzione. Viene specificato nella parte seguente del file di configurazione della distribuzione:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

Il comando seguente invia una coppia chiave-valore per il **-- json-values** parametro per modificare il nome del cluster per i big data **test-cluster**:

```bash
mssqlctl cluster config section set -c custom.json -j ".metadata.name=test-cluster"
```

> [!IMPORTANT]
> Il nome del cluster deve essere solo alfanumerici caratteri minuscoli, senza spazi. Tutti Kubernetes gli elementi (contenitori, i POD, set prive di stato e servizi) per il cluster verranno creati in uno spazio dei nomi con lo stesso nome del cluster il nome specificato.

## <a id="ports"></a> Aggiornare le porte di endpoint

Gli endpoint vengono definiti per il piano di controllo anche per quanto riguarda i singoli pool. La parte seguente del file di configurazione Mostra le definizioni di endpoint per il piano di controllo:

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
    },
    {
        "name": "AppServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30778
    },
    {
        "name": "Knox",
        "serviceType": "LoadBalancer",
        "port": 30443
    }
]
```

L'esempio seguente usa inline JSON per cambiare la porta per il **Controller** endpoint:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurare le repliche di pool

Le caratteristiche di ogni pool, ad esempio il pool di archiviazione, è definito nel file di configurazione. Ad esempio, la parte seguente mostra una definizione di pool di archiviazione:

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
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
        }
    }
]
```

È possibile configurare il numero di istanze in un pool modificando la **repliche** valore per ogni pool. L'esempio seguente usa inline JSON per modificare questi valori per i pool di archiviazione e i dati al `10` e `4` rispettivamente:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4'
```

## <a id="storage"></a> Configurare l'archiviazione

È anche possibile modificare la classe di archiviazione e le caratteristiche usate per ogni pool. Nell'esempio seguente assegna una classe di archiviazione personalizzati per il pool di archiviazione e aggiorna le dimensioni dell'attestazione di volume permanente per l'archiviazione dei dati da 100Gb. È necessario in questa sezione al file di configurazione per aggiornare le impostazioni tramite il *mssqlctl cluster config set* comando, vedere di seguito come utilizzare un file di patch per aggiungere in questa sezione:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.className=storage-pool-class"
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=32Gi"
```

> [!NOTE]
> Un file di configurazione di base **kubeadm-dev-test.json** non dispone di una definizione di archiviazione per ogni pool, ma questa può essere aggiunto manualmente se necessario.

Per altre informazioni sulla configurazione dell'archiviazione, vedere [persistenza dei dati con SQL Server del cluster di big data in Kubernetes](concept-data-persistence.md).

## <a id="podplacement"></a> Configurare il posizionamento di pod usando le etichette di Kubernetes

È possibile controllare la selezione host pod nei nodi Kubernetes che dispongono di risorse specifiche per supportare vari tipi di requisiti di carico di lavoro. Ad esempio, è possibile garantire il numero di POD di pool di archiviazione viene inseriti nei nodi con più spazio di archiviazione o istanze master di SQL Server vengono inserite nei nodi che dispongono di risorse di memoria e CPU superiore. In questo caso, prima di tutto si creerà un cluster Kubernetes eterogeneo con diversi tipi di hardware e quindi [assegnare le etichette nodo](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) conseguenza. Al momento della distribuzione di cluster di big data, è possibile specificare le stesse etichette a livello di pool nel file di configurazione di distribuzione del cluster. Kubernetes quindi si occuperà di consentendo i POD in nodi che soddisfano le etichette specificate.

Nell'esempio seguente viene illustrato come modificare un file di configurazione personalizzati per includere un'impostazione di etichetta del nodo per l'istanza master di SQL Server. Si noti che è presente alcun *nodeLabel* chiave nelle configurazioni di incorporata, pertanto sarà necessario modificare manualmente un file di configurazione personalizzato o creare un file di patch e applicarlo al file di configurazione personalizzato.

Creare un file denominato **patch.json** nella directory corrente con il contenuto seguente:

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a id="jsonpatch"></a> File della patch di JSON

File della patch di JSON configurare più impostazioni in una sola volta. Per altre informazioni sulle patch JSON, vedere [le patch di JSON in Python](https://github.com/stefankoegl/python-json-patch) e il [analizzatore Online JSONPath](https://jsonpath.com/).

Quanto segue **patch.json** file esegue le modifiche seguenti:

- Aggiorna la porta dell'endpoint singolo.
- Aggiorna tutti gli endpoint (**porta** e **serviceType**).
- Aggiorna lo spazio di archiviazione di piano di controllo. Queste impostazioni sono applicabili a tutti i componenti di cluster, a meno che non viene sottoposto a override a livello di pool.
- Aggiorna il nome della classe di archiviazione in archiviazione di piano di controllo.
- Aggiorna le impostazioni di archiviazione del pool per pool di archiviazione.
- Aggiorna le impostazioni di Spark per pool di archiviazione.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
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
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "AppServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30443,
            "name": "Knox"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.controlPlane",
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
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.data.className",
      "value": "managed-premium"
    },
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
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
    },
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

> [!TIP]
> Per altre informazioni sulla struttura e le opzioni per la modifica di un file di configurazione di distribuzione, vedere [riferimento a file di configurazione di distribuzione per i cluster di big data](reference-deployment-config.md).

Uso **gruppo di sezione di configurazione di cluster mssqlctl** per applicare le modifiche nel file di patch di JSON. L'esempio seguente applica il **patch.json** file in un file di configurazione di distribuzione di destinazione **custom.json**.

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'utilizzo dei file di configurazione nelle distribuzioni di cluster di big data, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md#configfile).
