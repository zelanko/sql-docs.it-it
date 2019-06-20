---
title: Modello di programmazione RDS di base | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4b8f08cda158c21d556b251d3e141b333418ca38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704354"
---
# <a name="basic-rds-programming-model"></a>Modello di programmazione RDS di base
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Servizi Desktop remoto consente di risolvere applicazioni esistenti nel seguente ambiente: Un'applicazione client specifica un programma che verrà eseguito su un server e i parametri necessari per restituire le informazioni desiderate. Il programma richiamato sul server ottiene accesso all'origine dati specificata, recupera le informazioni facoltativamente elabora i dati e quindi restituisce le informazioni risultanti per l'applicazione client in un formato che può facilmente utilizzare. Servizi Desktop remoto fornisce i mezzi per eseguire la sequenza di azioni seguente:  
  
-   Specificare il programma da richiamare sul server e ottenere un modo per farvi riferimento dal client. (Questo riferimento viene chiamato talvolta un *proxy*. Rappresenta il programma del server remoto. L'applicazione client "chiamerà" proxy come se fosse un programma locale, ma richiama effettivamente il programma del server remoto.)  
  
-   Richiamare il programma del server. Passare parametri all'applicazione server che identificano l'origine dati e il comando da eseguire. (Il programma del server utilizza effettivamente ADO per accedere all'origine dati. ADO esegue una connessione con uno dei parametri specificati e quindi rilascia il comando specificato nel parametro other.)  
  
-   L'applicazione server Ottiene un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto dall'origine dati. Facoltativamente, il **Recordset** oggetto viene elaborato nel server.  
  
-   Il programma del server restituisce l'elemento finale **Recordset** oggetto all'applicazione client.  
  
-   Sul client, il **Recordset** oggetto viene inserito in un form che può essere facilmente utilizzato dai controlli visual.  
  
-   Eventuali modifiche per il **Recordset** oggetto vengono inviate nuovamente al programma server, che li utilizza per aggiornare l'origine dati.  
  
 Questo modello di programmazione contiene alcune comode funzionalità. Se non è necessario un programma server complessi per accedere all'origine dati e se si forniscono le connessioni necessarie e i parametri di comando, servizi desktop remoto verrà automaticamente recuperare i dati con un semplice programma server predefinito specificati.  
  
 Se è necessaria un'elaborazione più complessa, è possibile specificare un'applicazione server personalizzata. Ad esempio, poiché un'applicazione server personalizzata dispone di tutta la potenza di ADO a sua disposizione, è stato possibile connettersi a più origini dati diverse, combinare i dati in qualche modo complesso e quindi restituire un risultato elaborato semplice all'applicazione client.  
  
 Infine, se le proprie esigenze sono compreso tra da qualche parte, ADO supporta ora la personalizzazione del comportamento del programma server predefinito.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello di programmazione RDS in dettaglio](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS Scenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


