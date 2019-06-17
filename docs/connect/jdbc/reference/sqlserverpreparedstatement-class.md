---
title: Classe SQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7112a20f7811a0796396045c50b1b243ed0c3802
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796945"
---
# <a name="sqlserverpreparedstatement-class"></a>Classe SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta l'implementazione di base della funzionalità dell'istruzione preparata di JDBC.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** SQLServerStatement  
  
 **Implementa**: [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerPreparedStatement offre metodi che consentono di specificare i parametri, ad esempio qualsiasi tipo nativo di Java e molti tipi di oggetti Java. SQLServerPreparedStatement prepara un'istruzione tramite la stored procedure **sp_prepare** di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e riutilizza l'handle di istruzione restituito per ogni esecuzione successiva dell'istruzione, in genere usando i diversi parametri specificati dall'utente.  
  
 SQLServerPreparedStatement supporta l'esecuzione in batch in cui un set di istruzioni preparate viene eseguito in un solo round trip del database per migliorare le prestazioni di esecuzione.  
  
 Questa classe supporta l'annullamento del wrapping nella classe SQLServerPreparedStatement, interfaccia ISQLServerPreparedStatement, interfaccia PreparedStatement e le classi e le interfacce supportate da SQLServerStatement per annullamento del wrapping. Per altre informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
