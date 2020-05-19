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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e3979390a58235dbb8ec7c76e7b16478e7d9deb9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704999"
---
# <a name="errors"></a>Errors
  Gli oggetti OLE/COM segnalano gli errori tramite il codice restituito HRESULT delle funzioni membro oggetto. Un HRESULT OLE/COM è una struttura costituita da pacchetti di byte. OLE fornisce macro che risolvono i riferimenti dei membri di struttura.  
  
 OLE/COM specifica l'interfaccia **IErrorInfo**. L'interfaccia espone metodi come **GetDescription**. In questo modo, i client possono estrarre i dettagli relativi agli errori dai server OLE/COM. OLE DB estende **IErrorInfo** per supportare la restituzione di più pacchetti di informazioni sugli errori nell'esecuzione di una funzione con singolo membro.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può restituire più errori. Un'applicazione può recuperare gli errori del server uno alla volta chiamando [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) insieme a ISQLErrorInfo e IErrorRecords.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client espone l'OLE DB **IErrorInfo**con miglioramento dei record, l' `ISQLErrorInfo` oggetto personalizzato e le interfacce dell'oggetto errore [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) specifiche del provider.  
  
 Per informazioni sulla traccia degli errori, vedere [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Traccia di accesso ai dati). Per informazioni sui miglioramenti apportati alla traccia degli errori aggiunta in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], vedere [Accesso alle informazioni di diagnostica nel log degli eventi estesi](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Codici restituiti](return-codes.md)  
  
-   [Informazioni nelle interfacce di errore](information-in-error-interfaces.md)  
  
-   [Dettagli relativi agli errori di SQL Server](sql-server-error-detail.md)  
  
-   [Recupero delle informazioni sugli errori](retrieving-error-information.md)  
  
-   [Risultati dei messaggi di SQL Server](sql-server-message-results.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
