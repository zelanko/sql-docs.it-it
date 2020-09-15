---
description: Metodo setFetchDirection (SQLServerStatement)
title: Metodo setFetchDirection (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9469fe9b0e559358e3e18c15719161b0ae0033
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431873"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>Metodo setFetchDirection (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornisce a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] un hint per la direzione da usare per l'elaborazione delle righe del set di risultati.  
  
> [!NOTE]  
>  Attualmente, il driver JDBC ignora l'hint fornito da questo metodo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>Parametri  
 *nDir*  
  
 Valore **int** che indica la direzione di elaborazione delle righe. Può essere uno dei valori seguenti:  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setFetchDirection viene specificato dal metodo setFetchDirection nell'interfaccia java.sql.Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
