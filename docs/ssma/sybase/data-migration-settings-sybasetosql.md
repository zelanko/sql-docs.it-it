---
title: Impostazioni di migrazione dati (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9fcf6142a0df913c33782b4c65e8e95d4fcf91ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029382"
---
# <a name="data-migration-settings-sybasetosql"></a>Impostazioni di migrazione dei dati (SybaseToSQL)
  
## <a name="data-migration-settings"></a>Impostazioni di migrazione dei dati  
**Le impostazioni di migrazione dati** consente all'utente di scrivere query personalizzate per la migrazione dei dati.  
  
-   Questa scheda è disponibile quando **opzioni di migrazione dati estese** è impostata su **mostrano** e viene nascosto quando l'impostazione è impostata su **nascondere** nelle impostazioni del progetto. Per altre informazioni sulle impostazioni di progetto di migrazione, vedere [impostazioni progetto (migrazione)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924) .  
  
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
[Migrazione dei dati di Sybase a SQL Server/SQL Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
