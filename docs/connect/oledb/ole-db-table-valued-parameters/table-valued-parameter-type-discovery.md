---
title: Individuazione del tipo di parametro con valori di tabella | Microsoft Docs
description: Individuazione del tipo di parametro con valori di tabella utilizzando OLE DB driver per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4e824e39a44985dc2f46a1a27c7b5b4e8d05a6dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015293"
---
# <a name="table-valued-parameter-type-discovery"></a>Individuazione del tipo di parametro con valori di tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il consumer, ovvero l'applicazione client che usa il driver OLE DB per SQL Server, può individuare il tipo di ogni parametro del comando se al provider OLE DB è stato indicato il testo del comando. Una volta noto il tipo di un parametro con valori di tabella, il consumer può individuare le informazioni sui metadati per ogni singola colonna del parametro con valori di tabella.  
  
 Le informazioni sul tipo dei parametri della procedura sono supportate da ICommandWithParameters:: GetParameterInfo per la maggior parte dei tipi di parametro. A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], con l'introduzione dei tipi definiti dall'utente e del tipo di dati **xml**, il metodo GetParameterInfo non era sufficiente per questo scopo poiché non era possibile specificare le informazioni sul tipo definito dall'utente (nome, schema e catalogo) tramite ICommandWithParameters. È stata definita una nuova interfaccia, ISSCommandWithParameters, per fornire informazioni sul tipo estese.  
  
 Per i parametri con valori di tabella, è inoltre possibile utilizzare l'interfaccia ISSCommandWithParameters per individuare informazioni dettagliate. Il client chiama ISSCommandWithParameters:: GetParameterInfo dopo aver preparato l'oggetto Command. Per i parametri con valori di tabella il membro *wType* della struttura DBPARAMINFO viene impostato su DBTYPE_TABLE dal provider. Il valore del campo *ulParamSize* della struttura DBPARAMINFO è ~0.  
  
 Il consumer può quindi richiedere proprietà aggiuntive (nome del catalogo del tipo di parametro con valori di tabella, nome dello schema del tipo di parametro con valori di tabella, nome del tipo di parametro con valori di tabella, ordinamento colonne e colonne predefinite) mediante ISSCommandWithParameters::GetParameterProperties.  
  
 Una volta noto il nome del tipo, per recuperare informazioni sulle singole colonne il consumer deve chiamare IOpenRowset::OpenRowset oppure ottenere il set di righe DBSCHEMA_TABLE_TYPE_COLUMNS specificando il nome del tipo di parametro con valori di tabella come nome della tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
