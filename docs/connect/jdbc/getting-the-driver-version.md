---
title: Recupero della versione del Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2cfe90d0a38cf5e599d82a6208a145daa3a3d1c7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781815"
---
# <a name="getting-the-driver-version"></a>Recupero della versione del driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  È possibile individuare la versione installata di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] nei modi seguenti:  
  
-   Chiamando il metodo [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) o [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md) di [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md).  
  
-   La versione viene visualizzata nel file readme.txt della distribuzione del prodotto.  
  
 Il nome del driver JDBC può inoltre essere restituito dalla chiamata del metodo [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) nella classe SQLServerDatabaseMetaData. La chiamata restituirà, ad esempio, "Microsoft JDBC Driver 6.4 for SQL Server".  
  
 Di seguito è riportato un esempio dell'output dalle chiamate ai metodi della classe SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Dove "xxx.x" è il numero della versione finale.  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
