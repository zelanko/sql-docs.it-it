---
title: Verifica dei problemi di ritardo di I/O nel sottosistema di I/O del disco
description: Informazioni su come abilitare i criteri per verificare nel sottosistema di IO del disco la presenza di problemi di ritardo di I/O controllando nel registro eventi il messaggio di errore 833 per la gestione basata su criteri con SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f8c880438491f697d57134b5004129eef38a7fe8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749512"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Verifica dei problemi di ritardo di I/O nel sottosistema di I/O del disco
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questa regola consente di controllare il messaggio di errore 833 nel registro eventi. Questo messaggio indica che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha eseguito una richiesta di lettura o scrittura dal disco e che la durata dell'operazione è stata superiore a 15 secondi. Questo errore viene segnalato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica un problema relativo al sottosistema di I/O. Ritardi così prolungati possono influire gravemente sulle prestazioni dell'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Per risolvere il problema che ha causato questo errore, individuare nel registro eventi di sistema i messaggi di errore correlati all'hardware. Esaminare inoltre eventuali log specifici dei componenti hardware se disponibili.  
  
 Utilizzare Performance Monitor per esaminare i contatori seguenti:  
  
-   Media secondi/trasf. disco  
  
-   Lunghezza media coda del disco  
  
-   Lunghezza corrente coda del disco  
  
 Il valore della durata media, ad esempio, di Disco sec/trasferimento in un computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in genere inferiore a 15 millisecondi. L'aumento di tale valore indica che il sottosistema di I/O del disco non è in grado di soddisfare in modo ottimale le richieste di I/O.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
   
  
 [Articolo 897284 della Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))
