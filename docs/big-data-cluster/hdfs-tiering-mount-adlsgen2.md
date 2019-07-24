---
title: Montare ADLS Gen2 per la suddivisione in livelli HDFS
titleSuffix: How to mount ADLS Gen2
description: Questo articolo illustra come configurare la suddivisione in livelli di HDFS per montare un file system di Azure Data Lake Storage esterno in HDFS in un cluster Big Data SQL Server 2019 (anteprima).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7d8a6dd53452700853dca9774ed0196ed7546fe
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419352"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Come montare ADLS Gen2 per la suddivisione in livelli di HDFS in un cluster Big Data

Le sezioni seguenti forniscono un esempio di come configurare la suddivisione in livelli di HDFS con un'origine dati Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a>Caricare i dati in Azure Data Lake Storage

Nella sezione seguente viene descritto come configurare Azure Data Lake Storage Gen2 per testare la suddivisione in livelli di HDFS. Se i dati sono già archiviati in Azure Data Lake Storage, è possibile ignorare questa sezione per usare i propri dati.

1. [Creare un account di archiviazione con data Lake storage Gen2 funzionalità](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Creare un contenitore BLOB](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) in questo account di archiviazione per i dati esterni.

1. Caricare un file con estensione CSV o parquet nel contenitore. Si tratta dei dati HDFS esterni che verranno montati in HDFS nel cluster Big Data.

## <a name="credentials-for-mounting"></a>Credenziali per il montaggio

## <a name="use-oauth-credentials-to-mount"></a>Usare le credenziali OAuth per il montaggio

Per usare le credenziali OAuth per il montaggio, è necessario attenersi alla procedura seguente:

1. Passare alla [portale di Azure](https://portal.azure.com)
1. Passare a "Services" (servizi) nel riquadro di spostamento a sinistra e clock on "Azure Active Directory".
1. Utilizzando "registrazioni per l'app" nel menu, creare un'applicazione Web e seguire la procedura guidata. **Ricordare il nome creato qui**. Sarà necessario aggiungere questo nome all'account ADLS come utente autorizzato.
1. Dopo aver creato l'applicazione Web, passare a "chiavi" in "Impostazioni" per l'app.
1. Selezionare una durata della chiave e fare clic su Salva. **Salvare la chiave generata.**
1.  Tornare alla pagina registrazioni per l'app e fare clic sul pulsante "endpoint" nella parte superiore. **Annotare l'URL dell'endpoint token**
1. A questo punto dovrebbero essere indicati gli elementi seguenti per OAuth:

    - "ID applicazione" dell'app Web creata in precedenza nel passaggio 3
    - Chiave appena generata nel passaggio 5
    - Endpoint token dal passaggio 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Aggiunta dell'entità servizio all'account ADLS

1. Tornare al portale e aprire l'account ADLS e selezionare controllo di accesso (IAM) nel menu a sinistra.
1. Selezionare "Aggiungi un'assegnazione di ruolo" e cercare il nome creato in passaggio 3 in precedenza (si noti che non viene visualizzato nell'elenco, ma verrà trovato se si cerca il nome completo).
1. Aggiungere ora il ruolo "collaboratore dati BLOB di archiviazione (anteprima)".

Attendere 5-10 minuti prima di usare le credenziali per il montaggio

### <a name="set-environment-variable-for-oauth-credentials"></a>Imposta la variabile di ambiente per le credenziali OAuth

Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data. Impostare una variabile di ambiente usando il formato seguente: Si noti che le credenziali devono trovarsi in un elenco delimitato da virgole. Il comando ' set ' viene usato in Windows. Se si usa Linux, usare invece ' export '.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Usare le chiavi di accesso per il montaggio

È anche possibile montare usando chiavi di accesso che è possibile ottenere per l'account ADLS nel portale di Azure.

 > [!TIP]
   > Per altre informazioni su come trovare la chiave di accesso (`<storage-account-access-key>`) per l'account di archiviazione, vedere [visualizzare le chiavi dell'account e la stringa di connessione](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Imposta la variabile di ambiente per le credenziali della chiave di accesso

1. Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data.

1. Aprire un prompt dei comandi in un computer client in grado di accedere al cluster Big Data. Impostare una variabile di ambiente usando il formato seguente. Si noti che le credenziali devono trovarsi in un elenco delimitato da virgole. Il comando ' set ' viene usato in Windows. Se si usa Linux, usare invece ' export '.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a>Montare la risorsa di archiviazione HDFS remota

Ora che è stata impostata la variabile di ambiente MOUNT_CREDENTIALS per le chiavi di accesso o l'uso di OAuth, è possibile avviare il montaggio. La procedura seguente consente di montare l'archiviazione HDFS remota in Azure Data Lake all'archiviazione HDFS locale del cluster di Big Data.

1. Usare **kubectl** per trovare l'indirizzo IP per il servizio endpoint **controller-SVC-external** nel cluster Big Data. Cercare **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Accedere con **azdata** usando l'indirizzo IP esterno dell'endpoint del controller con il nome utente e la password del cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. Imposta la variabile di ambiente MOUNT_CREDENTIALS (Scorri verso l'alto per istruzioni)

1. Montare la risorsa di archiviazione HDFS remota in Azure usando **azdata BDC storage-pool Mount create**. Sostituire i valori segnaposto prima di eseguire il comando seguente:

   ```bash
   azdata bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > Il comando Mount create è asincrono. A questo punto, non è presente alcun messaggio che indica se il montaggio è riuscito. Per verificare lo stato dei montaggi, vedere la sezione relativa allo [stato](#status) .

Se montata correttamente, dovrebbe essere possibile eseguire una query sui dati di HDFS ed eseguire processi Spark su di essa. Verrà visualizzato in HDFS per il cluster Big Data nel percorso specificato da `--mount-path`.

## <a id="status"></a>Ottenere lo stato dei montaggi

Per elencare lo stato di tutti i montaggi nel cluster Big Data, usare il comando seguente:

```bash
azdata bdc storage-pool mount status
```

Per elencare lo stato di un montaggio in un percorso specifico in HDFS, usare il comando seguente:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Aggiornare un montaggio

Nell'esempio seguente viene aggiornato il montaggio.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>Elimina il montaggio

Per eliminare il montaggio, usare il comando **azdata BDC storage-pool Mount Delete** e specificare il percorso di montaggio in HDFS:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster SQL Server 2019 Big Data, vedere [che cosa sono i cluster SQL Server 2019 Big Data?](big-data-cluster-overview.md).
