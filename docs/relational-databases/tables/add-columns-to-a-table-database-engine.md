---
title: Aggiungere colonne a una tabella (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4f3d7fe83359162d928c46578b64c59ae399b1f2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729530"
---
# <a name="add-columns-to-a-table-database-engine"></a>Aggiungere colonne a una tabella (Motore di database)

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Questo articolo descrive come aggiungere nuove colonne a una tabella in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="BeforeYouBegin"></a> Prima di iniziare

### <a name="Restrictions"></a> Limitazioni e restrizioni

 L'utilizzo dell'istruzione ALTER TABLE per aggiungere automaticamente colonne a una tabella aggiunge tali colonne alla fine della tabella. Se si desidera le colonne in un ordine specifico all'interno della tabella, utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, notare che questa non è una procedura consigliata di progettazione del database. La procedura consigliata è specificare l'ordine nel quale le colonne vengono restituite all'applicazione e il livello della query. Non è necessario basarsi sull'utilizzo di SELECT * per restituire tutte le colonne nell'ordine previsto basato sull'ordine nel quale sono definiti nella tabella. Nelle query e nelle applicazioni, specificare sempre le colonne per nome nell'ordine nel quale si desidera visualizzarle.

### <a name="Security"></a> Sicurezza

#### <a name="Permissions"></a> Autorizzazioni

È necessario disporre dell'autorizzazione ALTER per la tabella.

## <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio

### <a name="to-insert-columns-into-a-table-with-table-designer"></a>Per inserire colonne in una tabella con Progettazione tabelle

1. In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella a cui si vogliono aggiungere colonne e scegliere **Progetta**.
2. Fare clic sulla prima cella vuota nella colonna **Nome colonna** .
3. Immettere il nome della colonna nella cella. Il nome della colonna non può essere omesso.
4. Premere TAB per posizionarsi sulla cella **Tipo di dati** e selezionare un tipo di dati dall'elenco a discesa.

   Si tratta di un valore obbligatorio. Se non viene specificato, verrà assegnato un valore predefinito.

   > [!NOTE]
   > Il valore predefinito può essere modificato nella finestra di dialogo **Opzioni** in **Strumenti di database**.

5. Proseguire con la definizione delle altre proprietà della colonna nella scheda **Proprietà colonne** .

    > [!NOTE]
    > Quando si crea una nuova colonna, le vengono assegnati i valori predefiniti per le diverse proprietà. Tali valori possono comunque essere modificati nella scheda **Proprietà colonne** .

6. Dopo avere completato l'aggiunta delle colonne, scegliere **Salva** **nome tabella**  dal menu _File_.
  
## <a name="TsqlProcedure"></a> Uso di Transact-SQL
  
### <a name="to-insert-columns-into-a-table"></a>Per inserire le colonne in una tabella  
  
Negli esempi seguenti vengono aggiunte due colonne alla tabella `dbo.doc_exa`.

```sql
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;
```

#### <a name="FollowUp"></a> Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
