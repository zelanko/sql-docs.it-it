---
title: Impostazioni di migrazione dati (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 2b435b02060d32e61bc3e75054171023262a87b8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264209"
---
# <a name="data-migration-settings-oracletosql"></a>Impostazioni di migrazione dei dati (OracleToSQL)
  
## <a name="data-migration-settings"></a>Impostazioni di migrazione dei dati  
**Le impostazioni di migrazione dati** consente all'utente di scrivere query personalizzate per la migrazione dei dati.  
  
-   Questa scheda è disponibile quando **opzioni di migrazione dati estese** è impostata su **mostrano** e viene nascosto quando l'impostazione è impostata su **nascondere** nelle impostazioni del progetto. Per altre informazioni sulle impostazioni di progetto di migrazione, vedere [impostazioni progetto (migrazione)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
-   L'analisi delle istruzioni SQL personalizzate verranno implementato in **le impostazioni di migrazione dati** scheda del nodo della tabella.  
  
-   Di seguito sono le due caselle di controllo disponibili nel **le impostazioni di migrazione dati** una visualizzazione dei.:  
  
    1.  Troncare la tabella di SQL Server  
  
    2.  Selezionare utilizzo personalizzato  
  
1.  **Troncare la tabella di SQL Server:**  
     Questa opzione consente all'utente di avere una visione chiara dei dati migrati a livello di database di destinazione.  
  
    -   Per impostazione predefinita, viene selezionata questa casella di testo.  
  
    -   Se questa casella è deselezionata, verranno aggiunti i dati che viene eseguita la migrazione a quelli esistenti nel database di destinazione.  
  
2.  **Selezionare utilizzo personalizzato:**  
     Questa opzione consente all'utente di modificare la **selezionate** istruzione presente (**seleziona** istruzione consente agli utenti di selezionare i dati da visualizzare a livello di database di destinazione).  
  
    1.  Per impostazione predefinita, questa casella è deselezionata.  
  
    2.  Se è selezionata questa casella di testo e quindi consente agli utenti di modificare la **seleziona** istruzione presente.  
  
Esistono due pulsanti presenti una visualizzazione dei.:  
  
-   **Applicare:** Fare clic su **applica** per applicare le impostazioni che sono state modificate.  
  
-   **Annulla:** Fare clic su **annullare** per ripristinare le impostazioni presente prima che le modifiche sono state apportate.  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione dei dati di Oracle a SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)  
  
