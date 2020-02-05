---
title: setDateTimeOffset(int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 166c9ddbd4b5c11b3c032a5a4ecf43c95f183473
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974535"
---
# <a name="setdatetimeoffsetint-javasqldatetimeoffset-sqlserverstatement"></a>setDateTimeOffset(int, java.sql.DateTimeOffset) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore DateTimeOffset specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setDateTimeOffset(int parameterIndex, DateTimeOffset dateTime)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterIndex*  
  
 Indice della colonna da impostare.  
  
 *dateTimeOffset*  
  
 Oggetto DateTimeOffset.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il formato di DateTimeOffset è "AAAA-MM-GG HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Utilizzare la tabella seguente come riferimento.  
  
|Tipo SQL|Inserimento|  
|--------------|------------|  
|Datetime|Unico inserimento possibile: "AAAA-MM-GG hh:mm:ss[.nnn]"|  
|smalldatetime|Unico inserimento possibile: "AAAA-MM-GG hh:mm:ss"|  
|Tempo|Unico inserimento possibile: "hh:mm:ss[.nnnnnnn]"|  
|Data|Unico inserimento possibile: "AAAA-MM-GG"|  
|DateTime2|Unico inserimento possibile: "AAAA-MM-GG hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Vedere anche  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
