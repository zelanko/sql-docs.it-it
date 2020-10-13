---
title: Eseguire aggiornamenti parziali di dati FILESTREAM | Microsoft Docs
description: Informazioni sull'uso del valore FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT per eseguire aggiornamenti parziali dei dati BLOB FILESTREAM. Visualizzare un esempio di aggiornamento parziale.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3b47cdacd079bfa1235427938b3fa214a1babeb7
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809901"
---
# <a name="make-partial-updates-to-filestream-data"></a>Esecuzione di aggiornamenti parziali di dati FILESTREAM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Un'applicazione utilizza FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT per eseguire aggiornamenti parziali dei dati BLOB FILESTREAM. La funzione [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) passa il valore e l'handle restituito da [OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) al driver FILESTREAM. Tramite il driver viene forzata una copia lato server dei dati FILESTREAM correnti nel file a cui fa riferimento l'handle. Se l'applicazione rilascia il valore FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT dopo la scrittura nell'handle, l'ultima operazione di scrittura viene resa persistente, mentre quelle precedenti eseguite nell'handle vanno perse.  
  
> [!NOTE]  
>  Per l'accesso remoto, FILESTREAM è basato sul [protocollo SMB](/windows/win32/fileio/microsoft-smb-protocol-and-cifs-protocol-overview) .  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il valore `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` per eseguire un aggiornamento parziale di dati BLOB FILESTREAM inseriti.  
  
> [!NOTE]  
>  Questo esempio richiede il database e la tabella abilitati per FILESTREAM creati in [Creare un database abilitato per FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md) e [Creare una tabella per archiviare dati FILESTREAM](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md).  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../relational-databases/blob/codesnippet/cpp/make-partial-updates-to-_1.cpp)]  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso ai dati FILESTREAM con OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Creazione di applicazioni client per dati FILESTREAM](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
  
