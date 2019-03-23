---
title: Utilizzo di applicazioni nei cluster di big data
titleSuffix: SQL Server 2019 big data clusters
description: Utilizzare un'applicazione distribuita nel cluster di SQL Server 2019 big data usando un servizio web RESTful (anteprima).
author: jeroenterheerdt
ms.author: jterh
manager: craigg
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.reviewer: rothja
ms.openlocfilehash: 40ce93e9232d0492bd693e7920b62dc9805aa7ac
ms.sourcegitcommit: 20de089b6e23107c88fb38b9af9d22ab0c800038
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58356404"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>Usare un'app distribuita nel cluster di big data di SQL Server usando un servizio web RESTful

Questo articolo descrive come usare un'app distribuita in un cluster di SQL Server 2019 dei big data usando un servizio web RESTful (anteprima).

## <a name="prerequisites"></a>Prerequisiti

- [Cluster di big data di SQL Server 2019](deployment-guidance.md)
- [utilità della riga di comando mssqlctl](deploy-install-mssqlctl.md)
- Un'app distribuita usando [ `mssqlctl` ](big-data-cluster-create-apps.md) o il [distribuire App estensioni](app-deployment-extension.md)

## <a name="capabilities"></a>Capabilities

Dopo aver distribuito un'applicazione nel cluster di big data 2019 Server SQL (anteprima), è possibile accedere e utilizzare tale applicazione tramite un servizio web RESTful. Ciò consente l'integrazione di app da altre applicazioni o servizi (ad esempio, un'app per dispositivi mobili o sito Web). La tabella seguente descrive i comandi di distribuzione dell'applicazione che è possibile usare con **mssqlctl** per ottenere informazioni sul servizio web RESTful dell'app.

|Comando |Descrizione |
|:---|:---|
|`mssqlctl app describe` | Descrivere l'applicazione. |

È possibile ottenere assistenza con la `--help` parametro come nell'esempio seguente:

```bash
mssqlctl app describe --help
```

Le sezioni seguenti descrivono come recuperare un endpoint per un'applicazione e su come usare il servizio web RESTful per l'integrazione dell'applicazione.

## <a name="retrieve-the-endpoint"></a>Recuperare l'endpoint

Il **mssqlctl app descrivono** comando fornisce informazioni dettagliate sull'app tra cui il punto finale nel cluster. Ciò in genere viene usato da uno sviluppatore di app per compilare un'app usando il client di swagger e usando il servizio Web per interagire con l'app in modalità RESTful.

Descrivono l'app eseguendo un comando simile al seguente:

```bash
mssqlctl app describe --name addpy --version v1
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
    "app": "https://10.1.1.3:30777/api/app/addpy/v1",
    "swagger": "https://10.1.1.3:30777/api/app/addpy/v1/swagger.json"
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

Prendere nota dell'indirizzo IP (`10.1.1.3` in questo esempio) e il numero di porta (`30777`) nell'output.

## <a name="generate-a-jwt-access-token"></a>Generare un token di accesso JWT

Per accedere al servizio web RESTful per l'app che è stata distribuita è necessario innanzitutto generare un token di accesso JWT. Aprire l'URL seguente nel browser: `https://[IP]:[PORT]/api/docs/swagger.json` usando l'indirizzo IP e porta è stato recuperato in esecuzione il `describe` comando precedente. Sarà necessario accedere con le stesse credenziali usate per `mssqlctl login`.

Incollare il contenuto del `swagger.json` nella [Editor Swagger](https://editor.swagger.io) comprendere quali metodi sono disponibili:

![Definizione Swagger dell'API](media/big-data-cluster-consume-apps/api_swagger.png)

Si noti che il `app` metodo GET, nonché `token` metodo POST. Poiché l'autenticazione per le app Usa i token JWT è necessario ottenere un token l'utilizzando lo strumento preferito per effettuare una chiamata POST per il `token` (metodo). Ecco un esempio di come eseguire questa operazione solo [Postman](https://www.getpostman.com/):

![Token di postman](media/big-data-cluster-consume-apps/postman_token.png)

Il risultato di questa richiesta viene visualizzato un token JWT `access_token`, che è necessario chiamare l'URL per eseguire l'app.

## <a name="execute-the-app-using-the-restful-web-service"></a>Eseguire l'app usando il servizio web RESTful

> [!NOTE]
> Se si desidera, è possibile aprire l'URL per il `swagger` che è stato restituito quando è stato eseguito `mssqlctl app describe --name [appname] --version [version]` nel browser, che dovrebbe essere simile a `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`. Sarà necessario accedere con le stesse credenziali usate per `mssqlctl login`. Il contenuto del `swagger.json` è possibile incollare [Editor Swagger](https://editor.swagger.io). Si noterà che il servizio web espone i `run` (metodo).

È possibile usare lo strumento preferito per chiamare il `run` metodo (`https://[IP]:[PORT]/api/app/[appname]/[version]/run`), passando i parametri nel corpo della richiesta POST come json. In questo esempio si userà [Postman](https://www.getpostman.com/). Prima di effettuare la chiamata, è necessario impostare il `Authorization` a `Bearer Token` e incollare il token recuperato in precedenza. Questo verrà impostato un'intestazione della richiesta. Vedere la schermata seguente.

![Postman eseguire intestazioni](media/big-data-cluster-consume-apps/postman_run_1.png)

Successivamente, nel corpo delle richieste, passare i parametri per l'app esegue la chiamata e impostare il `content-type` a `application/json`:

![Postman eseguire corpo](media/big-data-cluster-consume-apps/postman_run_2.png)

Quando si invia la richiesta, si otterrà lo stesso output quando è stata eseguita l'app `mssqlctl app run`:

![Risultato dell'esecuzione postman](media/big-data-cluster-consume-apps/postman_result.png)

A questo punto è stato chiamato correttamente l'app tramite il servizio web. È possibile seguire una procedura simile per integrare il servizio web nell'applicazione.

## <a name="next-steps"></a>Passaggi successivi

È anche possibile consultare esempi aggiuntivi in [esempi di distribuire App](https://aka.ms/sql-app-deploy).

Per altre informazioni sui cluster dei big data a SQL Server, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
