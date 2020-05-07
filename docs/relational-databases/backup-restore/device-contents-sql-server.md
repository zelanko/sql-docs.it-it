---
title: Contenuto dispositivo (SQL Server) | Microsoft Docs
description: In SQL Server usare la finestra di dialogo Contenuto dispositivo per visualizzare le informazioni di backup che descrivono il dispositivo, i supporti, il set di supporti e il set o i set di backup.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.bnrdevicecontents.f1
ms.assetid: 95e1902e-8c7a-4830-bdf9-1a6aca414a24
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1c9819b7853121c006180d0a988dbc83e905505f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "82179187"
---
# <a name="device-contents-sql-server"></a>Contenuto dispositivo (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa finestra di dialogo per visualizzazione le informazioni di backup. Vengono riportate informazioni sul dispositivo, sui supporti, sul set di supporti e sul set o i set di backup.  
  
 **Per utilizzare SQL Server Management Studio per visualizzare il contenuto di un dispositivo di backup**  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opzioni  
 **Supporti**  
 Disco o set di nastri in cui sono archiviate le informazioni di backup.  
  
 **Sequenza supporti**  
 Consente di visualizzare il numero di sequenza dei supporti, il numero di sequenza del gruppo e l'identificatore del mirror, se disponibili. Ogni supporto di backup fisico è contrassegnato con un numero di sequenza dei supporti che indica l'ordine in cui i supporti sono stati utilizzati. Il supporto di backup iniziale è contrassegnato con 1, il secondo supporto, ovvero il primo nastro di continuità, con 2 e così via. Durante il ripristino del set di backup, i numeri di sequenza dei supporti consentono all'operatore che esegue il ripristino del backup di caricare i supporti in base all'ordine corretto.  
  
 **Data creazione**  
 Visualizza la data dei supporti.  
  
 **Set di supporti**  
 Un set di supporti consiste in una raccolta ordinata di supporti di backup sui quali è stata eseguita la scrittura di una o più operazioni di backup utilizzando un numero costante di dispositivi di backup.  
  
 **Nome**  
 Visualizza il nome del set di supporti.  
  
 **Descrizione**  
 Visualizza la descrizione del set di supporti.  
  
 **Conteggio gruppo di supporti**  
 Visualizza il conteggio del gruppo di supporti. Ogni set di supporti è un insieme formato da uno o più gruppi di supporti. L'output per un determinato dispositivo di backup individuale o per un gruppo di dispositivi di backup con mirroring forma un gruppo di supporti distinto. Ogni set di supporti contiene un gruppo di supporti per un dispositivo distinto o per un gruppo di dispositivi con mirroring. Ad esempio, se un set di supporti utilizza due dispositivi di backup senza mirroring, il set di supporti conterrà due gruppi di supporti.  
  
 **Set di backup**  
 Visualizza informazioni sul set o i set di backup contenuti nel supporto. Un set di backup è il risultato di un'operazione di backup riuscita, il cui contenuto viene distribuito tra i supporti del set di dispositivi di backup.  
  
|Intestazione|Valori|  
|------------|------------|  
|**Nome**|Nome del set di backup.|  
|**Tipo**|Tipo di operazione di backup eseguita: Completo, Differenziale o Log delle transazioni.|  
|**Componente**|Componente di cui è stato eseguito il backup: database, file o *\<vuoto>* , nel caso dei log delle transazioni.|  
|**Server**|Nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ha eseguito l'operazione di backup.|  
|**Database**|Nome del database di cui è stato eseguito il backup.|  
|**Posizione**|Posizione del set di backup nel volume.|  
|**Data**|Data e ora di fine dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.|  
|**Dimensione**|Dimensioni in byte del set di backup.|  
|**Nome utente**|Nome dell'utente che ha eseguito l'operazione di backup.|  
|**Scadenza**|Data e ora di scadenza del set di backup.|  
  
## <a name="see-also"></a>Vedere anche  
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
