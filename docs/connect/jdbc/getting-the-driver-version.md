---
title: Recupero della versione del driver | Microsoft Docs
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
ms.openlocfilehash: 1a1c5c6d4dcc3a5bd5acaac37ffdcdadc184e497
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924652"
---
# <a name="getting-the-driver-version"></a>Recupero della versione del driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  È possibile individuare la versione installata di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] nei modi seguenti:  
  
-   Chiamando il metodo [getDriverMajorVersion](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md) o [getDriverVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) di [SQLServerDatabaseMetaData](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
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
  
  
