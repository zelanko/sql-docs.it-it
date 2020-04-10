---
title: setAuthenticationScheme (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b942f78e-7ce1-44ef-923d-a7c3d7c76b83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08d9483a97be92acf7b08104e2f285fb954673ed
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924474"
---
# <a name="setauthenticationscheme-sqlserverdatasource"></a>setAuthenticationScheme (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica il tipo di sicurezza integrata che si desidera venga utilizzata dall'applicazione.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
public void setAuthenticationScheme(String authenticationScheme);  
```  
  
#### <a name="parameters"></a>Parametri  
 *authenticationScheme*  
  
 I valori sono **"JavaKerberos"** e il valore predefinito **"NativeAuthentication"** . Per altre informazioni, vedere [Uso dell'autenticazione integrata Kerberos per la connessione a SQL Server](../../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
