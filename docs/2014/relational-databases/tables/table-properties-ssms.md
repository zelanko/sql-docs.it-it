---
title: Proprietà tabella | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.tableproperties.storage.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql12.swb.tableproperties.filetable.f1
- sql12.swb.tableproperties.general.f1
- sql12.swb.tableproperties.changetracking.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07f157294700b3b3b7958ce4cdc6f1589bff864
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196712"
---
# <a name="table-properties"></a>Table Properties
  In questo argomento vengono descritte le proprietà della tabella visualizzate nella finestra di dialogo Proprietà tabella in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni su come visualizzare queste proprietà, vedere [Visualizzare la definizione di una tabella](view-the-table-definition.md).  
  
 **Contenuto dell'articolo**  
  
1.  [Pagina Generale](#GeneralPage)  
  
2.  [Pagina Rilevamento modifiche](#ChangeTracking)  
  
3.  [Pagina di Tabella di File](#FileTable)  
  
4.  [Pagina Archivio](#Storage)  
  
##  <a name="general-page"></a><a name="GeneralPage"></a> Pagina Generale  
 **Database**  
 Nome del database che contiene la tabella.  
  
 **Server**  
 Nome dell'istanza del server corrente.  
  
 **Utente**  
 Nome dell'utente della connessione.  
  
 **Data creazione**  
 Data e ora di creazione della tabella.  
  
 **Nome**  
 Nome della tabella.  
  
 **Schema**  
 Schema proprietario della tabella.  
  
 **Oggetto di sistema**  
 Indica che la tabella è una tabella di sistema usata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per contenere informazioni interne. È consigliabile non modificare direttamente le tabelle di sistema o fare riferimento a tali tabelle.  
  
 **ANSI NULLs**  
 Indica se l'oggetto è stato creato con l'opzione ANSI NULLs impostata su ON. Per altre informazioni, vedere [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).  
  
 **Identificatore delimitato**  
 Indica se l'oggetto è stato creato con l'opzione quoted identifier impostata su ON. Per altre informazioni, vedere [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **Escalation blocchi**  
 Indica la granularità dell'escalation dei blocchi della tabella. Per altre informazioni sui blocchi nel motore di database, vedere [Guida per il controllo delle versioni delle righe e il blocco della transazione di SQL Server](https://msdn.microsoft.com/library/jj856598.aspx). I valori possibili sono:  
  
 AUTO  
 Questa opzione consente al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di selezionare la granularità dell'escalation dei blocchi appropriata per lo schema della tabella.  
  
-   Se la tabella è partizionata, sarà consentita l'escalation dei blocchi nella granularità a livello di heap o albero B (HoBT). Una volta eseguita l'escalation del blocco nel livello HoBT, non verrà eseguita alcuna successiva escalation del blocco nella granularità TABLE.  
  
-   Se la tabella non è partizionata, l'escalation blocchi verrà eseguita nella granularità TABLE.  
  
 TABLE  
 L'escalation dei blocchi viene eseguita con una granularità a livello di tabella, indipendentemente dal fatto che la tabella sia o meno partizionata. TABLE rappresenta il valore predefinito.  
  
 DISABLE  
 Evita che venga eseguita l'escalation blocchi nella maggior parte dei casi. I blocchi a livello di tabella non vengono completamente disattivati. Quando si esegue l'analisi di una tabella che non dispone di alcun indice cluster nel livello di isolamento serializzabile, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve acquisire un blocco di tabella per proteggere l'integrità dei dati.  
  
 **Tabella replicata**  
 Indica se la tabella è stata replicata in un altro database usando la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I possibili valori sono `True` o `False`.  
  
##  <a name="change-tracking-page"></a><a name="ChangeTracking"></a>Pagina Rilevamento modifiche  
 **Rilevamento delle modifiche**  
 Indica se il rilevamento delle modifiche è abilitato per la tabella. Il valore predefinito è `False`.  
  
 Questa opzione è disponibile solo quando il rilevamento delle modifiche è abilitato per il database.  
  
 Per abilitare il rilevamento delle modifiche, è necessario che la tabella disponga di una chiave primaria e che si disponga dell'autorizzazione per modificare la tabella. È anche possibile configurare il rilevamento delle modifiche usando [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
 **Colonne di rilevamento aggiornate**  
 Indica se [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rileva le colonne che sono state aggiornate.  
  
 Per altre informazioni sul rilevamento delle modifiche, vedere [Informazioni sul rilevamento delle modifiche &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
##  <a name="filetable-page"></a><a name="FileTable"></a>Pagina FileTable  
 Consente di visualizzare le proprietà della tabella correlate alle tabelle FileTable. Per altre informazioni, vedere [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md).  
  
 **Regole di confronto colonna Name tabella FileTable**  
 Regole di confronto applicate alla colonna **Name** in una tabella FileTable. La colonna **Name** contiene i nomi di file e directory.  
  
 **Nome di directory FileTable**  
 Cartella radice per la tabella FileTable.  
  
 **Spazio dei nomi FileTable abilitato**  
 Se impostato su `True`, questo valore indica che la tabella è una tabella FileTable. Se si modifica questo valore in `False`, la tabella FileTable viene modificata in una comune tabella utente. Se in seguito si desidera modificare di nuovo la tabella in tabella FileTable, questa dovrà superare un controllo di coerenza per tabelle FileTable affinché la conversione riesca.  
  
##  <a name="storage-page"></a><a name="Storage"></a>Pagina archiviazione  
 Consente di visualizzare le proprietà relative all'archiviazione della tabella selezionata.  
  
### <a name="compression"></a>Compressione  
 **Tipo di compressione**  
 Tipo di compressione della tabella. Questa proprietà è disponibile solo per le tabelle non partizionate. Per altre informazioni, vedere [Data Compression](../data-compression/data-compression.md).  
  
 **Partizioni che usano la compressione di pagina**  
 Numeri di partizioni che usano la compressione di pagina. Questa proprietà è disponibile solo per le tabelle partizionate.  
  
 **Partizioni non compresse**  
 Numeri di partizioni non compresse. Questa proprietà è disponibile solo per le tabelle partizionate.  
  
 **Partizioni che usano la compressione di riga**  
 Numeri di partizioni che usano la compressione di riga. Questa proprietà è disponibile solo per le tabelle partizionate.  
  
### <a name="filegroup"></a>Filegroup  
 **Filegroup dati di testo**  
 Nome del filegroup che contiene i dati di testo della tabella.  
  
 **Filegroup**  
 Nome del filegroup che contiene la tabella.  
  
 **Tabella partizionata**  
 I valori possibili sono `True` e `False`.  
  
 **Filegroup FILESTREAM**  
 Specificare il nome del filegroup di dati FILESTREAM se la tabella contiene una colonna `varbinary(max)` con l'attributo FILESTREAM. Il filegroup di dati FILESTREAM predefinito è indicato per impostazione predefinita.  
  
 Se la tabella non contiene dati FILESTREAM, il campo è vuoto.  
  
### <a name="general"></a>Generale  
 **Formato di archiviazione vardecimal abilitato**  
 Se `True`, questo valore di sola lettura indica che `decimal` i `numeric` tipi di dati e vengono archiviati utilizzando il formato di archiviazione vardecimal. Per modificare questa opzione, usare l' `vardecimal storage format` opzione di [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql). Il formato di archiviazione vardecimal è deprecato. ed è necessario usare il tipo di compressione ROW.  
  
 **Spazio degli indici**  
 Quantità di spazio occupata dagli indici nella tabella, espresso in megabyte. Questo valore non include lo spazio usato dagli indici XML per la tabella. Se gli indici XML appartengono alla tabella, usare in alternativa [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) .  
  
 **Numero di righe**  
 Numero di righe della tabella.  
  
 **Spazio dati**  
 Quantità di spazio occupata dai dati nella tabella, espressa in megabyte.  
  
### <a name="partitioning"></a>Partizionamento  
 Questa sezione è disponibile solo se la tabella è partizionata. Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 **Colonna di partizione**  
 Nome della colonna in relazione alla quale è partizionata la tabella.  
  
 **Schema di partizione**  
 Nome dello schema di partizione, se la tabella è partizionata. Se la tabella non è partizionata, il campo è vuoto.  
  
 **Numero di partizioni**  
 Numero di partizioni della tabella.  
  
 **Schema di partizione FILESTREAM**  
 Nome dello schema di partizione FILESTREAM, se la tabella è partizionata. Se la tabella non è partizionata, il campo è vuoto.  
  
 Lo schema di partizione FILESTREAM deve essere simmetrico rispetto allo schema specificato nell'opzione **Schema partizione** .  
  
## <a name="see-also"></a>Vedi anche  
 [Visualizzare la definizione della tabella](view-the-table-definition.md)   
 [Modificare colonne &#40;Motore di database&#41;](../tables/modify-columns-database-engine.md)  
  
  
