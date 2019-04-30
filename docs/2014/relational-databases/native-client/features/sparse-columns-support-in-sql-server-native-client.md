---
title: Supporto per colonne di tipo sparse in SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79151d13f5b90e7da8ea50d3472d05ed46423e2e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225748"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Supporto per colonne di tipo sparse in SQL Server Native Client
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta le colonne di tipo sparse. Per altre informazioni sulle colonne di tipo sparse [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [usare le colonne di tipo Sparse](../../tables/use-sparse-columns.md) e [usare set di colonne](../../tables/use-column-sets.md).  
  
 Per altre informazioni sulle colonne di tipo sparse supporto in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [supporta colonne di tipo Sparse &#40;ODBC&#41; ](../odbc/sparse-columns-support-odbc.md) e [supporta colonne di tipo Sparse &#40;OLE DB&#41; ](../ole-db/sparse-columns-support-ole-db.md) .  
  
 Per informazioni sulle applicazioni di esempio in cui viene illustrata questa funzionalità, vedere la [pagina relativa agli esempi di programmazione dati di SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Scenari utente per colonne di tipo sparse e SQL Server Native Client  
 Nella tabella seguente vengono descritti in breve gli scenari comuni per gli utenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client che utilizzano colonne di tipo sparse:  
  
|Scenario|Comportamento|  
|--------------|--------------|  
|**Selezionare \* dalla tabella** o IOpenRowset:: OPENROWSET.|Restituisce tutte le colonne che non sono membri del set di colonne `column_set` di tipo sparse, nonché una colonna XML che contiene i valori di tutte le colonne non Null che sono membri del set di colonne `column_set` di tipo sparse.|  
|Fare riferimento a una colonna in base al nome.|È possibile fare riferimento alla colonna indipendentemente dal relativo stato di colonna di tipo sparse o dall'appartenenza al set di colonne `column_set`.|  
|Accedere alle colonne che sono membri del set di colonne `column_set` tramite una colonna XML calcolata.|È possibile accedere alle colonne che sono membri del set di colonne `column_set` di tipo sparse selezionando il set di colonne `column_set` in base al nome e i valori di tali colonne possono essere inseriti e aggiornati aggiornando i dati XML nella colonna `column_set`.<br /><br /> Il valore deve essere conforme allo schema per le colonne `column_set`.|  
|Recuperare i metadati per tutte le colonne in una tabella tramite SQLColumns con un criterio di ricerca colonna del valore NULL o '% s' (ODBC). o tramite il set di righe dello schema DBSCHEMA_COLUMNS senza restrizioni di colonna (OLE DB).|Restituisce una riga per tutte le colonne che non sono membri di un set di colonne `column_set`. Se la tabella include un set di colonne `column_set` di tipo sparse, verrà restituita una riga per la tabella.<br /><br /> Si noti che questo comportamento non restituisce metadati per colonne membri di un set di colonne `column_set`.|  
|Recuperare metadati per tutte le colonne, indipendentemente dal fatto che siano o meno di tipo sparse o dall'appartenenza a un set di colonne `column_set`. È possibile che venga restituito un numero molto elevato di righe.|Impostare il campo di descrizione SQL_SOPT_SS_NAME_SCOPE su SQL_SS_NAME_SCOPE_EXTENDED e chiamare [SQLColumns](../../native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Chiamare IDBSchemaRowset:: GetRowset di righe dello schema DBSCHEMA_COLUMNS_EXTENDED (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Questo tipo di applicazione, tuttavia, può eseguire direttamente query viste di sistema.|  
|Recuperare metadati solo per le colonne che sono membri di un set di colonne `column_set`. È possibile che venga restituito un numero molto elevato di righe.|Impostare il campo di descrizione SQL_SOPT_SS_NAME_SCOPE su SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET e chiamare SQLColumns (ODBC).<br /><br /> Chiamare IDBSchemaRowset:: GetRowset di righe dello schema DBSCHEMA_SPARSE_COLUMN_SET (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query sulle viste di sistema.|  
|Determinare se una colonna è di tipo sparse.|Consultare la colonna SS_IS_SPARSE del set di risultati SQLColumns (ODBC).<br /><br /> Esaminare la colonna SS_IS_SPARSE del set di righe dello schema DBSCHEMA_COLUMNS (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query sulle viste di sistema.|  
|Determinare se una colonna è un set di colonne `column_set`.|Esaminare la colonna SS_IS_COLUMN_SET del set di risultati SQLColumns. In alternativa, esaminare l'attributo di colonna specifico di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL_CA_SS_IS_COLUMN_SET (ODBC).<br /><br /> Esaminare la colonna SS_IS_COLUMN_SET del set di righe dello schema DBSCHEMA_COLUMNS. O, consultare *dwFlags* restituiti da IColumnsInfo:: GetColumnInfo o DBCOLUMNFLAGS nel set di righe restituito da IColumnsRowset::. Per le colonne `column_set`, DBCOLUMNFLAGS_SS_ISCOLUMNSET sarà impostato (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query sulle viste di sistema.|  
|Importazione ed esportazione di colonne di tipo sparse tramite BCP per una tabella senza `column_set`.|Nessuna modifica nel comportamento rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importazione ed esportazione di colonne di tipo sparse tramite BCP per una tabella con `column_set`.|Il `column_set` viene importato ed esportato nello stesso modo come XML; vale a dire, come `varbinary(max)` se associato come tipo binario oppure come `nvarchar(max)` se associato come un `char` o **wchar** tipo.<br /><br /> Le colonne che sono membri del set di colonne `column_set` di tipo sparse non vengono esportate come colonne distinte, ma vengono esportate solo nel valore di `column_set`.|  
|Comportamento di `queryout` per BCP.|Nessuna modifica nella gestione di colonne denominate in modo esplicito rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> Gli scenari che comportano l'importazione e l'esportazione tra tabelle con schemi diversi possono richiedere una gestione speciale.<br /><br /> Per ulteriori informazioni su BCP, vedere Supporto per la copia bulk (BCP) per colonne di tipo sparse più avanti in questo argomento.|  
  
## <a name="down-level-client-behavior"></a>Comportamento dei client legacy  
 I client legacy restituiscono metadati solo per le colonne che non sono membri di tipo sparse `column_set` per SQLColumns e DBSCHMA_COLUMNS. I set di righe dello schema OLE DB aggiuntivi introdotti in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client non sarà disponibile né saranno le modifiche apportate a SQLColumns di ODBC tramite SQL_SOPT_SS_NAME_SCOPE.  
  
 I client legacy possono accedere per nome alle colonne che sono membri del `column_set` di tipo sparse e la colonna `column_set` sarà accessibile come colonna XML per i client [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Supporto per la copia bulk (BCP) per colonne di tipo sparse  
 Non è stata apportata alcuna modifica all'API BCP in ODBC o OLE DB per le colonne di tipo sparse o le caratteristiche `column_set`.  
  
 Se una tabella include un set di colonne `column_set`, le colonne di tipo sparse non verranno gestite come colonne distinte. I valori di tutte le colonne di tipo sparse sono inclusi nel valore della `column_set`, che viene esportata esattamente come una colonna XML; ovvero come `varbinary(max)` se associato come tipo binario oppure come `nvarchar(max)` se associato come un `char` o **wchar** tipo). All'importazione, il valore di `column_set` deve essere conforme allo schema di `column_set`.  
  
 Per le operazioni `queryout`, non esiste alcuna modifica al modo in cui sono gestite le colonne a cui si fa esplicitamente riferimento. Le colonne `column_set` dispongono dello stesso comportamento delle colonne XML e il fatto che siano o meno di tipo sparse non ha effetto sulla gestione di colonne di tipo sparse denominate.  
  
 Se, tuttavia, si utilizza `queryout` per l'esportazione e si fa riferimento a colonne di tipo sparse che sono membri del set di colonne di tipo sparse in base al nome, non è possibile eseguire un'importazione diretta in una tabella dalla struttura analoga. Infatti BCP utilizza metadati consistenti con un **selezionate \***  operazione per l'importazione e non può corrispondere `column_set` colonne membri con questi metadati. Per importare colonne membri del set di colonne `column_set` singolarmente, è necessario definire una vista nella tabella che fa riferimento alle colonne `column_set` desiderate ed eseguire l'operazione di importazione utilizzando la vista.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione in SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
