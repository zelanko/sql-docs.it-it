---
description: Classe SQLServerResultSet
title: Classe SQLServerResultSet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f39b678960c18d0b9f4956ed05523ddcb0da965d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467073"
---
# <a name="sqlserverresultset-class"></a>Classe SQLServerResultSet
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta un set di risultati JDBC.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>Osservazioni  
 Esistono due tipi di set di risultati: lato client e lato server.  
  
 I set di risultati del lato client vengono utilizzati quando le dimensioni dei risultati sono tali da consentirne la conservazione nella memoria del processo client. Questi risultati sono disponibili più rapidamente e vengono letti interamente dal database da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Inoltre non impongono carico aggiuntivo sul database, evitando l'overhead correlato alla creazione di cursori sul lato server. Tuttavia, questi tipi di set di risultati non sono aggiornabili.  
  
 I set di risultati del lato server possono essere utilizzati quando le dimensioni dei risultati sono tali da non consentirne la conservazione nella memoria del processo client o quando il set di risultati deve essere aggiornabile. Con questo tipo di set di risultati, il driver JDBC crea un cursore sul lato server e recupera in modo trasparente le righe del set di risultati man mano che l'utente scorre il set stesso.  
  
 La classe SQLServerResultSet fornisce numerosi metodi che consentono l'aggiornamento del set di risultati con qualsiasi tipo di dati Java nativo e numerosi tipi di oggetti Java.  
  
 Questa classe supporta l'annullamento del wrapping per la classe SQLServerResultSet, l'interfaccia ISQLServerResultSet e l'interfaccia java.sql.ResultSet. Per altre informazioni, vedere [Wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
