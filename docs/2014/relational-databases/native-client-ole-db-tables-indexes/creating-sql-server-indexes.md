---
title: Creazione di indici SQL Server | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bda39528b6bc04fbff6faa4c72d85a4eccd576c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046455"
---
# <a name="creating-sql-server-indexes"></a>Creazione di indici SQL Server
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client espone il **iindexdefinition:: CreateIndex** funzione, che consente agli utenti di definire nuovi indici nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client crea indici di tabella come indici o vincoli. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce privilegio di creazione del vincolo al proprietario della tabella, del database e ai membri di determinati ruoli amministrativi. Per impostazione predefinita, solo il proprietario di tabella può creare un indice in una tabella. L'esito positivo o negativo di **CreateIndex** dipende quindi non solo dai diritti di accesso dell'utente dell'applicazione ma anche dal tipo di indice creato.  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di*pTableID* deve essere DBKIND_NAME.  
  
 Il *pIndexID* parametro può essere NULL e se si tratta, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client crea un nome univoco per l'indice. Il consumer può acquisire il nome dell'indice specificando un puntatore valido a un DBID nel parametro *ppIndexID*.  
  
 Il consumer può specificare il nome dell'indice come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* del parametro *pTableID*. Il membro *eKind* di *pIndexID* deve essere DBKIND_NAME.  
  
 Il consumer specifica la colonna o le colonne utilizzate nell'indice in base al nome. Per ogni struttura DBINDEXCOLUMNDESC usata in **CreateIndex**, il membro *eKind* di *pColumnID* deve essere DBKIND_NAME. Il nome della colonna viene specificato come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* in *pColumnID*.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano l'ordine crescente sui valori nell'indice. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce E_INVALIDARG se il consumer specifica DBINDEX_COL_ORDER_DESC in una qualsiasi struttura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta le proprietà di indice come segue.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Clustering dell'indice i controlli.<br /><br /> VARIANT_TRUE: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client tenta di creare un indice cluster sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta al massimo un indice con cluster su una tabella.<br /><br /> VARIANT_FALSE: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client tenta di creare un indice non cluster per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella.|  
|DBPROP_INDEX_FILLFACTOR|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: 0<br /><br /> Descrizione: Specifica la percentuale di una pagina di indice usata per l'archiviazione. Per altre informazioni, vedere [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql).<br /><br /> Il tipo della variante è VT_I4. Deve essere maggiore o uguale a 1 e minore o uguale a 100.|  
|DBPROP_INDEX_INITIALIZE|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE descrizione: Crea l'indice come integrità referenziale, vincolo PRIMARY KEY.<br /><br /> VARIANT_TRUE: L'indice viene creato per supportare il vincolo di chiave primaria della tabella. È necessario che le colonne non ammettano valori Null.<br /><br /> VARIANT_FALSE: L'indice non viene utilizzato come un vincolo PRIMARY KEY per i valori di riga nella tabella.|  
|DBPROP_INDEX_SORTBOOKMARKS|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: None<br /><br /> Descrizione: Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|L/S: lettura/scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Crea l'indice come vincolo UNIQUE nella colonna o colonne.<br /><br /> VARIANT_TRUE: L'indice viene utilizzato per vincolare in modo univoco i valori di riga nella tabella.<br /><br /> VARIANT_FALSE: L'indice non vincola in modo univoco i valori di riga.|  
  
 Nel provider specifici set di proprietà DBPROPSET_SQLSERVERINDEX il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client definisce la proprietà di informazioni di origine dati seguente.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Digitare:  VT_BOOL (R/W)<br /><br /> Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Quando questa proprietà viene specificata con un valore VARIANT_TRUE con iindexdefinition:: CreateIndex, viene generato in un indice xml primario viene creato corrispondente alla colonna da indicizzare. Se questa proprietà è VARIANT_TRUE, cIndexColumnDescs deve essere 1, in caso contrario si tratta di un errore.|  
  
 In questo esempio viene creato un indice di chiave primaria:  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
