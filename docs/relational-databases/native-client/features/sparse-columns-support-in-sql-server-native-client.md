---
title: Le colonne di tipo sparse supportano in SQL Native Client
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0271b8e07a6e9ea9b797427a66df097e1114cad4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247424"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Supporto per colonne di tipo sparse in SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta le colonne di tipo sparse. Per ulteriori informazioni sulle colonne di tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]sparse in, vedere [utilizzo di colonne di tipo sparse](../../../relational-databases/tables/use-sparse-columns.md) e [utilizzo di set di colonne](../../../relational-databases/tables/use-column-sets.md).  
  
 Per ulteriori informazioni sul supporto delle colonne di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo sparse in native client, vedere [supporto delle colonne di tipo sparse &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md) e [colonne di tipo sparse supportano &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md).  
  
 Per informazioni sulle applicazioni di esempio in cui viene illustrata questa funzionalità, vedere la pagina relativa agli [esempi di programmazione dati di SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Scenari utente per colonne di tipo sparse e SQL Server Native Client  
 Nella tabella seguente vengono descritti in breve gli scenari comuni per gli utenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client che utilizzano colonne di tipo sparse:  
  
|Scenario|Comportamento|  
|--------------|--------------|  
|**Select \* from table** o IOpenRowset:: OPENROWSET.|Restituisce tutte le colonne che non sono membri del set di colonne **column_set** di tipo sparse, nonché una colonna XML che contiene i valori di tutte le colonne non Null che sono membri del set di colonne **column_set** di tipo sparse.|  
|Fare riferimento a una colonna in base al nome.|È possibile fare riferimento alla colonna indipendentemente dal relativo stato di colonna di tipo sparse o dall'appartenenza al set di colonne **column_set**.|  
|Accedere alle colonne che sono membri del set di colonne **column_set** tramite una colonna XML calcolata.|È possibile accedere alle colonne che sono membri del set di colonne **column_set** di tipo sparse selezionando il set di colonne **column_set** in base al nome; inoltre, i valori di tali colonne possono essere inseriti e aggiornati aggiornando i dati XML nella colonna **column_set**.<br /><br /> Il valore deve essere conforme allo schema per le colonne **column_set**.|  
|Recuperare i metadati per tutte le colonne di una tabella tramite SQLColumns con un modello di ricerca di colonna NULL o '%' (ODBC); o tramite il DBSCHEMA_COLUMNS set di righe dello schema senza alcuna restrizione di colonna (OLE DB).|Restituisce una riga per tutte le colonne che non sono membri di un set di colonne **column_set**. Se la tabella include un set di colonne **column_set** di tipo sparse, verrà restituita una riga per la tabella.<br /><br /> Si noti che questo comportamento non restituisce metadati per colonne membri di un set di colonne **column_set**.|  
|Recuperare metadati per tutte le colonne, indipendentemente dal fatto che siano o meno di tipo sparse o dall'appartenenza a un set di colonne **column_set**. È possibile che venga restituito un numero molto elevato di righe.|Impostare il campo del descrittore SQL_SOPT_SS_NAME_SCOPE SQL_SS_NAME_SCOPE_EXTENDED e chiamare [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Chiamare IDBSchemaRowset:: GetRowset per il set di righe dello schema DBSCHEMA_COLUMNS_EXTENDED (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query direttamente sulle viste di sistema.|  
|Recuperare metadati solo per le colonne che sono membri di un set di colonne **column_set**. È possibile che venga restituito un numero molto elevato di righe.|Impostare il campo del descrittore SQL_SOPT_SS_NAME_SCOPE SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET e chiamare SQLColumns (ODBC).<br /><br /> Chiamare IDBSchemaRowset:: GetRowset per il set di righe dello schema DBSCHEMA_SPARSE_COLUMN_SET (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query sulle viste di sistema.|  
|Determinare se una colonna è di tipo sparse.|Consultare la colonna SS_IS_SPARSE del set di risultati SQLColumns (ODBC).<br /><br /> Esaminare la colonna SS_IS_SPARSE del set di righe dello schema DBSCHEMA_COLUMNS (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query sulle viste di sistema.|  
|Determinare se una colonna è un **column_set**.|Consultare la colonna SS_IS_COLUMN_SET del set di risultati SQLColumns. In alternativa, esaminare l'attributo di colonna specifico di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL_CA_SS_IS_COLUMN_SET (ODBC).<br /><br /> Esaminare la colonna SS_IS_COLUMN_SET del set di righe dello schema DBSCHEMA_COLUMNS. In alternativa, consultare *dwFlags* restituito da IColumnsInfo:: GETCOLUMNINFO o DBCOLUMNFLAGS nel set di righe restituito da IColumnsRowset:: GetColumnsRowset. Per **column_set** colonne, verrà impostato DBCOLUMNFLAGS_SS_ISCOLUMNSET (OLE DB).<br /><br /> Questo scenario non è possibile da un'applicazione che utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client da una versione precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Tale applicazione, tuttavia, può eseguire query sulle viste di sistema.|  
|Importazione ed esportazione di colonne di tipo sparse tramite BCP per una tabella senza **column_set**.|Nessuna modifica nel comportamento rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importazione ed esportazione di colonne di tipo sparse tramite BCP per una tabella con **column_set**.|Il **column_set** viene importato ed esportato in modo analogo a XML. ovvero, come **varbinary (max)** se associato come tipo binario o come **nvarchar (max)** se associato come tipo **char** o **WCHAR** .<br /><br /> Le colonne che sono membri del set di colonne **column_set** di tipo sparse non vengono esportate come colonne distinte, ma vengono esportate solo nel valore di **column_set**.|  
|comportamento di **query** per BCP.|Nessuna modifica nella gestione di colonne denominate in modo esplicito rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> Gli scenari che comportano l'importazione e l'esportazione tra tabelle con schemi diversi possono richiedere una gestione speciale.<br /><br /> Per ulteriori informazioni su BCP, vedere Supporto per la copia bulk (BCP) per colonne di tipo sparse più avanti in questo argomento.|  
  
## <a name="down-level-client-behavior"></a>Comportamento dei client legacy  
 I client restituiscono metadati solo per le colonne che non sono membri del set di colonne **column_set** di tipo sparse per SQLColumns e DBSCHMA_COLUMNS. I set di righe dello schema aggiuntivi OLE DB [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] introdotti in native client non saranno disponibili, né verranno apportate modifiche a SQLColumns in ODBC tramite SQL_SOPT_SS_NAME_SCOPE.  
  
 I client legacy possono accedere per nome alle colonne che sono membri del set di colonne **column_set** di tipo sparse e la colonna **column_set** sarà accessibile come colonna XML per i client e come colonna per i client [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Supporto per la copia bulk (BCP) per colonne di tipo sparse  
 Non sono state apportate modifiche all'API BCP in ODBC o OLE DB per le colonne di tipo sparse o le funzionalità di **column_set** .  
  
 Se una tabella include un set di colonne **column_set**, le colonne di tipo sparse non verranno gestite come colonne distinte. I valori di tutte le colonne di tipo sparse sono inclusi nel valore della **column_set**, che viene esportato in modo analogo a una colonna XML. ovvero, come **varbinary (max)** se associato come tipo binario o come **nvarchar (max)** se associato come tipo **char** o **WCHAR** ). Durante l'importazione, il valore **column_set** deve essere conforme allo schema della **column_set**.  
  
 Per le operazioni **queryout** non esiste alcuna modifica al modo in cui sono gestite le colonne a cui si fa esplicitamente riferimento. **column_set** colonne hanno lo stesso comportamento delle colonne XML e la sparsità non ha alcun effetto sulla gestione delle colonne di tipo sparse denominate.  
  
 Se, tuttavia, si utilizza **queryout** per l'esportazione e si fa riferimento a colonne di tipo sparse che sono membri del set di colonne di tipo sparse in base al nome, non è possibile eseguire un'importazione diretta in una tabella dalla struttura analoga. Questo perché BCP usa i metadati coerenti con un'operazione **select &#42;** per l'importazione e non è in grado di trovare corrispondenze **column_set** colonne membro con questi metadati. Per importare colonne membri del set di colonne **column_set** singolarmente, è necessario definire una vista nella tabella che fa riferimento alle colonne **column_set** desiderate ed eseguire l'operazione di importazione utilizzando la vista.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione in SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
