---
title: Metodo getSendStringParametersAsUnicode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df27a5368dfea7f417fb84e2ebe38a8987165aec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979976"
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>Metodo getSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **booleano** che indica se è abilitato l'invio di parametri di stringa al server in formato UNICODE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se i parametri di stringa vengono inviati al server in formato UNICODE. In caso contrario, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se la proprietà sendStringParametersAsUnicode è impostata su **true**, che è il valore predefinito, i parametri di stringa vengono inviati al server in formato UNICODE. Se la proprietà sendStringParametersAsUnicode è impostata su **false**, i parametri di stringa vengono inviati al server in formato ASCII/MBCS e non UNICODE. Se la proprietà sendStringParametersAsUnicode non è impostata, getSendStringParametersAsUnicode restituisce il valore predefinito **true**.  
  
 Per ulteriori informazioni sulla proprietà di connessione sendStringParametersAsUnicode, vedere [impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
