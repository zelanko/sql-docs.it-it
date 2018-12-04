---
title: Individuazione del tipo di parametro con valori di tabella | Microsoft Docs
description: Con valori di tabella di rilevamento tipo parametro usando il Driver OLE DB per SQL Server
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
manager: craigg
ms.openlocfilehash: aab78327d575858675ade3bbc5d652cce5db12a5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506253"
---
# <a name="table-valued-parameter-type-discovery"></a>Individuazione del tipo di parametro con valori di tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il consumer, ovvero l'applicazione client che usa il driver OLE DB per SQL Server, può individuare il tipo di ogni parametro del comando se al provider OLE DB è stato indicato il testo del comando. Una volta noto il tipo di un parametro con valori di tabella, il consumer può individuare le informazioni sui metadati per ogni singola colonna del parametro con valori di tabella.  
  
 Le informazioni sul tipo di parametri di routine è supportati da ICommandWithParameters:: GetParameterInfo per la maggior parte dei tipi di parametro. A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], con l'introduzione dei tipi definiti dall'utente e del tipo di dati **xml**, il metodo GetParameterInfo non era sufficiente per questo scopo poiché non era possibile specificare le informazioni sul tipo definito dall'utente (nome, schema e catalogo) tramite ICommandWithParameters. È stata definita una nuova interfaccia ISSCommandWithParameters, per fornire informazioni estese sul tipo.  
  
 Per i parametri con valori di tabella, utilizziamo inoltre l'interfaccia ISSCommandWithParameters per individuare informazioni dettagliate. Il client chiama ISSCommandWithParameters::GetParameterInfo dopo aver preparato l'oggetto comando. Per i parametri con valori di tabella il membro *wType* della struttura DBPARAMINFO viene impostato su DBTYPE_TABLE dal provider. Il valore del campo *ulParamSize* della struttura DBPARAMINFO è ~0.  
  
 Il consumer può quindi richiedere proprietà aggiuntive (nome del catalogo del tipo di parametro con valori di tabella, nome dello schema del tipo di parametro con valori di tabella, nome del tipo di parametro con valori di tabella, ordinamento colonne e colonne predefinite) mediante ISSCommandWithParameters::GetParameterProperties.  
  
 Una volta noto il nome del tipo, per recuperare informazioni sulle singole colonne il consumer deve chiamare IOpenRowset::OpenRowset oppure ottenere il set di righe DBSCHEMA_TABLE_TYPE_COLUMNS specificando il nome del tipo di parametro con valori di tabella come nome della tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
