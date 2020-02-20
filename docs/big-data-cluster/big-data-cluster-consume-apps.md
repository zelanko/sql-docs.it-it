---
title: Usare le applicazioni
titleSuffix: SQL Server Big Data Clusters
description: Usare un'applicazione distribuita in un cluster Big Data di SQL Server tramite un servizio Web RESTful.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 01/07/2020
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 305080d5c3b0a1c517d757c1f6f2bd07fefb216c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75721406"
---
# <a name="consume-an-app-deployed-on-big-data-clusters-2019-using-a-restful-web-service"></a>Usare un'app distribuita in [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] tramite un servizio Web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come usare un'applicazione distribuita in un cluster Big Data di SQL Server tramite un servizio Web RESTful.

## <a name="prerequisites"></a>Prerequisites

- [Cluster Big Data di SQL Server](deployment-guidance.md)
- [Utilità della riga di comando azdata](deploy-install-azdata.md)
- App distribuita tramite [azdata](big-data-cluster-create-apps.md) o l'[estensione per la distribuzione di app](app-deployment-extension.md)

## <a name="capabilities"></a>Capabilities

Dopo aver distribuito un'applicazione in [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], è possibile accedervi e usarla tramite un servizio Web RESTful. In questo modo, è possibile integrare l'app da altri servizi o applicazioni, ad esempio un'app per dispositivi mobili o un sito Web. La tabella seguente descrive i comandi per la distribuzione di applicazioni che è possibile usare con **azdata** per ottenere informazioni sul servizio Web RESTful per l'app.

|Comando |Descrizione |
|:---|:---|
|`azdata app describe` | Descrive un'applicazione. |

È possibile ottenere informazioni con il parametro `--help`, come nell'esempio seguente:

```bash
azdata app describe --help
```

Le sezioni seguenti descrivono come recuperare un endpoint per un'applicazione e come usare il servizio Web RESTful per l'integrazione dell'applicazione.

## <a name="retrieve-the-endpoint"></a>Recuperare l'endpoint

Il comando **azdata app describe** fornisce informazioni dettagliate sull'app, tra cui l'endpoint nel cluster. Viene usato in genere da uno sviluppatore di app per compilare un'app tramite il client Swagger e il servizio Web per interagire con l'app in modo RESTful.

Descrivere l'app eseguendo un comando simile all'esempio seguente:

```bash
azdata app describe --name add-app --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

Prendere nota dell'indirizzo IP (`10.1.1.3` in questo esempio) e del numero di porta (`30080`) nell'output.

In alternativa, è possibile trovare questa informazione facendo clic con il pulsante destro del mouse sull'opzione Gestisci nel server di Azure Data Studio, che consentirà di visualizzare gli endpoint dei servizi elencati.

![Endpoint di ADS](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>Generare un token di accesso JWT

Per accedere al servizio Web RESTful per l'app distribuita, prima di tutto è necessario generare un token di accesso JWT. L'URL per il token di accesso dipende dalla versione del cluster Big Data. 

|Versione |URL|
|------------|------|
|GDR1|  `https://[IP]:[PORT]/docs/swagger.json`|
|CU1 e versioni successive| `https://[IP]:[PORT]/api/v1/swagger.json`|

> Per informazioni sulle versioni, vedere [Cronologia delle versioni](release-notes-big-data-cluster.md#release-history).

Aprire l'URL appropriato nel browser usando l'indirizzo IP e la porta recuperati eseguendo il comando [`describe`](#retrieve-the-endpoint) in precedenza. Accedere con le stesse credenziali usate per `azdata login`.

Incollare il contenuto di `swagger.json` in [Swagger Editor](https://editor.swagger.io) per determinare i metodi disponibili:

![Swagger API](media/big-data-cluster-consume-apps/api_swagger.png)

Notare il metodo GET `app` e il metodo POST `token`. Poiché l'autenticazione per le app usa token JWT, è necessario ottenere un token usando lo strumento preferito per effettuare una chiamata POST al metodo `token`. Ecco un esempio di come eseguire questa operazione in [Postman](https://www.getpostman.com/):

![Token Postman](media/big-data-cluster-consume-apps/postman_token.png)

Il risultato di questa richiesta fornirà un token `access_token` JWT, necessario per chiamare l'URL per l'esecuzione dell'app.

## <a name="execute-the-app-using-the-restful-web-service"></a>Eseguire l'app usando il servizio Web RESTful

> [!NOTE]
> Se lo si desidera, è possibile aprire l'URL per `swagger` restituito durante l'esecuzione di `azdata app describe --name [appname] --version [version]` nel browser, che sarà simile a `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`. Sarà necessario accedere con le stesse credenziali usate per `azdata login`. È possibile incollare il contenuto di `swagger.json` in [Swagger Editor](https://editor.swagger.io). Si noterà che il servizio Web espone il metodo `run`. Notare anche l'URL di base visualizzato nella parte superiore.

È possibile usare lo strumento preferito per chiamare il metodo `run` (`https://[IP]:30778/api/app/[appname]/[version]/run`), passando i parametri nel corpo della richiesta POST come JSON. In questo esempio viene usato [Postman](https://www.getpostman.com/). Prima di effettuare la chiamata, è necessario impostare `Authorization` su `Bearer Token` e incollare il token recuperato in precedenza. In questo modo, verrà impostata un'intestazione per la richiesta. Vedere lo screenshot di seguito.

![Intestazioni di esecuzione in Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Nel corpo della richiesta passare quindi i parametri all'app che si sta chiamando e impostare `content-type` su `application/json`:

![Corpo per l'esecuzione in Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Quando si invia la richiesta, si ottiene lo stesso output restituito durante l'esecuzione dell'app tramite `azdata app run`:

![Risultato di esecuzione in Postman](media/big-data-cluster-consume-apps/postman_result.png)

L'app è stata chiamata tramite il servizio Web. È possibile seguire una procedura simile per integrare questo servizio Web nell'applicazione.

## <a name="next-steps"></a>Passaggi successivi

È anche possibile fare riferimento ad altri esempi in [Esempi di distribuzione di app](https://aka.ms/sql-app-deploy).

Per altre informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
