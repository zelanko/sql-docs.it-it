---
title: Recupero della versione del driver
description: Informazioni su come e dove trovare la versione di Microsoft JDBC Driver per SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f90f521457f5df17be814a179353d138a3245aea
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381195"
---
# <a name="getting-the-driver-version"></a>Recupero della versione del driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  È possibile individuare la versione installata di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] nei modi seguenti:  
  
-   Chiamando il metodo [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) o [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md) di [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md).  
  
-   La versione viene visualizzata nel file readme.txt della distribuzione del prodotto.  
  
 Il nome del driver JDBC può inoltre essere restituito dalla chiamata del metodo [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) nella classe SQLServerDatabaseMetaData. La chiamata restituirà, ad esempio, "Microsoft JDBC Driver 6.4 for SQL Server".  
  
 Di seguito è riportato un esempio dell'output delle chiamate ai metodi della classe SQLServerDatabaseMetaData:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Dove "xxx.x" è il numero della versione finale.  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
