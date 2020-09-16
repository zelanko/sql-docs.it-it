---
description: Supporto per set di caratteri nazionali
title: Supporto per set di caratteri nazionali | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 394d81f28921bfc4e68204778ed6fcdf1e2fb9e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438343"
---
# <a name="national-character-set-support"></a>Supporto per set di caratteri nazionali
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Il driver JDBC supporta l'API di JDBC 4.0, che include nuovi metodi API per la conversione dei set di caratteri nazionali. Questo supporto include nuovi metodi setter, getter e updater per i tipi JDBC **NCHAR**, **NVARCHAR**, **LONGNVARCHAR** e **NCLOB**.  
  
 Di seguito sono elencati i nuovi metodi di richiamo, impostazione e aggiornamento per supportare la conversione dei set di caratteri nazionali:  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md).  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md).  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md).  
  
> [!NOTE]  
>  Per utilizzare questi metodi nell'applicazione, è necessario impostare il classpath per includere il file sqljdbc4.jar.  
  
 Per inviare parametri String al server in formato Unicode, le applicazioni devono usare i nuovi metodi per caratteri nazionali di JDBC 4.0 oppure impostare la proprietà di connessione **sendStringParametersAsUnicode** su "**true**" quando vengono usati metodi per caratteri non nazionali. Laddove possibile, è consigliabile utilizzare i nuovi metodi per caratteri nazionali di JDBC 4.0. Per altre informazioni sulla proprietà di connessione **sendStringParametersAsUnicode**, vedere [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
