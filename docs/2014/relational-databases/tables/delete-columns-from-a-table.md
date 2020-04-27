---
title: Eliminare le colonne da una tabella | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 718aeca12c90435b68fd6cedde150dfbdeb3c063
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62761658"
---
# <a name="delete-columns-from-a-table"></a>Eliminare le colonne da una tabella
  In questo argomento viene descritta la modalità di eliminazione delle colonne tabella in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!CAUTION]  
>  Quando si elimina una colonna da una tabella, tale colonna e tutti i dati in essa contenuti verranno eliminati dal database. Questa azione non può essere annullata.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per eliminare una colonna da una tabella:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Non è possibile eliminare una colonna che dispone di un vincolo CHECK. È necessario eliminare prima questo vincolo.  
  
 Non è possibile eliminare una colonna che dispone di vincoli PRIMARY KEY o FOREIGN KEY o altre dipendenze a parte quando si utilizza Progettazione tabelle. Quando si utilizza Esplora oggetti o [!INCLUDE[tsql](../../includes/tsql-md.md)], è necessario prima rimuovere tutte le dipendenze sulla colonna.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-columns-by-using-object-explorer"></a>Per eliminare le colonne utilizzando Esplora oggetti.  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella da cui si vogliono eliminare colonne, quindi scegliere **Elimina**.  
  
3.  Nella finestra di dialogo **Elimina oggetto** fare clic su **OK**.  
  
 Se la colonna contiene vincoli o altre dipendenze, un messaggio di errore sarà visualizzato nella finestra di dialogo **Elimina oggetto** . Risolvere l'errore eliminando i vincoli a cui si fa riferimento.  
  
#### <a name="to-delete-columns-by-using-table-designer"></a>Per eliminare le colonne utilizzando Progettazione tabelle.  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella da cui si vogliono eliminare colonne, quindi scegliere **Progettazione**.  
  
2.  Fare clic con il pulsante destro del mouse sulla colonna che si vuole eliminare e scegliere **Elimina colonna** dal menu di scelta rapida.  
  
3.  Se la colonna fa parte di una relazione (FOREIGN KEY o PRIMARY KEY), verrà visualizzato un messaggio in cui viene chiesto di confermare l'eliminazione delle colonne selezionate e delle corrispondenti relazioni. Scegliere **Sì**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-delete-columns"></a>Per eliminare le colonne  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
    ```  
  
 Se la colonna contiene vincoli o altre dipendenze, verrà restituito un messaggio di errore. Risolvere l'errore eliminando i vincoli a cui si fa riferimento.  
  
 Per altri esempi, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
##  <a name="FollowUp"></a>  
