---
title: I membri di SQLServerParameterMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f3f0c6558416c3a5736d7e5ce9663c5f9a7190a0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773519"
---
# <a name="sqlserverparametermetadata-members"></a>Membri di SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Nelle tabelle seguenti sono elencati i membri esposti dalla classe [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md).  
  
## <a name="constructors"></a>Costruttori  
 Nessuna.  
  
## <a name="fields"></a>Campi  
 Nessuna.  
  
## <a name="inherited-fields"></a>Campi ereditati  
  
|nome|Descrizione|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn, parameterModeInOut, parameterModeOut, parameterModeUnknown, parameterNoNulls, parameterNullable, parameterNullableUnknown|  
  
## <a name="methods"></a>Metodi  
  
|nome|Descrizione|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|Recupera il nome completo della classe Java le cui istanze devono essere passate al metodo [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) della classe [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|Recupera il numero di parametri nell'oggetto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) per cui questo oggetto [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) contiene informazioni.|  
|[getParameterMode](../../../connect/jdbc/reference/getparametermode-method-sqlserverparametermetadata.md)|Recupera la modalità del parametro designato.|  
|[getParameterType](../../../connect/jdbc/reference/getparametertype-method-sqlserverparametermetadata.md)|Recupera il tipo SQL del parametro designato.|  
|[getParameterTypeName](../../../connect/jdbc/reference/getparametertypename-method-sqlserverparametermetadata.md)|Recupera il nome del tipo specifico del database del parametro designato.|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverparametermetadata.md)|Recupera il numero di cifre decimali per il parametro designato.|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverparametermetadata.md)|Recupera il numero di cifre a destra del separatore decimale per il parametro designato.|  
|[isNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverparametermetadata.md)|Recupera un valore che indica se nel parametro designato sono consentiti valori Null.|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverparametermetadata.md)|Recupera un valore che indica se i valori per il parametro designato possono essere numeri con segno.|  
  
## <a name="inherited-methods"></a>Metodi ereditati  
  
|Classe ereditata da:|Metodi|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
