---
title: Metodo setPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52f5093d4f9ba61bda2b3fb44cf6a64e76b6fe4e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920782"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>Metodo setPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta le dimensioni, specificate in byte, del pacchetto di rete corrente usato per comunicare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parametri  
 *packetSize*  
  
 Valore **int** contenente la dimensione del pacchetto di rete.  
  
## <a name="remarks"></a>Osservazioni  
 L'intervallo di valori accettabili di questa proprietà è [-1 | 0 | 512..32767]. Se questa proprietà è impostata su un valore che non rientra nell'intervallo valido, viene generata un'eccezione.  
  
 È possibile impostare la proprietà packetSize durante la connessione alla crittografia SSL (Secure Sockets Layer). Le dimensioni del pacchetto vengono negoziate con il server da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se la proprietà di crittografia è impostata su "**true**" e le dimensioni del pacchetto negoziate sono superiori alle dimensioni dei record SSL del provider di sicurezza predefinito di JVM (Java Virtual Machine), verrà generato un errore e la connessione verrà terminata.  
  
 È inoltre possibile impostare la proprietà packetSize senza richiedere la crittografia SSL. In questo caso, se il server richiede il supporto della crittografia SSL da parte del client, il driver verificherà le dimensioni dei record SSL del provider di sicurezza predefinito di JVM. Se le dimensioni della proprietà packetSize sono superiori rispetto alle dimensioni dei record SSL del provider di sicurezza predefinito di JVM, il driver genererà un errore e terminerà la connessione.  
  
 Per altre informazioni sull'uso di SSL, vedere [Uso della crittografia SSL](../../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
