---
title: Mapping dei tipi di dati in ITableDefinition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3e828efa513db1ace272e59379f77d063220290
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297031"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapping dei tipi di dati in ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando si creano tabelle utilizzando la funzione **ITableDefinition::CreateTable** , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client può specificare i tipi di dati nel membro *pwszTypeName* della matrice DBCOLUMNDESC passata. Se il consumer specifica il tipo di dati di una colonna in base al nome, il mapping del tipo di dati OLE DB rappresentato dal membro *wType* della struttura DBCOLUMNDESC viene ignorato.  
  
 Quando si specificano nuovi tipi di dati di colonna con tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati OLE DB utilizzando il membro *wType* della struttura DBCOLUMNDESC , il provider OLE DB di Native Client esegue il mapping dei tipi di dati OLE DB come indicato di seguito.  
  
|Tipo di dati OLE DB|SQL Server<br /><br /> Tipo di dati|Informazioni aggiuntive|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** o **varbinary(max)**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client esamina il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione dell'istanza, il provider OLE DB Native Client esegue il mapping del tipo a **image**.<br /><br /> Se il valore di *ulColumnSize* è inferiore alla lunghezza massima [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di una colonna di tipo di dati **binari,** il provider OLE DB di Native Client esamina il membro DBCOLUMNDESC *rgPropertySets.* Se DBPROP_COL_FIXEDLENGTH è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, il provider OLE DB Native Client esegue il mapping del tipo a **binary**. Se il valore della proprietà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è VARIANT_FALSE, il provider OLE DB Native Client esegue il mapping del tipo a **varbinary**. In entrambi i casi il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di SQL Server creata.|  
|DBTYPE_CY|**Soldi**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**UNIQUEIDENTIFIER**||  
|DBTYPE_I2|**Smallint**||  
|DBTYPE_I4|**Int**||  
|DBTYPE_NUMERIC|**Numerico**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client esamina i membri DBCOLUMDESC *bPrecision* e *bScale* per determinare la precisione e la scala per la colonna **numerica.**|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**Galleggiante**||  
|DBTYPE_STR|**char**, **varchar**, **text,** o **varchar(max)**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client esamina il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione dell'istanza, il provider OLE DB Native Client esegue il mapping del tipo a **text**.<br /><br /> Se il valore di *ulColumnSize* è inferiore alla lunghezza massima di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una colonna di tipo di dati carattere multibyte, il provider OLE DB di Native Client esamina il membro DBCOLUMNDESC *rgPropertySets* . Se DBPROP_COL_FIXEDLENGTH è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, il provider OLE DB Native Client esegue il mapping del tipo a **char**. Se il valore della proprietà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è VARIANT_FALSE, il provider OLE DB Native Client esegue il mapping del tipo a **varchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_UDT|**Udt**|Le informazioni seguenti vengono usate nelle strutture **DBCOLUMNDESC** impiegate da **ITableDefinition::CreateTable** quando sono necessarie colonne di tipo definito dall'utente:<br /><br /> *pwSzTypeName* viene ignorato.<br /><br /> *rgPropertySets* deve includere un set di proprietà **DBPROPSET_SQLSERVERCOLUMN**, come descritto nella sezione **DBPROPSET_SQLSERVERCOLUMN**, in [Uso dei tipi definiti dall'utente](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**Tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** o **nvarchar(max)**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client esamina il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valore, il provider OLE DB Native Client esegue il mapping del tipo a **ntext**.<br /><br /> Se il valore di *ulColumnSize* è inferiore alla lunghezza massima di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una colonna di tipo di dati carattere Unicode, il provider OLE DB di Native Client esamina il membro DBCOLUMNDESC *rgPropertySets* . Se DBPROP_COL_FIXEDLENGTH è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, il provider OLE DB Native Client esegue il mapping del tipo a **nchar**. Se il valore della proprietà [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è VARIANT_FALSE, il provider OLE DB Native Client esegue il mapping del tipo a **nvarchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_XML|**Xml**||  
  
> [!NOTE]  
>  In caso di creazione di una nuova tabella, il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue il mapping solo dei valori di enumerazione del tipo di dati OLE DB specificati nella tabella precedente. Il tentativo di creare una tabella con una colonna di qualsiasi altro tipo di dati OLE DB DB genera un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
