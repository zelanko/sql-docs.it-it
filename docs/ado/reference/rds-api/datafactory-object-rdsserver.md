---
title: Oggetto DataFactory (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97597e15bc5cd8ee8d3008c97f3a4e8b07b2d43d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964328"
---
# <a name="datafactory-object-rdsserver"></a>Oggetto DataFactory (RDSServer)
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Questo oggetto di business sul lato server per impostazione predefinita implementa metodi che forniscono accesso ai dati di lettura/scrittura per le applicazioni lato client per origini dati specificate.  
  
 Il **RDSServer** oggetto è stato progettato come un oggetto di automazione sul lato server che riceve le richieste client. In un'implementazione di Internet, lo si trova in un server Web e viene creata un'istanza dal componente ADISAPI. Il **RDSServer** oggetto offre lettura e accesso in scrittura ai dati specificati origini, ma non contiene alcuna logica di regole di convalida o business.  
  
 Se si usa un metodo che è disponibile in entrambe le **RDSServer** e [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetti, Remote Data Service Usa la **Servizi Desktop remoto. DataControl** versione per impostazione predefinita. Il valore predefinito presuppone uno scenario di programmazione di base, in cui il **RDSServer** funge da un oggetto generico business sul lato server.  
  
 Se si desidera che l'applicazione Web per gestire l'elaborazione sul lato server specifici dell'attività, è possibile sostituire il **RDSServer** con un oggetto business personalizzato.  
  
 È possibile creare oggetti business sul lato server che chiamano il **RDSServer** metodi, ad esempio [Query](../../../ado/reference/rds-api/query-method-rds.md) e [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Ciò è utile se si desidera aggiungere funzionalità a oggetti business, ma è possibile sfruttare le tecnologie esistenti di servizio dati remoto.  
  
 Il **DataFactory** oggetto non è sicuro per gli script eseguiti sul lato client.  
  
 L'ID della classe per il **RDSServer** oggetto è il D 9381D8F5-0288-11 0-9501-00AA00B911A5.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di oggetto DataFactory, metodo Query e metodo CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


