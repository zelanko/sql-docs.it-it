---
title: Utilizzare le applicazioni in cluster SQL Server Big Data
titleSuffix: SQL Server big data clusters
description: Utilizzare un'applicazione distribuita [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] in utilizzando un servizio Web RESTful (anteprima).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d65cb2577749a45bccf1383bdf880ce8c5a7a46
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653065"
---
# <a name="consume-an-app-deployed-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-a-restful-web-service"></a>Utilizzare un'app distribuita [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] con un servizio Web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come utilizzare un'applicazione distribuita in un cluster Big Data di SQL Server 2019 tramite un servizio Web RESTful (anteprima).

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data di SQL Server 2019](deployment-guidance.md)
- [Utilità della riga di comando azdata](deploy-install-azdata.md)
- App distribuita tramite [azdata](big-data-cluster-create-apps.md) o l'[estensione per la distribuzione di app](app-deployment-extension.md)

## <a name="capabilities"></a>Funzionalità

Dopo aver distribuito un'applicazione in [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], è possibile accedere a tale applicazione e utilizzarla utilizzando un servizio Web RESTful. In questo modo, è possibile integrare l'app da altri servizi o applicazioni, ad esempio un'app per dispositivi mobili o un sito Web. La tabella seguente descrive i comandi per la distribuzione di applicazioni che è possibile usare con **azdata** per ottenere informazioni sul servizio Web RESTful per l'app.

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
azdata app describe --name addpy --version v1
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

Uno degli altri modi per ottenere queste informazioni è fare clic con il pulsante destro del mouse su Gestisci nel server in Azure Data Studio in cui si troveranno gli endpoint dei servizi elencati.

![Endpoint ADS](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>Generare un token di accesso JWT

Per accedere al servizio Web RESTful per l'app distribuita, prima di tutto è necessario generare un token di accesso JWT. Aprire l'URL `https://[IP]:[PORT]/docs/swagger.json` nel browser usando l'indirizzo IP e la porta recuperati prima eseguendo il comando `describe`. Dovrai accedere con le stesse credenziali usate per `azdata login`.

Incollare il contenuto di `swagger.json` in [Swagger Editor](https://editor.swagger.io) per determinare i metodi disponibili:

![Swagger API](media/big-data-cluster-consume-apps/api_swagger.png)

Notare il metodo GET `app` e il metodo POST `token`. Poiché l'autenticazione per le app usa token JWT, è necessario ottenere un token usando lo strumento preferito per effettuare una chiamata post al `token` metodo. Ecco un esempio di come eseguire questa operazione in [Postman](https://www.getpostman.com/):

![Token Postman](media/big-data-cluster-consume-apps/postman_token.png)

Il risultato di questa richiesta fornirà un JWT `access_token`, che sarà necessario chiamare l'URL per eseguire l'app.

## <a name="execute-the-app-using-the-restful-web-service"></a>Eseguire l'app usando il servizio Web RESTful

> [!NOTE]
> Se lo si desidera, è possibile aprire l'URL per `swagger` restituito durante l'esecuzione di `azdata app describe --name [appname] --version [version]` nel browser, che sarà simile a `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`. Sarà necessario accedere con le stesse credenziali usate per `azdata login`. È possibile incollare il contenuto di `swagger.json` in [Swagger Editor](https://editor.swagger.io). Si noterà che il servizio Web espone il metodo `run`. Notare anche l'URL di base visualizzato nella parte superiore.

È possibile usare lo strumento preferito per chiamare il metodo `run` (`https://[IP]:30778/api/app/[appname]/[version]/run`), passando i parametri nel corpo della richiesta POST come JSON. In questo esempio verrà usato il [post](https://www.getpostman.com/). Prima di effettuare la chiamata, è necessario impostare `Authorization` su `Bearer Token` e incollare il token recuperato in precedenza. In questo modo, verrà impostata un'intestazione per la richiesta. Vedere lo screenshot di seguito.

![Intestazioni di esecuzione in Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Nel corpo della richiesta passare quindi i parametri all'app che si sta chiamando e impostare `content-type` su `application/json`:

![Corpo per l'esecuzione in Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Quando si invia la richiesta, si ottiene lo stesso output restituito durante l'esecuzione dell'app tramite `azdata app run`:

![Risultato di esecuzione in Postman](media/big-data-cluster-consume-apps/postman_result.png)

L'app è stata chiamata tramite il servizio Web. È possibile seguire una procedura simile per integrare questo servizio Web nell'applicazione.

## <a name="next-steps"></a>Passaggi successivi

È anche possibile fare riferimento ad altri esempi in [Esempi di distribuzione di app](https://aka.ms/sql-app-deploy).

Per ulteriori informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
