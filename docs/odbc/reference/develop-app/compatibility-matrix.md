---
title: Matrice di compatibilità | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d0fc510c7c45dab8fbc79cc8e74001ff1855b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026571"
---
# <a name="compatibility-matrix"></a>Matrice di compatibilità
Nella tabella seguente viene descritta la compatibilità dei tipi di applicazioni e driver definiti precedentemente in questa sezione.  
  
|Tipo di applicazione<br /><br /> e versione|ODBC 32-bit<br /><br /> 2.*x* driver|ODBC 3.*x*<br /><br /> Driver|Driver ODBC 3.8|ISO e aprire compatibile con gruppo di driver|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|applicazione a 16 bit, qualsiasi versione|Compatibilità|Compatibilità|Compatibilità|Compatibilità|  
|2 pure. *x* applicazione|Compatibilità|Compatibilità|Compatibilità|Non compatibile con [3]|  
|2 pure. *x* ricompilate dell'applicazione|Compatibilità|Compatibile con [1]|Compatibile con [1]|Non compatibile con [3]|  
|2 pure. *x* Unicode application|Compatibilità|Compatibile con [1]|Compatibile con [1]|Non compatibile con [3]|  
|Applicazione di gruppo aprire puro e conforme allo standard ISO|Non è compatibile|Compatibile con [2]|Compatibile con [2]|Compatibile con [2]|  
|Applicazione 3.0 pure|Non è compatibile|Compatibilità|Compatibilità|Non compatibile con [4]|  
|Applicazione 3.5 pure|Non è compatibile|Compatibilità|Compatibilità|Non compatibile con [4]|  
|Applicazione puramente 3,8 (o versioni successive)|Non compatibile con [5]|Non compatibile con [5]|Compatibilità|Non compatibile con [4]|  
|Applicazione sostituito|Compatibilità|Compatibilità|Compatibilità|Non compatibile con [3]|  
  
 [1] l'applicazione è necessario ricompilare utilizzando le intestazioni ODBC 3.5 (o versione successive) con l'opzione di UNICODE (se si tratta di un'applicazione Unicode) e devono impostare ODBCVER su 0x0250.  
  
 [2] l'applicazione deve compilare con le intestazioni ODBC 3.5 (o versione successive) e collegare con gestione Driver ODBC. Inoltre necessario impostare il flag di intestazione ODBC_STD.  
  
 [3] questa configurazione possa potenzialmente non funzionerà perché sono presenti funzioni di ODBC 2. *x* che non sono presenti gli standard, ad esempio i segnalibri.  
  
 [4] questa configurazione possa potenzialmente non funzionano perché sono presenti funzionalità in ODBC 3*x* che non sono presenti gli standard, ad esempio i segnalibri.  
  
 [5] questa configurazione può non riuscire perché sono presenti funzionalità che non si trovano in ODBC 2.x o 3.x driver, ad esempio specifici del driver ODBC 3.8 [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilità di Gestione driver  
 Un'applicazione ODBC 3.0 che deve funzionare con tutte le versioni di gestione Driver deve eseguire le operazioni seguenti all'avvio:  
  
-   Allocare un handle di ambiente.  
  
-   Impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80. Se Gestione Driver restituisce SQL_ERROR, gestione Driver è anteriore a 3.8. Reimpostare SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 o SQL_OV_ODBC2, come appropriato, in modo che corrisponda al Driver Manager.  
  
-   Allocare un handle di connessione.  
  
-   Stabilire una connessione.  
  
-   Chiamare SQLGetInfo per SQL_DRIVER_ODBC_VER determinare la versione del driver. Se il driver è un driver ODBC 3.8, è possibile utilizzare i tipi C specifici del driver. In caso contrario, non usare tipi di dati C specifici del driver.  
  
 Si noti che un'applicazione di 3.x ODBC ricompilata può usare le funzionalità di ODBC 3.8 diverso dai tipi C specifiche del driver senza specificare SQL_OV_ODBC3_80 per SQL_ATTR_ODBC_VERSION. Ciò è simile a un'applicazione ODBC 2.x ricompilata usando funzioni ODBC 3.x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Uso di SQLCancelHandle in un'applicazione compatibile con tutti i gestori del Driver  
 In quanto [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) non è supportato nelle Gestioni di Driver che sono state rilasciate prima di Windows 7, non è possibile caricare un'applicazione nelle versioni precedenti di Windows se chiama **SQLCancelHandle** direttamente. Per funzionare con tutte le versioni dei Driver Manager e usare **SQLCancelHandle** sulle nuove versioni di Windows, un'applicazione deve chiamare **SQLCancelHandle** indirettamente tramite **LoadLibrary** e **GetProcAddress.**  
  
## <a name="see-also"></a>Vedere anche  
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
