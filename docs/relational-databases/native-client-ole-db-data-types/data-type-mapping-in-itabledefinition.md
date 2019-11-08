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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bdf3a1e716fd1de5354b735e353916bab863059c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73774311"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapping dei tipi di dati in ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando si creano tabelle tramite la funzione **ITableDefinition:: CreateTable** , il consumer del provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client può specificare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati nel membro *PWSZTYPENAME* della matrice DBCOLUMNDESC passata. Se il consumer specifica il tipo di dati di una colonna in base al nome, il mapping del tipo di dati OLE DB rappresentato dal membro *wType* della struttura DBCOLUMNDESC viene ignorato.  
  
 Quando si specificano nuovi tipi di dati di colonna con OLE DB tipi di dati utilizzando il membro della struttura DBCOLUMNDESC *wType* , il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client esegue il mapping OLE DB tipi di dati come indicato di seguito.  
  
|Tipo di dati OLE DB|SQL Server<br /><br /> Tipo di dati|Informazioni aggiuntive|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** o **varbinary(max)**|Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controlla il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore e alla versione dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il provider di OLE DB Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il mapping del tipo all' **immagine**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna con tipo di dati **binario** , il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client esegue il mapping del tipo a **Binary**. Se il valore della proprietà è VARIANT_FALSE, il provider di OLE DB Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il mapping del tipo a **varbinary**. In entrambi i casi il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di SQL Server creata.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|Il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB controlla i membri *bPrecision* e *bScale* di DBCOLUMDESC per determinare la precisione e la scala per la colonna **numerica** .|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text,** o **varchar(max)**|Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controlla il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore e alla versione dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client esegue il mapping del tipo al **testo**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna con tipo di dati character multibyte, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client esegue il mapping del tipo a **char**. Se il valore della proprietà è VARIANT_FALSE, il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Native client esegue il mapping del tipo a **varchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_UDT|**UDT**|Le informazioni seguenti vengono usate nelle strutture **DBCOLUMNDESC** impiegate da **ITableDefinition::CreateTable** quando sono necessarie colonne di tipo definito dall'utente:<br /><br /> *pwSzTypeName* viene ignorato.<br /><br /> *rgPropertySets* deve includere un set di proprietà **DBPROPSET_SQLSERVERCOLUMN** come descritto nella sezione **DBPROPSET_SQLSERVERCOLUMN**, in [uso di tipi definiti dall'utente](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** o **nvarchar(max)**|Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controlla il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client esegue il mapping del tipo a **ntext**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna con tipo di dati carattere Unicode, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client esegue il mapping del tipo a **nchar**. Se il valore della proprietà è VARIANT_FALSE, il provider di OLE DB Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il mapping del tipo a **nvarchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  In caso di creazione di una nuova tabella, il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue il mapping solo dei valori di enumerazione del tipo di dati OLE DB specificati nella tabella precedente. Il tentativo di creare una tabella con una colonna di qualsiasi altro tipo di dati OLE DB DB genera un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi &#40;di dati OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
