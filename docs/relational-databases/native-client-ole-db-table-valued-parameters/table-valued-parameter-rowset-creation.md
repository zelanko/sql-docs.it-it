---
title: Creazione di set di righe di parametri con valori di tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67ef2448dd1b39bf03a43c942b2206199f087fb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62516050"
---
# <a name="table-valued-parameter-rowset-creation"></a>Creazione di un set di righe di parametri con valori di tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Sebbene i consumer siano in grado di fornire qualsiasi oggetto set di righe per i parametri con valori di tabella, vengono implementati gli oggetti set di righe tipici rispetto agli archivi dati di back-end, con conseguente limitazione delle prestazioni. Per questo motivo, il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client consente ai consumer di creare un oggetto set di righe specializzato nei dati in memoria. Questo oggetto set di righe speciali, in memoria è un nuovo oggetto COM definito un set di righe di parametri con valori di tabella. Tale oggetto fornisce funzionalità simili ai set di parametri.  
  
 Gli oggetti set di righe di parametri con valori di tabella vengono creati in modo esplicito dal consumer per i parametri di input tramite più interfacce a livello di sessione. Esiste una sola istanza di un oggetto set di righe di parametri con valori di tabella per parametro con valori di tabella. Il consumer può creare gli oggetti set di righe di parametri con valori di tabella fornendo le informazioni sui metadati già note (scenario statico) o individuandole tramite le interfacce del provider (scenario dinamico). Nelle sezioni seguenti vengono descritti questi due scenari.  
  
## <a name="static-scenario"></a>Scenario statico  
 Quando le informazioni sul tipo è noto, il consumer utilizza ITableDefinitionWithConstraints::CreateTableWithConstraints per creare un'istanza di un oggetto set di righe di parametri con valori di tabella che corrisponde a un parametro con valori di tabella.  
  
 Il *guid* campo (*pTableID* parametro) contiene il GUID speciale (CLSID_ROWSET_TVP). Il membro *pwszName* contiene il nome del tipo di parametro con valori di tabella di cui il consumer intende creare un'istanza. Il campo *eKind* sarà impostato su DBKIND_GUID_NAME. Questo nome è necessario quando si tratta di un'istruzione SQL ad hoc; il nome è facoltativo se è una chiamata di procedura.  
  
 Per l'aggregazione il consumer passa il *pUnkOuter* parametro con l'interfaccia IUnknown di controllo.  
  
 Le proprietà dell'oggetto parametro con valori di tabella di righe sono di sola lettura, in modo che il consumer non deve impostare alcuna proprietà *rgPropertySets*.  
  
 Per il membro *rgPropertySets* di ogni struttura DBCOLUMNDESC, il consumer può specificare proprietà aggiuntive per ogni colonna. Queste proprietà appartengono al set di proprietà DBPROPSET_SQLSERVERCOLUMN. Tali proprietà consentono di specificare le impostazioni predefinite e calcolate per ogni colonna. Supportano inoltre le proprietà esistenti della colonna, ad esempio nullability e identity.  
  
 Per recuperare le informazioni corrispondenti da un oggetto set di righe di parametri con valori di tabella, il consumer usa IRowsetInfo::GetProperties.  
  
 Per recuperare informazioni su null, univoco, calcolata e aggiornare lo stato di ogni colonna, il consumer utilizza IColumnsRowset:: o IColumnsInfo:: GetColumnInfo. Questi metodi forniscono informazioni dettagliate su ogni colonna del set di righe di parametri con valori di tabella.  
  
 Il consumer specifica il tipo di ogni colonna del parametro con valori di tabella, analogamente al modo in cui vengono specificate le colonne quando viene creata una tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il consumer Ottiene un oggetto set di righe di parametri con valori di tabella dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Provider OLE DB tramite il *ppRowset* parametro di output.  
  
## <a name="dynamic-scenario"></a>Scenario dinamico  
 Quando il consumer non dispone di informazioni sul tipo, IOpenRowset:: OPENROWSET da usare per creare istanze degli oggetti set di righe di parametri con valori di tabella. L'unica informazione che il consumer deve fornire al provider è il nome del tipo.  
  
 In questo scenario, il provider ottiene le informazioni sul tipo relative a un oggetto set di righe di parametri con valori di tabella dal server per conto del consumer.  
  
 Il *pTableID* e *pUnkOuter* parametri devono essere impostati come nello scenario statico. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Provider OLE DB Native quindi Ottiene le informazioni sul tipo (informazioni sulle colonne e vincoli) dal server e restituire un oggetto set di righe di parametri con valori di tabella tramite il *ppRowset* parametro. Questa operazione richiede la comunicazione con il server e pertanto non viene eseguita rispetto allo scenario statico. Lo scenario dinamico funziona solo con le chiamate di procedura con parametri.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
