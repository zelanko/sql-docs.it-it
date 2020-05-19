---
title: Mapping dei tipi di dati in ITableDefinition | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 55c84e62326b7b1aa8619bf57ffccf16c43aec67
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705128"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapping dei tipi di dati in ITableDefinition
  Quando si creano tabelle tramite la funzione **ITableDefinition:: CreateTable** , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider di OLE DB di Native client può specificare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati nel membro *pwszTypeName* della matrice DBCOLUMNDESC che viene passata. Se il consumer specifica il tipo di dati di una colonna in base al nome, il mapping del tipo di dati OLE DB rappresentato dal membro *wType* della struttura DBCOLUMNDESC viene ignorato.  
  
 Quando si specificano nuovi tipi di dati di colonna con OLE DB tipi di dati utilizzando il membro della struttura DBCOLUMNDESC *wType* , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native client esegue il mapping OLE DB tipi di dati come indicato di seguito.  
  
|Tipo di dati OLE DB|SQL Server<br /><br /> Tipo di dati|Informazioni aggiuntive|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** o **varbinary(max)**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore e alla versione dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client esegue il mapping del tipo a **Image**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna con tipo di dati **binario** , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native client esegue il mapping del tipo a **Binary**. Se il valore della proprietà è VARIANT_FALSE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native client esegue il mapping del tipo a **varbinary**. In entrambi i casi il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di SQL Server creata.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla i membri *BPrecision* e *bScale* di DBCOLUMDESC per determinare la precisione e la scala per la colonna **numerica** .|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text,** o **varchar(max)**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore e alla versione dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client esegue il mapping del tipo al **testo**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna con tipo di dati character multibyte, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native client esegue il mapping del tipo a **char**. Se il valore della proprietà è VARIANT_FALSE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native client esegue il mapping del tipo a **varchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_UDT|**UDT**|Le informazioni seguenti vengono utilizzate nelle `DBCOLUMNDESC` strutture da **ITableDefinition:: CreateTable** quando sono richieste le colonne UDT:<br /><br /> -   *pwszTypeName* viene ignorato.<br />-   *rgPropertySets* deve includere un `DBPROPSET_SQLSERVERCOLUMN` set di proprietà, come descritto nella sezione relativa all' `DBPROPSET_SQLSERVERCOLUMN` [uso di tipi definiti dall'utente](../native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** o **nvarchar(max)**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla il membro *ulColumnSize* della struttura DBCOLUMNDESC. In base al valore, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client esegue il mapping del tipo a **ntext**.<br /><br /> Se il valore di *ulColumnSize* è minore della lunghezza massima di una colonna con tipo di dati carattere Unicode, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client controlla il membro *rgPropertySets* di DBCOLUMNDESC. Se DBPROP_COL_FIXEDLENGTH è VARIANT_TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native client esegue il mapping del tipo a **nchar**. Se il valore della proprietà è VARIANT_FALSE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client esegue il mapping del tipo a **nvarchar**. In entrambi i casi, il membro *ulColumnSize* di DBCOLUMNDESC determina la larghezza della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creata.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  In caso di creazione di una nuova tabella, il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue il mapping solo dei valori di enumerazione del tipo di dati OLE DB specificati nella tabella precedente. Il tentativo di creare una tabella con una colonna di qualsiasi altro tipo di dati OLE DB DB genera un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
