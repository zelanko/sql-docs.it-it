---
title: Metodo setClientInfo (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7673bf2aff3d5ea60966a8594d3b4ab13950f92d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974628"
---
# <a name="setclientinfo-method-javalangstring-javalangstring"></a>Metodo setClientInfo (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il valore della proprietà delle informazioni client specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setClientInfo (java.lang.String name,  
                           java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parametri  
 *name*  
  
 Valore String contenente il nome della proprietà delle informazioni client da impostare.  
  
 *Valore*  
  
 Valore String contenente il valore su cui impostare la proprietà delle informazioni client.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setClientInfo viene specificato dal Metodo setClientInfo nell'interfaccia java. SQL. Connection.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] non supporta alcuna proprietà delle informazioni client. In Microsoft JDBC Driver 2.0 questo metodo genera un avviso per una proprietà. Per le applicazioni è previsto l'uso del metodo [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) della classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) per il recupero di un avviso.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
