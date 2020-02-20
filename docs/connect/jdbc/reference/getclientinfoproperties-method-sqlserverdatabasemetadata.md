---
title: Metodo getClientInfoProperties (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08b919ec6b626cd61b757b380d24efffcada0d55
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953108"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>Metodo getClientInfoProperties (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un elenco di proprietà delle informazioni client supportate dal driver.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto ResultSet.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getClientInfoProperties viene specificato dal metodo getClientInfoProperties nell'interfaccia java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  Questo metodo restituisce un set di risultati vuoto. Il driver supporta solo l'impostazione di **applicationName** e imposta **applicationName** solo in fase di connessione. SQL Server non supporta l'aggiornamento delle informazioni sull'applicazione client una volta stabilita la connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
