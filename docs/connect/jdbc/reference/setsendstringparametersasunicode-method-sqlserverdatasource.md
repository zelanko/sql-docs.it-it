---
title: Metodo setSendStringParametersAsUnicode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe32325caccebd0e85204bbbc11b7a0cbe4eefca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972989"
---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>Metodo setSendStringParametersAsUnicode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta un valore **booleano** che indica se è abilitato l'invio di parametri di stringa al server in formato UNICODE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sendStringParametersAsUnicode*  
  
 **true** se i parametri di stringa vengono inviati al server in formato UNICODE. In caso contrario, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se la proprietà sendStringParametersAsUnicode è impostata su **true**, che è il valore predefinito, i parametri di stringa vengono inviati al server in formato UNICODE. Se la proprietà sendStringParametersAsUnicode è impostata su **false**, i parametri di stringa vengono inviati al server in formato ASCII/MBCS e non UNICODE. Se la proprietà sendStringParametersAsUnicode non è impostata, [getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) restituisce il valore predefinito **true**.  
  
 Per ulteriori informazioni sulla proprietà di connessione sendStringParametersAsUnicode, vedere [impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
