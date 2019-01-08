---
title: Verificare i problemi di ritardo di I/O nel sottosistema di I/O del disco | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7ff6a91f14242d79c3fec543632f74eeb9f452bd
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354811"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Verifica dei problemi di ritardo di I/O nel sottosistema di I/O del disco
  Questa regola consente di controllare il messaggio di errore 833 nel registro eventi. Questo messaggio indica che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha eseguito una richiesta di lettura o scrittura dal disco e che la durata dell'operazione è stata superiore a 15 secondi. Questo errore viene segnalato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica un problema relativo al sottosistema di I/O. Ritardi così prolungati possono influire gravemente sulle prestazioni dell'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Per risolvere il problema che ha causato questo errore, individuare nel registro eventi di sistema i messaggi di errore correlati all'hardware. Esaminare inoltre eventuali log specifici dei componenti hardware se disponibili.  
  
 Utilizzare Performance Monitor per esaminare i contatori seguenti:  
  
-   Media secondi/trasf. disco  
  
-   Lunghezza media coda del disco  
  
-   Lunghezza corrente coda del disco  
  
 Il valore della durata media, ad esempio, di Disco sec/trasferimento in un computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in genere inferiore a 15 millisecondi. L'aumento di tale valore indica che il sottosistema di I/O del disco non è in grado di soddisfare in modo ottimale le richieste di I/O.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [MSSQLSERVER_833](../errors-events/mssqlserver-833-database-engine-error.md)  
  
 [Articolo 897284 della Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [SQL Server I/O Basics, Chapter 2](https://go.microsoft.com/fwlink/?LinkId=69370)  
  
  
