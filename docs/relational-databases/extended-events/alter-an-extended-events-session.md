---
title: Modificare una sessione Eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cedb0addec5d6164b418b6bec0458de429dd6a82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66198205"
---
# <a name="alter-an-extended-events-session"></a>Modificare una sessione Eventi estesi

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Dopo avere creato una sessione Eventi estesi, è possibile modificarla secondo necessità utilizzando la **Creazione guidata Eventi estesi di SQL Server**.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Non è possibile modificare una destinazione per sessioni attive e inattive né modificare le configurazioni delle proprietà avanzate per una sessione attiva.  
  
 È possibile apportare le modifiche seguenti alle sessioni di eventi attive e inattive:  
  
-   Aggiungere o rimuovere eventi dalla sessione e modificare le configurazioni degli eventi, ad esempio campi evento, filtri e azioni.  
  
-   Aggiungere o rimuovere una destinazione dalla sessione eventi.  
  
-   Abilitare l'opzione **Avvia la sessione eventi all'avvio del server** .  
  
 È possibile apportare le modifiche aggiuntive seguenti a una sessioni eventi inattiva:  
  
-   Abilitare l'opzione **Rileva la relazione tra gli eventi** .  
  
-   Modificare la configurazione delle proprietà avanzate.  
  
> [!NOTE]  
>  La **Creazione guidata eventi estesi di SQL Server** non supporta la modifica delle sessioni evento.  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>Modifica di una sessione Eventi estesi utilizzando la Creazione guidata Eventi estesi SQL Server  
  
-   In Esplora oggetti espandere **Gestione**, **Eventi estesi**, quindi **Sessioni**.  
  
-   Fare clic con il pulsante destro del mouse sulla sessione che si vuole modificare, quindi scegliere **Proprietà**.  
  
-   Nella finestra di dialogo **Proprietà** apportare le modifiche desiderate, quindi fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [Creare una sessione Eventi estesi tramite l'editor di query](quick-start-extended-events-in-sql-server.md)  
  
  
