---
title: Errori | Microsoft Docs
description: Errori
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9bf1985706cefc3007da56a9bf782a070e3b8edf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994962"
---
# <a name="errors"></a>Errori
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Gli oggetti OLE/COM segnalano gli errori tramite il codice restituito HRESULT delle funzioni membro oggetto. Un HRESULT OLE/COM è una struttura costituita da pacchetti di byte. OLE fornisce macro che risolvono i riferimenti dei membri di struttura.  
  
 OLE/COM specifica l'interfaccia **IErrorInfo**. L'interfaccia espone metodi come **GetDescription**. In questo modo, i client possono estrarre i dettagli relativi agli errori dai server OLE/COM. OLE DB estende **IErrorInfo** per supportare la restituzione di più pacchetti di informazioni sugli errori nell'esecuzione di una funzione con singolo membro.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può restituire più errori. Un'applicazione può recuperare gli errori del server uno alla volta chiamando [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) insieme a ISQLErrorInfo e IErrorRecords.  
  
 Il driver OLE DB per SQL Server espone le interfacce per oggetti errore seguenti: l'interfaccia OLE DB **IErrorInfo** ottimizzata per i record, l'interfaccia **IErrorRecords** personalizzata e l'interfaccia [ISQLErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) specifica del provider.  
  
 Per informazioni sulla traccia degli errori, vedere [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Traccia di accesso ai dati). Per informazioni sui miglioramenti alla traccia degli errori aggiunta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], vedere [accesso alle informazioni di diagnostica nel log degli eventi estesi](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Codici restituiti](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Informazioni nelle interfacce di errore](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Dettagli relativi agli errori di SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Recupero delle informazioni sugli errori](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Risultati dei messaggi di SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per programmazione con SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
