---
title: Creare, eliminare o modificare un ruolo (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 703615793c1c9ced7252a03e7597b701c977fbdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306553"
---
# <a name="create-delete-or-modify-a-role-management-studio"></a>Creare, eliminare o modificare un ruolo (Management Studio)
  In Reporting Services sono disponibili ruoli predefiniti che definiscono un livello di accesso a un server di report. La richiesta di accesso al server di report da parte di ogni utente o gruppo viene effettuata tramite un ruolo che descrive le attività che possono essere eseguite. I ruoli vengono definiti per il server di report complessivamente. Non è possibile variare una definizione di ruolo per parti specifiche del server di report o specificare che un ruolo venga utilizzato in modo diverso a seconda delle circostanze.  
  
 Per creare, modificare o eliminare ruoli, usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È possibile eliminare solo ruoli che non sono utilizzati.  
  
 Per assegnare utenti e gruppi ai ruoli creati, utilizzare Gestione report. Per altre informazioni, vedere [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](grant-user-access-to-a-report-server.md).  
  
> [!NOTE]  
>  Se il server di report è configurato per la modalità integrata SharePoint e si è connessi al sito di SharePoint con cui il server di report è integrato, è possibile visualizzare e modificare i livelli di autorizzazione che controllano l'accesso al contenuto e alle operazioni del server di report.  
  
### <a name="to-create-a-role-definition"></a>Per creare una definizione di ruolo  
  
1.  Espandere il nodo di un server di report in Esplora oggetti.  
  
2.  Espandere la cartella sicurezza.  
  
3.  Per creare una definizione di ruolo a livello di elemento, fare clic con il pulsante destro del mouse su **Ruoli**e scegliere **Nuovo ruolo**.  
  
     Se invece si vuole creare una definizione di ruolo a livello di sistema, fare clic con il pulsante destro del mouse su **Ruoli a livello di sistema**e scegliere **Nuovo ruolo a livello di sistema**.  
  
4.  Digitare un nome univoco per il ruolo. Il nome deve includere almeno un carattere. È inoltre possibile utilizzare spazi e alcuni simboli, con l'esclusione dei caratteri ; ? : \@ & = +, $ / * \< > | "o /.  
  
5.  Se lo si desidera, digitare una descrizione. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] questa descrizione verrà visualizzata solo in questa pagina. Gli utenti che visualizzeranno l'elemento in Gestione report potranno leggere la descrizione.  
  
6.  Selezionare le attività che i membri del ruolo potranno eseguire.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>Per eliminare o modificare una definizione di ruolo  
  
1.  Espandere il nodo di un server di report in Esplora oggetti.  
  
2.  Espandere la cartella sicurezza.  
  
3.  Per eliminare o modificare una definizione di ruolo a livello di elemento, espandere la cartella Ruoli. Eseguire una delle operazioni seguenti:  
  
    1.  Per eliminare una definizione di ruolo, fare clic con il pulsante destro del mouse sull'elemento e scegliere **Elimina**. Verrà visualizzata la finestra di dialogo **Elimina oggetto** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  Per modificare una definizione di ruolo, fare clic con il pulsante destro del mouse sull'elemento e scegliere **Proprietà**. Verrà visualizzata la scheda Generale della finestra di dialogo **Proprietà ruolo utente** .  
  
         Selezionare le attività che i membri del ruolo potranno eseguire e fare clic su **OK**.  
  
4.  Per eliminare o modificare una definizione di ruolo a livello di sistema, espandere la cartella **Ruoli a livello di sistema** . Eseguire una delle operazioni seguenti:  
  
    1.  Per eliminare una definizione di ruolo di sistema, fare clic con il pulsante destro del mouse sull'elemento e scegliere **Elimina**. Verrà visualizzata la finestra di dialogo **Elimina oggetto** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  Per modificare una definizione di ruolo di sistema, fare clic con il pulsante destro del mouse sull'elemento e scegliere **Proprietà**. Verrà visualizzata la scheda Generale della finestra di dialogo **Proprietà ruolo a livello di sistema** .  
  
         Selezionare le attività che i membri del ruolo potranno eseguire e fare clic su **OK** per applicare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire la connessione a un server di report in Management Studio](../tools/connect-to-a-report-server-in-management-studio.md)   
 (create-and-manage-role-assignments.md)   
 [Reporting Services in SQL Server Management Studio &#40;SSRS&#41;](../tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
