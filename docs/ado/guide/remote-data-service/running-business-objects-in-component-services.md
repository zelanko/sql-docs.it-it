---
title: Esecuzione di oggetti Business in Servizi componenti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f64909f4f7db1f765d233878631eb90a4760531e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704205"
---
# <a name="running-business-objects-in-component-services"></a>Esecuzione di oggetti business nei Servizi componenti
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Gli oggetti business possono essere file eseguibili (.exe) o librerie a collegamento dinamico (DLL). La configurazione utilizzata per eseguire l'oggetto business dipende dal fatto che l'oggetto è un file con estensione dll o .exe:  
  
-   Gli oggetti business creati come file .exe possono essere chiamati tramite DCOM. Se vengono utilizzati tramite Internet Information Services (IIS), sono soggetti a marshalling aggiuntiva dei dati, con conseguente rallentano delle prestazioni dei client.  
  
-   Gli oggetti business creati come file con estensione DLL possono essere usati tramite IIS e pertanto anche tramite HTTP. Possono inoltre essere utilizzati su DCOM solo tramite Servizi componenti o tramite Microsoft Transaction Server, se si utilizza Windows NT. Oggetto business dll dovrà essere registrata nel computer del server IIS per accedere a essi tramite IIS. Per informazioni su come configurare un file DLL per l'esecuzione su DCOM, vedere la sezione [attivazione di una DLL per l'esecuzione su DCOM](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Quando gli oggetti business nel livello intermedio vengono implementati come componenti di Servizi componenti usando **GetObjectContext**, **SetComplete**, e **SetAbort**, l'azienda gli oggetti possono utilizzare Servizi componenti (o MTS, se si utilizza Windows NT) gli oggetti di contesto per mantenere il proprio stato tra più chiamate del client. Questo scenario è possibile eseguire con DCOM, che viene in genere implementata tra client e server in una rete intranet attendibili. In questo caso, il [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetto e [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) metodo sul lato client vengono sostituiti dall'oggetto di contesto di transazione e **CreateInstance** (metodo), che vengono forniti dal **ITransactionContext** interfaccia e implementati da Servizi componenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


