---
title: Classe SQLServerParameterMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1393d7c6a5665730517d8aa1f248eaadb0db65aa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773562"
---
# <a name="sqlserverparametermetadata-class"></a>Classe SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta i metadati per i parametri delle istruzioni preparate.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 **Implementa:** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>Remarks  
 Per recuperare i metadati del parametro, le istruzioni preparate vengono eseguite con SET FMT ONLY. Le istruzioni disponibili per la chiamata chiamano sp_sproc_columns per recuperare nomi e metadati per i parametri della procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
