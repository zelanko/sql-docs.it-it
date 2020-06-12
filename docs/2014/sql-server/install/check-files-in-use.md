---
title: Controllare i file in uso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccd65867-d4c0-43b2-8361-7fd41c6f79ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3610ad08d34942dd7dbc1af1371a6c5d86e7890
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83856608"
---
# <a name="check-files-in-use"></a>Controllo file in uso
  Per evitare il riavvio di Windows dopo l'installazione degli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizzare la pagina Controllo file in uso per identificare i processi che bloccano i file necessari per il programma di installazione degli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Arrestare tutti i servizi e le applicazioni che si connettono alle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da aggiornare, Arrestare anche [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Se vengono rilevati file bloccati durante l'installazione, potrebbe essere necessario riavviare il computer al termine dell'installazione. In questo caso, verrà richiesto di riavviare il computer. Se durante l'installazione degli aggiornamenti è necessario arrestare un determinato servizio, al termine dell'installazione tale servizio verrà riavviato automaticamente.  
  
 Per eliminare la necessità di riavviare il computer dopo l'installazione, verrà visualizzato un elenco dei processi che bloccano i file necessari. Arrestare o terminare i processi e le applicazioni elencati. Fare clic su **Aggiorna controllo** per ripetere il controllo. Per arrestare un controllo in esecuzione, fare clic su **Arresta controllo** . Se non vengono rilevati file bloccati, la tabella risulta vuota. Dopo la chiusura o l'arresto di tutti i processi bloccati, fare clic su **Avanti** per continuare.  
  
 Le informazioni verranno registrate nei file di log. Per altre informazioni sulla visualizzazione dei file di log, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md) e [Procedura: Lettura di un file di log del programma di installazione di SQL Server](https://go.microsoft.com/fwlink/?LinkID=134490).  
  
 Nel file di log sono incluse le seguenti informazioni:  
  
-   Nome del processo  
  
-   Nome della caratteristica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Tipo di processo  
  
-   Account con il quale viene eseguito il processo  
  
-   ID di processo  
  
-   Nome del file bloccato  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
  
|Nome|Descrizione|  
|----------|-----------------|  
|Processo|Indica il nome completo del processo che utilizza i file da aggiornare.|  
|Tipo|Indica il tipo di processo.|  
|Account|Indica l'account con il quale viene eseguito il processo.|  
|ID di processo|Indica l'ID del processo.|  
  
  
