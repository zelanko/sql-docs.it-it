---
title: Metodo setEncrypt (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8bb95e1eb547037d7ecf1855f71fa519102cf621
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773485"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>Metodo setEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta un valore **Boolean** che indica se la proprietà encrypt è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>Parametri  
 *encrypt*  
  
 **true** se è abilitata la crittografia Secure Sockets Layer (SSL) tra il client e il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. In caso contrario, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se la proprietà encrypt è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fa in modo che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] venga usata la crittografia SSL per tutti i dati inviati tra il client e il server, se nel server è installato un certificato. Il valore predefinito è **false**.  
  
 Il driver JDBC rileva l'ambiente Java Virtual Machine (JVM) in cui viene eseguito durante il tentativo di stabilire un handshake SSL.  
  
 Se la proprietà encrypt è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usa il provider di sicurezza JSSE predefinito di JVM per negoziare la crittografia SSL con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È possibile che il provider di sicurezza predefinito non supporti tutte le funzionalità necessarie per negoziare la crittografia SSL. Tale provider può, ad esempio, non supportare la dimensione della chiave pubblica RSA usata nel certificato SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. In questo caso, è possibile che venga generato un errore dal provider di sicurezza predefinito, a causa del quale la connessione viene terminata dal driver JDBC. Per risolvere il problema, eseguire una delle operazioni seguenti:  
  
-   Configurare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con un certificato del server con una chiave pubblica RSA di dimensione inferiore  
  
-   Configurare JVM per l'uso di un provider di sicurezza JSSE diverso nel file delle proprietà di sicurezza "\<java-home>/lib/security/java.security"  
  
-   Utilizzare una versione di JVM diversa.  
  
 Se la proprietà encrypt non è specificata o è impostata su **false**, il driver non impone a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il supporto della crittografia SSL. Se l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non è configurata in modo da forzare la crittografia SSL, viene stabilita una connessione senza crittografia. Se l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è configurata in modo da forzare la crittografia SSL, questa viene abilitata automaticamente da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] durante l'esecuzione in un ambiente JVM correttamente configurato. In caso contrario, la connessione viene terminata e il driver genera un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
