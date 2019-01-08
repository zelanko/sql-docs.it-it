---
title: Backup e ripristino di server di pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 911d0a740a20f74edf9e32d4a6ff69a8d6040f24
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756263"
---
# <a name="backup-and-restore-for-oracle-publishers"></a>Backup e ripristino di server di pubblicazione Oracle
  Durante il backup e il ripristino, attenersi alle linee guida seguenti:  
  
-   Verificare che l'agente di lettura log non sia in esecuzione e che non siano in corso altre attività di database sulle tabelle pubblicate durante il backup del server di pubblicazione.  
  
-   Eseguire il backup del server di pubblicazione e del server di distribuzione contemporaneamente.  
  
-   Se è necessario ripristinare il server di pubblicazione o il server di distribuzione, reinizializzare tutte le sottoscrizioni.  
  
-   Per ripristinare un Sottoscrittore da un backup senza reinizializzarne le sottoscrizioni, devono essere ancora disponibili le transazioni recapitate al database di distribuzione dopo il completamento dell'ultimo backup del database di sottoscrizione. Il periodo di tempo in cui sono disponibili le transazioni dipende dalle impostazioni di memorizzazione per la distribuzione. Per informazioni su queste impostazioni, vedere [Scadenza e disattivazione delle sottoscrizioni](../subscription-expiration-and-deactivation.md).  
  
-   Se il server di pubblicazione o il server di distribuzione risulta non sincronizzato in seguito a un ripristino di database, gli agenti di replica registrano messaggi di errore. A questo punto, è necessario eliminare e ricreare tutte le pubblicazioni e le sottoscrizioni significative:  
  
    1.  Creare script per la definizione delle pubblicazioni e delle sottoscrizioni. Per altre informazioni, vedere [Scripting Replication](../scripting-replication.md).  
  
         Se la definizione delle pubblicazioni è stata modificata tra le versioni degli stati del server di pubblicazione e del server di distribuzione, sarà necessario modificare gli script.  
  
    2.  Eliminare le pubblicazioni e le sottoscrizioni.  
  
    3.  Eseguire gli script creati nel passaggio 1.  
  
     Se è necessario eliminare e riconfigurare il server di pubblicazione, eliminare il sinonimo public **MSSQLSERVERDISTRIBUTOR** e l'utente di replica Oracle configurato con l'opzione **CASCADE** per rimuovere tutti gli oggetti di replica dal server di pubblicazione Oracle.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup e ripristino di database replicati](../administration/back-up-and-restore-replicated-databases.md)   
 [Configurare un server di pubblicazione Oracle](configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](oracle-publishing-overview.md)  
  
  
