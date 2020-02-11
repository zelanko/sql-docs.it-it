---
title: Errori | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 434b4251c51809c97744e7aaf954ac1f11c06cfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63050676"
---
# <a name="errors"></a>Errors
  Gli oggetti OLE/COM segnalano gli errori tramite il codice restituito HRESULT delle funzioni membro oggetto. Un HRESULT OLE/COM è una struttura costituita da pacchetti di byte. OLE fornisce macro che risolvono i riferimenti dei membri di struttura.  
  
 OLE/COM specifica l'interfaccia **IErrorInfo**. L'interfaccia espone metodi come **GetDescription**. In questo modo, i client possono estrarre i dettagli relativi agli errori dai server OLE/COM. OLE DB estende **IErrorInfo** per supportare la restituzione di più pacchetti di informazioni sugli errori nell'esecuzione di una funzione con singolo membro.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire più errori. Un'applicazione può recuperare gli errori del server uno alla volta chiamando [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) insieme a ISQLErrorInfo e IErrorRecords.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client espone l'OLE DB **IErrorInfo**con miglioramento dei record `ISQLErrorInfo`, l'oggetto personalizzato e le interfacce dell'oggetto errore [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) specifiche del provider.  
  
 Per informazioni sulla traccia degli errori, vedere [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Traccia di accesso ai dati). Per informazioni sui miglioramenti alla traccia degli errori aggiunta in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], vedere [accesso alle informazioni di diagnostica nel log degli eventi estesi](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Codici restituiti](return-codes.md)  
  
-   [Informazioni nelle interfacce di errore](information-in-error-interfaces.md)  
  
-   [Dettagli relativi agli errori SQL Server](sql-server-error-detail.md)  
  
-   [Recupero delle informazioni sugli errori](retrieving-error-information.md)  
  
-   [Risultati dei messaggi di SQL Server](sql-server-message-results.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
