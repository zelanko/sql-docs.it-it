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
author: rothja
ms.author: jroth
ms.openlocfilehash: 441d3f9f2de12e269839c3561dd0d202121018be
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750183"
---
# <a name="basic-rds-programming-model"></a>Modello di programmazione RDS di base
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS indirizza le applicazioni presenti nell'ambiente seguente: un'applicazione client specifica un programma che verrà eseguito in un server e i parametri necessari per restituire le informazioni desiderate. Il programma richiamato sul server ottiene l'accesso all'origine dati specificata, recupera le informazioni, elabora facoltativamente i dati e quindi restituisce le informazioni risultanti all'applicazione client in un modulo che può essere facilmente utilizzato. RDS fornisce i mezzi per eseguire la sequenza di azioni seguente:  
  
-   Specificare il programma da richiamare sul server e ottenere un modo per farvi riferimento dal client. Questo riferimento è talvolta denominato *proxy*. Rappresenta il programma server remoto. L'applicazione client chiamerà il proxy come se fosse un programma locale, ma richiama effettivamente il programma server remoto.  
  
-   Richiamare il programma server. Passare i parametri al programma server che identificano l'origine dati e il comando da emettere. Il programma server utilizza effettivamente ADO per ottenere l'accesso all'origine dati. ADO crea una connessione con uno dei parametri specificati, quindi emette il comando specificato nell'altro parametro.  
  
-   Il programma server ottiene un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dall'origine dati. Facoltativamente, l'oggetto **Recordset** viene elaborato nel server.  
  
-   Il programma server restituisce l'oggetto **Recordset** finale all'applicazione client.  
  
-   Nel client, l'oggetto **Recordset** viene inserito in un modulo che può essere facilmente utilizzato dai controlli visivi.  
  
-   Tutte le modifiche all'oggetto **Recordset** vengono restituite al programma server, che le utilizza per aggiornare l'origine dati.  
  
 Questo modello di programmazione contiene alcune funzionalità di praticità. Se non è necessario un programma server complesso per accedere all'origine dati e se si specificano i parametri di connessione e comando necessari, Servizi Desktop remoto recupererà automaticamente i dati specificati con un semplice programma server predefinito.  
  
 Se è necessaria un'elaborazione più complessa, è possibile specificare un programma server personalizzato. Poiché, ad esempio, un programma server personalizzato ha tutta la potenza di ADO a sua disposizione, può connettersi a diverse origini dati, combinare i dati in modo complesso e quindi restituire un risultato semplice e elaborato all'applicazione client.  
  
 Infine, se le esigenze si trovano in un punto qualsiasi, ADO supporta ora la personalizzazione del comportamento del programma server predefinito.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello di programmazione RDS in dettaglio](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [Scenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Oggetto recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


