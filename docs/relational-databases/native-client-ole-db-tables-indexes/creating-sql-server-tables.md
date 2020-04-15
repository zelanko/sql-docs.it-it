---
title: Creazione di tabelle di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f3d1ae29828e18cf98941666e7884e70115ba39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301862"
---
# <a name="creating-sql-server-tables"></a>Creazione di tabelle di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client espone la funzione **ITableDefinition::CreateTable,** consentendo ai consumer di creare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle. I consumer utilizzano **CreateTable** per creare tabelle permanenti con nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer e tabelle permanenti o temporanee con nomi univoci generati dal provider OLE DB di Native Client.  
  
 Quando il consumer chiama **ITableDefinition::CreateTable**, se il valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] della proprietà DBPROP_TBL_TEMPTABLE è VARIANT_TRUE, il provider OLE DB Native Client genera un nome di tabella temporaneo per il consumer. Il consumer imposta il parametro *pTableID* del metodo **CreateTable** su NULL. Le tabelle temporanee con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i nomi generati dal provider OLE DB Native Client non vengono visualizzate nel set di righe **TABLES,** ma sono accessibili tramite l'interfaccia **IOpenRowset.**  
  
 Quando i consumer specificano il nome della tabella nel membro *pwszName* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'unione *uName* nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametro *pTableID,* il provider OLE DB Native Client crea una tabella con tale nome. Vengono applicati i vincoli di denominazione di tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il nome tabella può indicare una tabella permanente o una tabella temporanea locale o globale. Per altre informazioni, vedere [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md). Il parametro *ppTableID* può essere NULL.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client può generare i nomi delle tabelle permanenti o temporanee. Quando il consumer imposta il parametro *pTableID* su NULL e\*imposta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *ppTableID* in modo che punti a un DBID valido, il provider OLE DB Native Client restituisce il nome generato della tabella nel membro *pwszName* dell'unione *uName* del DBID a cui punta il valore di *ppTableID*. Per creare una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella temporanea con nome provider OLE DB Native Client, il consumer include la proprietà della tabella OLE DB DBPROP_TBL_TEMPTABLE in un set di proprietà della tabella a cui viene fatto riferimento nel parametro *rgPropertySets.* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Le tabelle temporanee denominate dal provider OLE DB Native Client sono locali.  
  
 **CreateTable** restituisce DB_E_BADTABLEID se il membro *eKind* del parametro *pTableID* non indica DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Utilizzo di DBCOLUMNDESC  
 Il consumer può indicare un tipo di dati della colonna tramite il membro *pwszTypeName* o il membro *wType*. Se il consumer specifica il tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in *pwszTypeName*, il provider OLE DB Native Client ignora il valore di *wType*.  
  
 Se si usa il membro *pwszTypeName*, il consumer specifica il tipo di dati usando i nomi dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I nomi dei tipi di dati validi sono quelli restituiti nella colonna TYPE_NAME del set di righe dello schema PROVIDER_TYPES.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client riconosce un subset di valori DBTYPE enumerati da OLE DB nel membro *wType.* Per altre informazioni, vedere [Mapping dei tipi di dati in ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** restituisce DB_E_BADTYPE se il consumer imposta il membro *pTypeInfo* o *pclsid* per specificare il tipo di dati della colonna.  
  
 Il consumer specifica il nome di colonna nel membro *pwszName* dell'unione *uName* del membro *dbcid* di DBCOLUMNDESC. Il nome di colonna viene specificato come stringa di caratteri Unicode. Il membro *eKind* di *dbcid* deve essere DBKIND_NAME. **CreateTable** restituisce DB_E_BADCOLUMNID se *eKind* non è valido, se *pwszName* è NULL o se il valore di *pwszName* non è un identificatore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido.  
  
 Tutte le proprietà delle colonne sono disponibili in tutte le colonne definite per la tabella. **CreateTable** può restituire DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED in caso di conflitto tra i valori di proprietà impostati. **CreateTable** restituisce un errore quando impostazioni delle proprietà delle colonne non valide determinano un errore di creazione tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Le proprietà delle colonne in un parametro DBCOLUMNDESC vengono interpretate nel modo seguente.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE Descrizione: imposta la proprietà Identity nella colonna creata. Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la proprietà Identity è valida per una singola colonna all'interno di una tabella. L'impostazione della proprietà su VARIANT_TRUE per più [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di una singola colonna genera un errore quando il provider OLE DB Native Client tenta di creare la tabella nel server.<br /><br /> La proprietà Identity di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è valida solo per i tipi **integer**, **numeric** e **decimal** quando la scala è 0. L'impostazione della proprietà su VARIANT_TRUE in una colonna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di qualsiasi altro tipo di dati genera un errore quando il provider OLE DB Native Client tenta di creare la tabella nel server.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce DB_S_ERRORSOCCURRED quando DBPROP_COL_AUTOINCREMENT e DBPROP_COL_NULLABLE sono sia VARIANT_TRUE che *dwOption* di DBPROP_COL_NULLABLE non è DBPROPOPTIONS_REQUIRED. DB_E_ERRORSOCCURRED viene restituito quando DBPROP_COL_AUTOINCREMENT e DBPROP_COL_NULLABLE sono entrambe VARIANT_TRUE e il membro *dwOption* di DBPROP_COL_NULLABLE è uguale a DBPROPOPTIONS_REQUIRED. La colonna viene definita con la proprietà Identity di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il membro *dwStatus* di DBPROP_COL_NULLABLE viene impostato su DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: crea un vincolo DEFAULT di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la colonna.<br /><br /> Il membro *vValue* di DBPROP può essere uno qualsiasi di diversi tipi. Il membro *vValue.vt* deve specificare un tipo compatibile con il tipo di dati della colonna. La definizione di BSTR N/A come valore predefinito per una colonna definita come DBTYPE_WSTR rappresenta una corrispondenza compatibile. La definizione dello stesso valore predefinito in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una colonna definita come DBTYPE_R8 genera un errore quando il provider OLE DB Native Client tenta di creare la tabella nel server.|  
|DBPROP_COL_DESCRIPTION|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: la proprietà DBPROP_COL_DESCRIPTION della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colonna non viene implementata dal provider OLE DB di Native Client.<br /><br /> Il membro *dwStatus* della struttura DBPROP restituisce DBPROPSTATUS_NOTSUPPORTED quando il consumer tenta di scrivere il valore della proprietà.<br /><br /> L'impostazione della proprietà non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] costituisce un errore irreversibile per il provider OLE DB di Native Client. Se tutti gli altri valori di parametro sono validi, viene creata la tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il provider OLE DB native Client utilizza DBPROP_COL_FIXEDLENGTH per determinare il mapping dei tipi di dati quando il consumer definisce il tipo di dati di una colonna utilizzando il membro *wType* di DBCOLUMNDESC. Per altre informazioni, vedere [Mapping dei tipi di dati in ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: nessuna<br /><br /> Descrizione: quando si crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la tabella, il provider OLE DB Native Client indica se la colonna deve accettare valori null se la proprietà è impostata. Quando la proprietà non è impostata, la possibilità di accettare valori NULL per la colonna è determinata dall'opzione di database predefinita ANSI_NULLS di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client è un provider compatibile con ISO. Le sessioni connesse adottano comportamenti ISO. Se il consumer non imposta DBPROP_COL_NULLABLE, le colonne accettano valori Null.|  
|DBPROP_COL_PRIMARYKEY|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE Descrizione: quando VARIANT_TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client crea la colonna con un vincolo PRIMARY KEY.<br /><br /> Se definita come proprietà della colonna, solo una singola colonna può determinare il vincolo. L'impostazione della proprietà VARIANT_TRUE per più [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di una singola colonna restituisce [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un errore quando il provider OLE DB Native Client tenta di creare la tabella.<br /><br /> Nota: il consumer può usare **IIndexDefinition::CreateIndex** per creare un vincolo PRIMARY KEY in due o più colonne.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce DB_S_ERRORSOCCURRED quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE sono VARIANT_TRUE e *dwOption* di DBPROP_COL_UNIQUE non è DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED viene restituito quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE sono entrambe VARIANT_TRUE e il membro *dwOption* di DBPROP_COL_UNIQUE è uguale a DBPROPOPTIONS_REQUIRED. La colonna viene definita con la proprietà Identity di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il membro *dwStatus* di DBPROP_COL_PRIMARYKEY viene impostato su DBPROPSTATUS_CONFLICTING.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce un errore quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_NULLABLE sono entrambi VARIANT_TRUE.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client restituisce un errore da quando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer tenta di creare un vincolo PRIMARY KEY in una colonna di tipo di dati non valido. Non è possibile definire vincoli PRIMARY KEY in colonne create con i tipi di dati **bit**, **text**, **ntext** e **image** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_UNIQUE|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE Descrizione: applica un vincolo UNIQUE di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alla colonna.<br /><br /> Se è definita come proprietà della colonna, il vincolo viene applicato solo a una singola colonna. Il consumer può usare **IIndexDefinition::CreateIndex** per applicare un vincolo UNIQUE nei valori combinati di due o più colonne.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce DB_S_ERRORSOCCURRED quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE sono sia VARIANT_TRUE che *dwOption* non è DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED viene restituito quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE sono entrambe VARIANT_TRUE e *dwOption* è uguale a DBPROPOPTIONS_REQUIRED. La colonna viene definita con la proprietà Identity di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il membro *dwStatus* di DBPROP_COL_PRIMARYKEY viene impostato su DBPROPSTATUS_CONFLICTING.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce DB_S_ERRORSOCCURRED quando DBPROP_COL_NULLABLE e DBPROP_COL_UNIQUE sono sia VARIANT_TRUE che *dwOption* non è DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED viene restituito quando DBPROP_COL_NULLABLE e DBPROP_COL_UNIQUE sono entrambe VARIANT_TRUE e *dwOption* è uguale a DBPROPOPTIONS_REQUIRED. La colonna viene definita con la proprietà Identity di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il membro *dwStatus* di DBPROP_COL_NULLABLE viene impostato su DBPROPSTATUS_CONFLICTING.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client restituisce un errore da quando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer tenta di creare un vincolo UNIQUE su una colonna di tipo di dati non valido. Non è possibile definire vincoli UNIQUE in colonne create con il tipo di dati  **bit** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Quando il consumer chiama **ITableDefinition::CreateTable**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client interpreta le proprietà della tabella come indicato di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|L/S: Lettura/Scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE descrizione: per impostazione predefinita, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client crea tabelle denominate dal consumer. Quando VARIANT_TRUE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il provider OLE DB Native Client genera un nome di tabella temporaneo per il consumer. Il consumer imposta il parametro *pTableID* di **CreateTable** su NULL. Il parametro *ppTableID* deve contenere un puntatore valido.|  
  
 Se il consumer richiede che un set di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] righe venga aperto in una tabella creata correttamente, il provider OLE DB Native Client apre un set di righe supportato dal cursore. Qualsiasi proprietà del set di righe può essere indicata nei set di proprietà passati.  
  
 In questo esempio viene creata una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
