---
title: 'Lezione 2: Preparazione della cartella snapshot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bbe571002a1168ca3f60592b86fb58fd482ecd05
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000420"
---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>Lezione 2: Preparazione della cartella snapshot
  In questa lezione verrà configurata la cartella snapshot utilizzata per la creazione e l'archiviazione dello snapshot di pubblicazione.  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>Per creare una condivisione per la cartella snapshot e assegnare le autorizzazioni  
  
1.  In Esplora risorse passare alla cartella di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il percorso predefinito è C:\Programmi\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Creare una nuova cartella denominata **repldata**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Proprietà**.  
  
4.  Nella scheda **Condivisione** della finestra di dialogo **Proprietà di repldata** fare clic su **Condividi**.  
  
5.  Nella finestra di dialogo **Condivisione file** fare clic su **Condividi**e quindi su **Chiudi**.  
  
6.  Nella scheda **Sicurezza** fare clic su **Modifica**.  
  
7.  Nella finestra di dialogo **Autorizzazioni** fare clic su **Aggiungi**. Nella casella di testo **Seleziona utente, computer, account servizio o gruppi** Digitare il nome dell'account agente di snapshot creato nella lezione 1, come \< _Machine_Name>_ **\ repl_snapshot**, dove \< *Machine_Name>* è il nome del server di pubblicazione. Fare clic su **Controlla nomi** e quindi su **OK**.  
  
8.  Ripetere il passaggio precedente per aggiungere le autorizzazioni per il agente di distribuzione, come \< _Machine_Name>_ **\ repl_distribution**e per il agente di merge Machine_Name \< _>_ **\ repl_merge**.  
  
9. Verificare che siano state concesse le autorizzazioni seguenti:  
  
    -   repl_snapshot - Controllo completo  
  
    -   repl_distribution - Lettura  
  
    -   repl_merge - Lettura  
  
10. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà di repldata** e creare la condivisione repldata.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo è stata configurata la condivisione per la cartella snapshot. Il passaggio successivo consiste nella configurazione della distribuzione. Vedere [Lezione 3: Configurazione della distribuzione](lesson-3-configuring-distribution.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md)  
  
  
