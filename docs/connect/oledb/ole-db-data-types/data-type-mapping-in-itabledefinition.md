---
title: Mapping dei tipi di dati in ITableDefinition | Microsoft Docs
description: Mapping dei tipi di dati in ITableDefinition
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 5dcd4b33121d5459120572b2b31de413106aeeda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66775603"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapping dei tipi di dati in ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  In caso di creazione di tabelle tramite la funzione **ITableDefinition::CreateTable**, il consumer del driver OLE DB per SQL Server può specificare tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel membro *pwszTypeName* della matrice DBCOLUMNDESC passata. Se il consumer specifica il tipo di dati di una colonna in base al nome, il mapping del tipo di dati OLE DB rappresentato dal membro *wType* della struttura DBCOLUMNDESC viene ignorato.  
  
 Per specificare nuovi tipi di dati di colonna con tipi di dati OLE DB mediante il membro *wType* della struttura DBCOLUMNDESC, il driver OLE DB per SQL Server esegue il mapping dei tipi di dati OLE DB come segue.  
  
|Tipo di dati OLE DB|SQL Server<br /><br /> Tipo di dati|Informazioni aggiuntive|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** o **varbinary(max)**|Il Driver OLE DB per SQL Server esamina il *ulColumnSize* membro della struttura DBCOLUMNDESC. Base, il valore e la versione del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dell'istanza, il Driver OLE DB per SQL Server esegue il mapping di tipo da **immagine**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna del tipo di dati **binary**, il driver OLE DB per SQL Server controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il Driver OLE DB per SQL Server viene eseguito il mapping di tipo **binario**. Se il valore della proprietà è VARIANT_FALSE, il Driver OLE DB per SQL Server viene eseguito il mapping di tipo **varbinary**. In entrambi i casi il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di SQL Server creata.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|Il driver OLE DB per SQL Server controlla i membri *bPrecision* e *bScale* di DBCOLUMDESC per determinare la precisione e la scala per la colonna **numeric**.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text,** o **varchar(max)**|Il Driver OLE DB per SQL Server esamina il *ulColumnSize* membro della struttura DBCOLUMNDESC. In base al valore e una versione del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dell'istanza, il Driver OLE DB per SQL Server esegue il mapping di tipo da **testo**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna del tipo di dati multibyte, il driver OLE DB per SQL Server controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il Driver OLE DB per SQL Server viene eseguito il mapping di tipo **char**. Se il valore della proprietà è VARIANT_FALSE, il Driver OLE DB per SQL Server viene eseguito il mapping di tipo **varchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_UDT|**UDT**|Le informazioni seguenti vengono usate nelle strutture **DBCOLUMNDESC** impiegate da **ITableDefinition::CreateTable** quando sono necessarie colonne di tipo definito dall'utente:<br /><br /> *pwSzTypeName* viene ignorato.<br /><br /> *rgPropertySets* deve includere una **DBPROPSET_SQLSERVERCOLUMN** proprietà impostata come descritto nella sezione sul **DBPROPSET_SQLSERVERCOLUMN**nella [User-Defined Type ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** o **nvarchar(max)**|Il Driver OLE DB per SQL Server esamina il *ulColumnSize* membro della struttura DBCOLUMNDESC. In base al valore, il Driver OLE DB per SQL Server esegue il mapping di tipo da **ntext**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna del tipo di dati Unicode, il driver OLE DB per SQL Server controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il Driver OLE DB per SQL Server viene eseguito il mapping di tipo **nchar**. Se il valore della proprietà è VARIANT_FALSE, il Driver OLE DB per SQL Server viene eseguito il mapping di tipo **nvarchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  In caso di creazione di una nuova tabella, il driver OLE DB per SQL Server esegue il mapping solo dei valori di enumerazione del tipo di dati OLE DB specificati nella tabella precedente. Il tentativo di creare una tabella con una colonna di qualsiasi altro tipo di dati OLE DB DB genera un errore.  

## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
