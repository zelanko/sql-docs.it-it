---
title: Creazione di indici di SQL Server | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3693355eec7a290c03658c10db500161aa52062d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017906"
---
# <a name="creating-sql-server-indexes"></a>Creazione di indici SQL Server
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client espone la funzione **IIndexDefinition:: CreateIndex** , consentendo ai consumer di definire nuovi indici nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client crea indici di tabella come indici o vincoli. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce privilegio di creazione del vincolo al proprietario della tabella, del database e ai membri di determinati ruoli amministrativi. Per impostazione predefinita, solo il proprietario di tabella può creare un indice in una tabella. L'esito positivo o negativo di **CreateIndex** dipende quindi non solo dai diritti di accesso dell'utente dell'applicazione ma anche dal tipo di indice creato.  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di*pTableID* deve essere DBKIND_NAME.  
  
 Il parametro *pIndexID* può essere null e, in caso contrario, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client crea un nome univoco per l'indice. Il consumer può acquisire il nome dell'indice specificando un puntatore valido a un DBID nel parametro *ppIndexID*.  
  
 Il consumer può specificare il nome dell'indice come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* del parametro *pTableID*. Il membro *eKind* di *pIndexID* deve essere DBKIND_NAME.  
  
 Il consumer specifica la colonna o le colonne utilizzate nell'indice in base al nome. Per ogni struttura DBINDEXCOLUMNDESC usata in **CreateIndex**, il membro *eKind* di *pColumnID* deve essere DBKIND_NAME. Il nome della colonna viene specificato come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* in *pColumnID*.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'ordinamento crescente in base ai valori dell'indice. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client restituisce E_INVALIDARG se il consumer specifica DBINDEX_COL_ORDER_DESC in qualsiasi struttura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta le proprietà di indice come segue.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|R/W (L/S): Lettura/Scrittura<br /><br /> Predefinito: VARIANT_FALSE<br /><br /> Descrizione: controlla il clustering dell'indice.<br /><br /> VARIANT_TRUE: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client tenta di creare un indice cluster nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta al massimo un indice con cluster su una tabella.<br /><br /> VARIANT_FALSE: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client tenta di creare un indice non cluster nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella.|  
|DBPROP_INDEX_FILLFACTOR|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: 0<br /><br /> Descrizione: specifica la percentuale di una pagina di indice utilizzata per l'archiviazione. Per altre informazioni, vedere [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql).<br /><br /> Il tipo della variante è VT_I4. Deve essere maggiore o uguale a 1 e minore o uguale a 100.|  
|DBPROP_INDEX_INITIALIZE|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: descrizione VARIANT_FALSE: crea l'indice come integrità referenziale, vincolo PRIMARY KEY.<br /><br /> VARIANT_TRUE: l'indice viene creato per supportare il vincolo PRIMARY KEY della tabella. È necessario che le colonne non ammettano valori Null.<br /><br /> VARIANT_FALSE: l'indice non viene utilizzato come vincolo PRIMARY KEY per i valori di riga nella tabella.|  
|DBPROP_INDEX_SORTBOOKMARKS|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|R/W (L/S): Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client non supporta questa proprietà. I tentativi di impostare la proprietà in **CreateIndex** determinano un valore restituito DB_S_ERRORSOCCURRED. Il membro *dwStatus* della struttura di proprietà indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|R/W (L/S): Lettura/Scrittura<br /><br /> Predefinito: VARIANT_FALSE<br /><br /> Descrizione: crea l'indice come vincolo UNIQUE nella colonna o nelle colonne utilizzate.<br /><br /> VARIANT_TRUE: l'indice viene utilizzato per vincolare in modo univoco i valori della tabella.<br /><br /> VARIANT_FALSE: l'indice non vincola in modo univoco i valori di riga.|  
  
 Nel set di proprietà specifico del provider DBPROPSET_SQLSERVERINDEX, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client definisce la seguente proprietà delle informazioni sull'origine dati.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Tipo: VT_BOOL (L/S)<br /><br /> Predefinito: VARIANT_FALSE<br /><br /> Descrizione: quando questa proprietà viene specificata con un valore VARIANT_TRUE con IIndexDefinition::CreateIndex, determina la creazione di un indice xml primario corrispondente alla colonna indicizzata. Se questa proprietà è VARIANT_TRUE, cIndexColumnDescs deve essere 1, in caso contrario si tratta di un errore.|  
  
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
  
  
