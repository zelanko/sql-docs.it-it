---
title: Impostazioni di migrazione dei dati (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: b86114566be6b560aa571f15af1e3dfac3e59501
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934879"
---
# <a name="data-migration-settings-oracletosql"></a>Impostazioni di migrazione dei dati (OracleToSQL)
  
## <a name="data-migration-settings"></a>Impostazioni di migrazione dei dati  
**Le impostazioni di migrazione dei dati** consentono all'utente di scrivere query personalizzate per la migrazione dei dati.  
  
-   Questa scheda è disponibile quando le **Opzioni di migrazione dei dati estese** sono impostate su **Mostra** ed è nascosta quando l'impostazione è impostata su **Nascondi** in Impostazioni progetto. Per ulteriori informazioni sulle impostazioni di migrazione del progetto, vedere [Impostazioni progetto (migrazione)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
-   L'analisi delle istruzioni SQL personalizzate verrà implementata nella scheda **Impostazioni migrazione dati** del nodo tabella.  
  
-   Di seguito sono riportate le due caselle di controllo disponibili nelle **impostazioni di migrazione dei dati** :  
  
    1.  Tronca SQL Server tabella  
  
    2.  Usa selezione personalizzata  
  
1.  **Tronca SQL Server tabella:**  
     Questa opzione consente all'utente di avere una visualizzazione chiara dei dati migrati nel database di destinazione.  
  
    -   Per impostazione predefinita, questa casella di testo è selezionata.  
  
    -   Se questa casella di testo è deselezionata, i dati di cui viene eseguita la migrazione verranno aggiunti ai dati esistenti nel database di destinazione.  
  
2.  **Usa selezione personalizzata:**  
     Questa opzione consente all'utente di modificare l'istruzione **Select** presente. l'istruzione**SELECT** consente agli utenti di selezionare i dati da visualizzare nel database di destinazione.  
  
    1.  Per impostazione predefinita, questa casella di testo è deselezionata.  
  
    2.  Se questa casella di testo è selezionata, consente agli utenti di modificare l'istruzione **Select** presente.  
  
Sono presenti due pulsanti, vale a dire:  
  
-   **Applica:** Fare clic su **applica** per applicare le impostazioni modificate.  
  
-   **Annulla:** Fare clic su **Annulla** per ripristinare le impostazioni presenti prima che siano state apportate le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di dati Oracle a SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)  
  
