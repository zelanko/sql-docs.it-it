---
title: Aggiungere colonne a una tabella (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- adding columns
ms.assetid: abeb8d52-d562-4e29-9e1e-2923ae874859
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eed258c78e76c5ec3f6aeeeb6bdd647166592613
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856137"
---
# <a name="add-columns-to-a-table-database-engine"></a>Aggiungere colonne a una tabella (Motore di database)
  In questo argomento viene descritto come aggiungere nuove colonne a una tabella in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per inserire le colonne:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 L'utilizzo dell'istruzione ALTER TABLE per aggiungere automaticamente colonne a una tabella aggiunge tali colonne alla fine della tabella. Se si desidera le colonne in un ordine specifico all'interno della tabella, utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, notare che questa non è una procedura consigliata di progettazione del database. La procedura consigliata è specificare l'ordine nel quale le colonne vengono restituite all'applicazione e il livello della query. Non è necessario basarsi sull'utilizzo di SELECT * per restituire tutte le colonne nell'ordine previsto basato sull'ordine nel quale sono definiti nella tabella. Nelle query e nelle applicazioni, specificare sempre le colonne per nome nell'ordine nel quale si desidera visualizzarle.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-insert-columns-into-a-table-with-table-designer"></a>Per inserire colonne in una tabella con Progettazione tabelle  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella a cui si vogliono aggiungere colonne e scegliere **Progetta**.  
  
2.  Fare clic sulla prima cella vuota nella colonna **Nome colonna** .  
  
3.  Immettere il nome della colonna nella cella. Il nome della colonna non può essere omesso.  
  
4.  Premere TAB per posizionarsi sulla cella **Tipo di dati** e selezionare un tipo di dati dall'elenco a discesa. Anche questo è un valore obbligatorio. Se non viene specificato, verrà assegnato un valore predefinito.  
  
    > [!NOTE]  
    >   Il valore predefinito può essere modificato nella finestra di dialogo **Opzioni** in **Database Tools**.  
  
5.  Proseguire con la definizione delle altre proprietà della colonna nella scheda **Proprietà colonne** .  
  
    > [!NOTE]  
    >   Quando si crea una nuova colonna, le vengono assegnati i valori predefiniti per le diverse proprietà. Tali valori possono comunque essere modificati nella scheda **Proprietà colonne** .  
  
6.  Dopo aver completato l'aggiunta delle colonne, scegliere **Salva**_nome tabella_ dal menu **File**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-insert-columns-into-a-table"></a>Per inserire le colonne in una tabella  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Negli esempi seguenti vengono aggiunte due colonne alla tabella `dbo.doc_exa`. Copiare e incollare l'esempio seguente nella finestra query, quindi fare clic su **Esegui** .  
  
```  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;  
```  
  
##  <a name="for-more-information-see-alter-table-40transact-sql41"></a><a name="FollowUp"></a>Per ulteriori informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
