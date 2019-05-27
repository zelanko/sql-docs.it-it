---
title: Eseguire aggiornamenti parziali di dati FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96d9cb3d5c5317ecc9dd069f2e99b20c30327a3d
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66009891"
---
# <a name="make-partial-updates-to-filestream-data"></a>Esecuzione di aggiornamenti parziali di dati FILESTREAM
  Un'applicazione utilizza FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT per eseguire aggiornamenti parziali dei dati BLOB FILESTREAM. La funzione [DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527) passa il valore e l'handle restituito da [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) al driver FILESTREAM. Tramite il driver viene forzata una copia lato server dei dati FILESTREAM correnti nel file a cui fa riferimento l'handle. Se l'applicazione rilascia il valore FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT dopo la scrittura nell'handle, l'ultima operazione di scrittura viene resa persistente, mentre quelle precedenti eseguite nell'handle vanno perse.  
  
> [!NOTE]  
>  Per l'accesso remoto, FILESTREAM è basato sul [protocollo SMB](https://go.microsoft.com/fwlink/?LinkId=112454) .  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il valore `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` per eseguire un aggiornamento parziale di dati BLOB FILESTREAM inseriti.  
  
> [!NOTE]  
>  Questo esempio richiede il database e la tabella abilitati per FILESTREAM creati in [Creare un database abilitato per FILESTREAM](create-a-filestream-enabled-database.md) e [Creare una tabella per archiviare dati FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso ai dati FILESTREAM con OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)   
 [Creazione di applicazioni client per dati FILESTREAM](create-client-applications-for-filestream-data.md)  
  
  
