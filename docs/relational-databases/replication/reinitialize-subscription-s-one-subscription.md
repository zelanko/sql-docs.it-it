---
title: Reinizializza sottoscrizioni - Una sottoscrizione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c7992f3b9b27c219c2a28d226136442bddb2646f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767702"
---
# <a name="reinitialize-subscriptions---one-subscription"></a>Reinizializza sottoscrizioni - Una sottoscrizione
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La finestra di dialogo **Reinizializza sottoscrizioni** consente di contrassegnare una sottoscrizione per la reinizializzazione. La reinizializzazione implica l'applicazione di uno snapshot al Sottoscrittore e viene eseguita dall'agente di distribuzione per le sottoscrizioni di pubblicazioni transazionali e dall'agente di merge per le sottoscrizioni di pubblicazioni di tipo merge.  
  
## <a name="options"></a>Opzioni  
 **Usa lo snapshot corrente**  
 Selezionare questa opzione per applicare lo snapshot corrente al Sottoscrittore alla successiva esecuzione dell'agente di distribuzione o dell'agente di merge. Se non sono disponibili snapshot validi, questa opzione non può essere selezionata.  
  
 **Usa un nuovo snapshot**  
 Selezionare questa opzione per reinizializzare la sottoscrizione con un nuovo snapshot. Lo snapshot può essere applicato al Sottoscrittore solo dopo essere stato generato dall'agente snapshot. Se l'agente snapshot è impostato per essere eseguito in base a una pianificazione, la sottoscrizione non verrà reinizializzata se non dopo la successiva esecuzione dell'agente snapshot.  
  
 Per avviare l'agente snapshot immediatamente, selezionare **Genera il nuovo snapshot ora** .  
  
 **Carica le modifiche non sincronizzate prima della reinizializzazione**  
 Solo per la replica di tipo merge. Selezionare questa opzione per caricare le eventuali modifiche in sospeso dal database della sottoscrizione prima che i dati nel Sottoscrittore vengano sovrascritti con uno snapshot.  
  
 Se si aggiunge, elimina o modifica un filtro con parametri, le modifiche in sospeso nel Sottoscrittore non possono essere caricate nel server di pubblicazione durante la reinizializzazione. Per caricare le modifiche in sospeso, sincronizzare tutte le sottoscrizioni prima di modificare il filtro.  
  
 **Contrassegna per la reinizializzazione**  
 Fare clic su questo pulsante per contrassegnare la sottoscrizione per la reinizializzazione. Dopo aver verificato la disponibilità di uno snapshot valido, alla successiva esecuzione dell'agente di distribuzione o dell'agente di merge per la sottoscrizione viene applicato lo snapshot nel Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Reinizializzare le sottoscrizioni](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
