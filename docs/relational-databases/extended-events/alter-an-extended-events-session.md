---
title: Modificare una sessione Eventi estesi
description: Usare la Creazione guidata Eventi estesi SQL Server per modificare una sessione Eventi estesi. Le modifiche che è possibile apportare variano a seconda che la sessione sia attiva o inattiva.
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ad23756f19dd2305215ed7e44f52e65f5e52f74
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465602"
---
# <a name="alter-an-extended-events-session"></a>Modificare una sessione Eventi estesi

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Dopo avere creato una sessione Eventi estesi, è possibile modificarla secondo necessità utilizzando la **Creazione guidata Eventi estesi di SQL Server**.  
  
## <a name="before-you-begin"></a>Operazioni preliminari  
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
  
  
