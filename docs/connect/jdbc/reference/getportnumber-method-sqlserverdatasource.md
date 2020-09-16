---
description: Metodo getPortNumber (SQLServerDataSource)
title: Metodo getPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ded903bb6696c3dfefd51979d37605af899b6d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435013"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Metodo getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il numero della porta corrente usata per comunicare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** contenente il numero di porta corrente.  
  
## <a name="remarks"></a>Osservazioni  
 Il numero di porta è il numero di porta TCP/IP usato quando si apre una connessione socket a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se la proprietà portNumber non è impostata, il metodo getPortNumber restituisce il valore predefinito 1433.  
  
> [!NOTE]  
>  Il metodo [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) non esegue alcun controllo dell'intervallo sul valore di porta passato. È possibile passare numeri di porta non validi, ad esempio 99999, senza generare un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
