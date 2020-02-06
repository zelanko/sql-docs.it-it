---
title: Creare, eliminare o modificare un ruolo (Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
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
ms.openlocfilehash: f079b7b16f485b92c60952d082281a1dba52d024
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65570548"
---
# <a name="role-definitions---create-delete-or-modify"></a>Definizioni di ruolo - Creare, eliminare o modificare

Reporting Services offre ruoli predefiniti che definiscono i livelli di accesso al server di report. A ogni utente o gruppo che deve accedere al server di report viene assegnato un ruolo che definisce le attività consentite. I ruoli vengono definiti per il server di report complessivamente. È necessario mantenere coerenza nella definizione e nell'uso di un ruolo in tutte le aree del server di report.

Per creare, modificare o eliminare ruoli, è possibile usare [!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)]. Si possono eliminare solo ruoli non in uso.

 Per assegnare utenti e gruppi ai ruoli creati, usare il portale Web SSRS. Per altre informazioni, vedere [Concedere l'accesso utente a un server di report](../../reporting-services/security/grant-user-access-to-a-report-server.md).

> [!NOTE]  
>Se il server di report è configurato per la modalità integrata SharePoint e si è connessi al sito di SharePoint con cui il server di report è integrato, è possibile visualizzare e modificare i livelli di autorizzazione che controllano l'accesso al contenuto e alle operazioni del server di report.

## <a name="to-create-a-role-definition"></a>Per creare una definizione di ruolo

1. Espandere il nodo di un server di report in Esplora oggetti.

2. Espandere la cartella sicurezza.

3. Per creare una definizione di ruolo a livello di elemento, fare clic con il pulsante destro del mouse su **Ruoli** > **Nuovo ruolo**.

    Per creare una definizione di ruolo a livello di sistema, invece, fare clic con il pulsante destro del mouse su **Ruoli a livello di sistema** > **Nuovo ruolo**.

4. Digitare un nome univoco per il ruolo. Il nome deve includere almeno un carattere. È anche possibile inserire spazi e alcuni simboli, ma non i caratteri `[; : \ / @ & = + , $ / * < > | "]`.

5. Se lo si desidera, digitare una descrizione. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], questa descrizione sarà visibile solo in questa pagina. Per gli utenti che visualizzeranno l'elemento con il portale Web, la descrizione sarà visibile in tale strumento.

6. Selezionare le attività che potranno essere eseguite dai membri del ruolo.

7. Selezionare **OK**.

### <a name="to-delete-or-modify-a-role-definition"></a>Per eliminare o modificare una definizione di ruolo  

1. Espandere il nodo di un server di report in Esplora oggetti.

2. Espandere la cartella sicurezza.

3. Per eliminare o modificare una definizione di ruolo a livello di elemento, espandere la cartella Ruoli e quindi eseguire una di queste azioni:

    1. Per eliminare una definizione di ruolo, fare clic con il pulsante destro del mouse sull'elemento e quindi scegliere **Elimina**. Verrà visualizzata la finestra di dialogo **Elimina elementi catalogo**. Selezionare **OK** per eliminare il ruolo.
  
    2. Per modificare una definizione di ruolo, fare clic con il pulsante destro del mouse sull'elemento e quindi scegliere **Proprietà**. Verrà visualizzata la scheda Generale della finestra di dialogo **Proprietà ruolo utente** .

         Selezionare le attività che potranno essere eseguite dai membri del ruolo e quindi **OK**.
  
4. Per eliminare o modificare una definizione di ruolo a livello di sistema, espandere la cartella **Ruoli a livello di sistema** . Eseguire una di queste azioni:

- Per eliminare una definizione di ruolo a livello di sistema, fare clic con il pulsante destro del mouse sull'elemento e scegliere **Elimina**. Verrà visualizzata la finestra di dialogo **Elimina elementi catalogo**. Selezionare **OK** per eliminare il ruolo.

- Per modificare una definizione di ruolo a livello di sistema, fare clic con il pulsante destro del mouse sull'elemento e scegliere **Proprietà**. Verrà visualizzata la scheda Generale della finestra di dialogo **Proprietà ruolo a livello di sistema** . Selezionare le attività che potranno essere eseguite dai membri del ruolo e quindi **OK** per applicare le modifiche.

## <a name="see-also"></a>Vedere anche

 [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [Creare e gestire assegnazioni di ruolo](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [Reporting Services in SQL Server Management Studio &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
