---
title: Metodo getEncrypt (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ae50bcd5499ffa3bd5c10ef492d78de4685402e8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767214"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>Metodo getEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **Boolean** che indica se la proprietà di crittografia è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la crittografia è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se la proprietà di crittografia è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fa in modo che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] venga usata la crittografia SSL per tutti i dati inviati tra il client e il server, se nel server è installato un certificato.  
  
 Se la proprietà encrypt non è specificata o è impostata su **false**, il driver non impone a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il supporto della crittografia SSL. Se l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non è configurata in modo da forzare la crittografia SSL, viene stabilita una connessione senza crittografia. Se l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è configurata in modo da forzare la crittografia SSL, quest'ultima viene abilitata automaticamente da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] durante l'esecuzione in un ambiente JVM correttamente configurato. In caso contrario, la connessione viene terminata e il driver genera un errore. Se la proprietà di crittografia non è impostata, il metodo [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) restituisce il valore predefinito **false**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
