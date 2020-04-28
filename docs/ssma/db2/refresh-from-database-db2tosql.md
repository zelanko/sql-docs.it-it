---
title: Aggiornare dal database (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a53c3005aca2e599d8ceb0b973a58bcf2ca5e14c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060136"
---
# <a name="refresh-from-database-db2tosql"></a>Aggiornamento dal database (DB2ToSQL)
La finestra di dialogo **Aggiorna da database** consente di selezionare gli oggetti da aggiornare dal database DB2. Le righe nella finestra di dialogo sono codificate a colori in base allo stato dei metadati:  
  
-   Se i metadati dell'oggetto sono stati modificati localmente e nel database DB2, la riga è blu.  
  
-   Se i metadati dell'oggetto sono stati modificati nel database DB2 ma non in SSMA, la riga è gialla.  
  
-   Se i metadati dell'oggetto sono stati modificati in locale, ma non nel database DB2, la riga è verde.  
  
-   Se l'oggetto è nuovo nel database DB2, la riga è rosa.  
  
È possibile specificare le impostazioni di aggiornamento oggetti predefinite nella finestra di dialogo **Impostazioni progetto** . Per altre informazioni, vedere [Impostazioni progetto&#40;sincronizzazione&#41; &#40;&#41;DB2ToSQL ](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Per accedere alla finestra di dialogo **Aggiorna da database** , fare clic con il pulsante destro del mouse su un oggetto in DB2 Metadata Explorer e scegliere **Aggiorna da database**.  
  
## <a name="options"></a>Opzioni  
**Comprimi (-)**  
Comprime tutti i gruppi di oggetti per nascondere i singoli oggetti.  
  
**Espandi (+)**  
Espandere tutti i gruppi di oggetti per visualizzare i singoli oggetti.  
  
**Nascondi/Mostra oggetti uguali**  
Nasconde gli oggetti dall'elenco se i metadati dell'oggetto sono gli stessi nel database DB2 e in SSMA.  
  
**Aggiorna da database (pulsante freccia)**  
Usare il pulsante freccia per specificare che i metadati per gli oggetti selezionati devono essere aggiornati in SSMA.  
  
**Non aggiornare dal database (pulsante X)**  
Usare il pulsante X per specificare che i metadati per gli oggetti selezionati non devono essere aggiornati in SSMA.  
  
**Legenda**  
Consente di visualizzare una finestra di dialogo **Legenda** . La legenda contiene il mapping tra i colori delle righe e gli Stati dei metadati.  
  
Per lasciare la finestra di dialogo **Legenda** nella parte superiore della finestra di dialogo **Aggiorna da database** , selezionare la casella di controllo **Mostra in primo piano** .  
  
