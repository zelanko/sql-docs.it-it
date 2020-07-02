---
title: Set di righe LINKEDSERVERS (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e4d0c26821cfc9870dc2e5f01f7927257599fe4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787689"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>Set di righe dello schema - Set di righe LINKEDSERVERS
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Il set di righe **LINKEDSERVERS** enumera le origini dati dell'organizzazione che possono partecipare nelle query distribuite di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Il set di righe **LINKEDSERVERS** contiene le colonne seguenti.  
  
|Nome colonna|Indicatore del tipo|Descrizione|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|Nome di un server collegato.|  
|SVR_PRODUCT|DBTYPE_WSTR|Produttore o altro nome che identifica il tipo di archivio dati rappresentato dal nome del server collegato.|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|Nome descrittivo del provider OLE DB impiegato per utilizzare dati dal server.|  
|SVR_DATASOURCE|DBTYPE_WSTR|Stringa OLE DB DBPROP_INIT_DATASOURCE utilizzata per acquisire un'origine dati dal provider.|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|Valore OLE DB DBPROP_INIT_PROVIDERSTRING utilizzato per acquisire un'origine dati dal provider.|  
|SVR_LOCATION|DBTYPE_WSTR|Stringa OLE DB DBPROP_INIT_LOCATION utilizzata per acquisire un'origine dati dal provider.|  
  
 Il set di righe viene ordinato su SRV_NAME e una singola restrizione è supportata su SRV_NAME.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto del set di righe dello schema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
  
