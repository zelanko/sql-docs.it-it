---
description: Metodo setTrustStore (SQLServerDataSource)
title: Metodo setTrustStore (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be69bd333d0264e4833dd053979f1e3dfe5a9b39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354927"
---
# <a name="settruststore-method-sqlserverdatasource"></a>Metodo setTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il percorso (incluso il nome file) del file trustStore del certificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>Parametri  
 *trustStore*  
  
 Una **stringa** contenente il percorso, nome file incluso, del file trustStore del certificato.  
  
## <a name="remarks"></a>Osservazioni  
 Quando la proprietà trustStore non è specificata o è impostata su Null, per determinare l'archivio certificati da utilizzare in [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] vengono utilizzate le regole di ricerca della factory del responsabile dell'attendibilità. Tramite l'istanza predefinita di TrustManagerFactory SunX509 viene eseguito un tentativo di individuare il materiale attendibile nelle posizioni seguenti in base all'ordine indicato:  
  
-   1. Un file specificato dalla proprietà di sistema JVM (Java Virtual Machine) "javax.net.ssl.trustStore".  
  
-   2. File "\<java-home>/lib/security/jssecacerts".  
  
-   3. File "\<java-home>/lib/security/cacerts".  
  
 Per ulteriori informazioni, vedere la documentazione relativa all'interfaccia TrustManager SunX509 nel sito Web Sun Microsystems.  
  
 Se la proprietà trustStore è impostata su una stringa o una stringa vuota "", tale valore verrà usato dal driver per trovare il file trustStore e convalidare il certificato TLS/SSL del server.  
  
 È possibile specificare la proprietà trustStorePassword insieme alla proprietà trustStore in modo da utilizzarne il valore per aprire il file trustStore. Per ulteriori informazioni, vedere [setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
