---
title: Attivazione di una DLL per l'esecuzione su DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ccfb1189e0c4d9bb0b1684ac3fd47709f491cd48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704560"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Abilitazione di un file DLL per l'esecuzione su DCOM
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 I passaggi seguenti illustrano come abilitare una DLL di oggetti business di utilizzare DCOM e Microsoft Internet Information Services (HTTP) tramite Servizi componenti.  
  
1.  Creare un nuovo pacchetto vuoto nello snap-in MMC Servizi componenti.  
  
     Si userà lo snap-in MMC Servizi componenti per creare un pacchetto e aggiungere la DLL nel pacchetto. In questo modo il file DLL accessibili tramite DCOM, ma rimuove l'accessibilità tramite IIS. (Se si archivia il Registro di sistema per il file DLL, il **Inproc** chiave corrisponde a vuota, impostando l'attributo di attivazione, descritto più avanti in questo argomento, viene aggiunto un valore nel **Inproc** chiave.)  
  
2.  Installare un oggetto business nel pacchetto.  
  
     oppure  
  
     Importa i [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto nel pacchetto.  
  
3.  Impostare l'attributo di attivazione per il pacchetto **nel processo di creazione** (applicazione di libreria).  
  
     Per rendere il file DLL accessibili tramite DCOM e IIS nello stesso computer, è necessario impostare l'attributo di attivazione del componente snap-in MMC Servizi componenti. Dopo aver impostato l'attributo su **nel processo di creazione**, si noterà che un' **Inproc** chiave server nel Registro di sistema è stato aggiunto che punta a un componente di servizi di surrogati. dll.  
  
 Per altre informazioni sui servizi componenti (o del servizio Microsoft Transaction, se si utilizza Windows NT) e su come eseguire questi passaggi, visitare il sito Web di Microsoft Transaction Server.


