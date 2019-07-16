---
title: Specificare valori predefiniti per le colonne | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a02385a6cd12b85be1661c738488c000f810510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196718"
---
# <a name="specify-default-values-for-columns"></a>Specificare valori predefiniti per le colonne
  È possibile specificare un valore predefinito che sarà immesso nella colonna in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se non si assegna un valore predefinito e l'utente lascia la colonna vuota, si verificherà quanto segue:  
  
-   Se è stata impostata l'opzione che consente l'immissione di valori Null, nella colonna verrà inserito il valore NULL.  
  
-   Se non è stata impostata l'opzione che consente l'immissione di valori Null, la colonna resterà vuota, ma non sarà possibile salvare la riga senza avere fornito un valore per la colonna.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per specificare un valore predefinito personalizzato:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se la voce nel campo **Valore predefinito** sostituisce un valore predefinito associato (visualizzato senza parentesi), verrà chiesto se separare il valore predefinito e sostituirlo con il nuovo valore.  
  
-   Per immettere una stringa di testo, è necessario racchiudere il valore tra virgolette singole ('). Non è consentito l'utilizzo delle virgolette doppie (") poiché sono riservate per gli identificatori delimitati.  
  
-   Per immettere un valore predefinito numerico immettere il numero senza virgolette.  
  
-   Per specificare un oggetto o una funzione, immetterne il nome senza racchiuderlo tra virgolette.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>Per specificare un valore predefinito per una colonna  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulle colonne della tabella di cui modificare la scala e scegliere **Progetta**.  
  
2.  Selezionare la colonna per la quale si desidera specificare un valore predefinito.  
  
3.  Nella scheda **Proprietà colonne** , immettere il nuovo valore predefinito nella proprietà **Valore predefinito dell'associazione** .  
  
    > [!NOTE]  
    >  Per specificare un valore predefinito numerico, immettere il numero desiderato. Per specificare un oggetto o una funzione, immetterne il nome. Per specificare un valore predefinito alfanumerico, immettere il valore racchiudendolo tra virgolette singole.  
  
4.  Nel menu **File** scegliere **Salva**_table name_.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>Per specificare un valore predefinito per una colonna  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
    GO  
    INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
    GO  
    ALTER TABLE dbo.doc_exz  
    ADD CONSTRAINT col_b_def  
    DEFAULT 50 FOR column_b ;  
    GO  
  
    ```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>  
