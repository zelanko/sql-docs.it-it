---
title: Supporto di query distribuite nei set di righe dello schema | Microsoft Docs
description: L'interfaccia IDBSchemaRowset di OLE DB Driver per SQL Server restituisce metadati sui server collegati per supportare le query SQL Server distribuite.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61105b2e974cd111cd4f5dfd10e7f528cd04519a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861559"
---
# <a name="schema-rowsets---distributed-query-support"></a>Set di righe dello schema - Supporto di query distribuite
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Per supportare query distribuite di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'interfaccia **IDBSchemaRowset** del driver OLE DB per SQL Server restituisce metadati sui server collegati.  
  
 Se la proprietà SSPROP_QUOTEDCATALOGNAMES di DBPROPSET_SQLSERVERSESSION è VARIANT_TRUE, è possibile utilizzare un identificatore tra virgolette per specificare il nome di catalogo (ad esempio "catalogo.personale"). Quando si restringe l'output del set di righe dello schema restituito in base al catalogo, il driver OLE DB per SQL Server riconosce un nome in due parti che contiene il server collegato e il nome del catalogo. Per il set di righe dello schema riportato nella tabella seguente, la specifica di un nome di catalogo in due parti, quale _linked\_server_ **.** _catalog_, restringe l'output al catalogo applicabile del server collegato denominato.  
  
|Set di righe dello schema|Restrizione per catalogo|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  Per limitare un set di righe dello schema a tutti i cataloghi di un server collegato, usare la sintassi *linked_server* (dove il separatore carattere di sottolineatura fa parte della specifica del nome). Questa sintassi è equivalente alla specifica di NULL come restrizione del nome di catalogo e viene utilizzata anche quando il server collegato indica un'origine dati che non supporta cataloghi.  
 
 Il driver OLE DB per SQL Server definisce il set di righe dello schema LINKEDSERVERS restituendo un elenco delle origini dati OLE DB registrate come server collegati.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto del set di righe dello schema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [Set di righe LINKEDSERVERS &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
