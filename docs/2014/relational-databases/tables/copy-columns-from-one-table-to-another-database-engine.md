---
title: Copiare colonne da una tabella a un'altra (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
ms.openlocfilehash: 37b98bf0910cbbb4c2a1d7fe01f11d52703ec88c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047286"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>Copia di colonne da una tabella a un'altra (Motore di database)
  In questo argomento viene illustrato come copiare colonne di una tabella a un'altra copiando solo la definizione di colonna oppure la definizione e i dati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per copiare le colonne tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Quando si copia una colonna contenente un tipo di dati alias da un database a un altro, il tipo di dati alias potrebbe non essere disponibile nel database di destinazione. In questo caso, alla colonna verrà assegnato il tipo di dati di base più simile tra quelli disponibili nel database.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Per copiare le definizioni delle colonne tra tabelle  
  
1.  Aprire la tabella contenente le colonne da copiare e quella in cui verranno copiate le colonne facendo clic con il pulsante destro del mouse sulle tabelle, quindi scegliendo **Progetta**.  
  
2.  Fare clic sulla scheda relativa alla tabella contenente le colonne da copiare e selezionarle.  
  
3.  Scegliere **Copia** dal menu **Modifica**.  
  
4.  Fare clic sulla scheda relativa alla tabella in cui copiare le colonne.  
  
5.  Selezionare la colonna prima della quale si desidera che vengano inserite le colonne appena copiate, quindi scegliere **Incolla** dal menu **Modifica**.  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>Per copiare dati tra tabelle  
  
1.  Seguire le istruzioni sopra riportate per copiare le definizioni delle colonne.  
  
    > [!NOTE]  
    >  Prima di iniziare a copiare i dati da una tabella a un'altra, assicurarsi che i tipi di dati delle colonne di destinazione siano compatibili con quelli delle colonne di origine.  
  
2.  In Esplora oggetti selezionare con il pulsante destro del mouse il nodo **Viste** , quindi scegliere **Nuova vista**.  
  
3.  Scegliere **Modifica tipo** dal menu **Progettazione query**, quindi **Accodamento**.  
  
4.  Nella finestra di dialogo **Scegliere la tabella di destinazione per Accodamento** selezionare la tabella in cui si desidera copiare i dati, quindi scegliere **OK**.  
  
     Se si sta effettuando la copia di righe all'interno di una stessa tabella, sarà possibile aggiungere la tabella di origine come tabella di destinazione.  
  
    > [!NOTE]  
    >  In**Progettazione query** non è possibile stabilire in anticipo le tabelle e le viste da aggiornare. Pertanto, nell'elenco delle tabelle nella finestra di dialogo **Scegliere la tabella di destinazione per Accodamento** sono visualizzate tutte le tabelle e le viste disponibili nella connessione dati su cui si esegue la query, anche quelle che potrebbero non essere valide come tabelle o viste di destinazione.  
  
5.  Fare clic con il pulsante destro del mouse nel corpo del riquadro Diagramma, quindi scegliere **Aggiungi tabella a diagramma**dal menu di scelta rapida.  
  
6.  Nella finestra di dialogo **Aggiungi tabella** selezionare le singole tabelle da cui si desidera copiare i dati, fare clic su **Aggiungi**, quindi su **Chiudi**.  
  
     Le tabelle verranno visualizzate in forma abbreviata nel riquadro Diagramma.  
  
7.  Nelle tabelle in forma abbreviata selezionare le caselle relative alle colonne da cui si desidera copiare i dati.  
  
8.  Nella colonna **Accodamento** del riquadro Criteri selezionare per ogni colonna di destinazione una colonna da cui copiare i dati.  
  
9. Specificare le righe da copiare immettendo le condizioni di ricerca nel riquadro Criteri. Per i dettagli, vedere [Definire condizioni di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md).  
  
     Se non si specifica alcuna condizione di ricerca, tutte le righe della tabella di origine verranno copiate nella tabella di destinazione.  
  
10. Se si desidera copiare le informazioni di riepilogo, specificare le opzioni **di raggruppamento** . Per i dettagli, vedere [Riepilogare o aggregare valori per tutte le righe di una tabella &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md).  
  
11. Scegliere il pulsante **Esegui SQL** per eseguire la query.  
  
     Quando si esegue una query di Accodamento, non viene restituito alcun risultato nel [riquadro risultati](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Viene invece visualizzato un messaggio che indica il numero di righe copiate.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Per copiare le definizioni delle colonne tra tabelle  
  
1.  Non è possibile copiare singole colonne da una tabella a un'altra tramite istruzioni Transact-SQL. È tuttavia possibile creare una nuova tabella nel filegroup predefinito e inserirvi le righe restituite dalla query. Per altre informazioni, vedere [Clausola INTO &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-into-clause-transact-sql).  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>Per copiare dati tra tabelle  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
