---
title: Impostazioni di migrazione dei dati (SybaseToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029382"
---
# <a name="data-migration-settings-sybasetosql"></a>Impostazioni di migrazione dei dati (SybaseToSQL)
  
## <a name="data-migration-settings"></a>Impostazioni di migrazione dei dati  
**Le impostazioni di migrazione dei dati** consentono all'utente di scrivere query personalizzate per la migrazione dei dati.  
  
-   Questa scheda è disponibile quando le **Opzioni di migrazione dei dati estese** sono impostate su **Mostra** ed è nascosta quando l'impostazione è impostata su **Nascondi** in Impostazioni progetto. Per ulteriori informazioni sulle impostazioni di migrazione del progetto, vedere [Impostazioni progetto (migrazione)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924) .  
  
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
[Migrazione di dati Sybase a SQL Server/SQL Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
