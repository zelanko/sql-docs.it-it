---
title: 'Matrice di compatibilità : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0406599e1657a900d1669861572ff13834cec670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307454"
---
# <a name="compatibility-matrix"></a>Matrice di compatibilità
Nella tabella seguente viene descritta la compatibilità dei tipi di applicazioni e driver definiti in precedenza in questa sezione.  
  
|Tipo di applicazione<br /><br /> e la versione|ODBC a 32 bit<br /><br /> *Driver 2.x*|ODBC *3.x*<br /><br /> driver|Driver ODBC 3.8|Driver conforme allo standard ISO e Open Group|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|Applicazione a 16 bit, qualsiasi versione|Compatibile|Compatibile|Compatibile|Compatibile|  
|Applicazione Pure *2.x*|Compatibile|Compatibile|Compatibile|Non compatibile[3]|  
|Applicazione ricompilata Pure *2.x*|Compatibile|Compatibile[1]|Compatibile[1]|Non compatibile[3]|  
|Applicazione Unicode Pure *2.x*|Compatibile|Compatibile[1]|Compatibile[1]|Non compatibile[3]|  
|Pure Open Group e applicazione conforme allo standard ISO|Non compatibile|Compatibile[2]|Compatibile[2]|Compatibile[2]|  
|Applicazione Pure 3.0|Non compatibile|Compatibile|Compatibile|Non compatibile[4]|  
|Applicazione Pure 3.5|Non compatibile|Compatibile|Compatibile|Non compatibile[4]|  
|Applicazione pura 3.8 (o superiore)|Non compatibile [5]|Non compatibile [5]|Compatibile|Non compatibile [4]|  
|Applicazione sostituita|Compatibile|Compatibile|Compatibile|Non compatibile[3]|  
  
 [1] L'applicazione deve ricompilare utilizzando intestazioni ODBC 3.5 (o successive) con l'opzione UNICODE (se si tratta di un'applicazione Unicode) e deve impostare ODBCVER su 0x0250.  
  
 [2] L'applicazione deve essere compilata utilizzando le intestazioni ODBC 3.5 (o superiore) e deve essere collegata a Gestione driver ODBC. È inoltre necessario impostare il flag di intestazione ODBC_STD.  
  
 [3] Questa configurazione potrebbe non funzionare perché ci sono funzionalità in ODBC *2.x* che non sono negli standard, come i segnalibri.  
  
 [4] Questa configurazione potrebbe non funzionare perché ci sono funzionalità in ODBC *3.x* che non sono negli standard, come i segnalibri.  
  
 [5] Questa configurazione può potenzialmente non riuscire perché sono presenti funzionalità in ODBC 3.8 che non sono presenti in driver ODBC 2.x o 3.x, ad esempio tipi di dati C specifici del driver [in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilità di Driver Manager  
 Un'applicazione ODBC 3.0 che deve funzionare con tutte le versioni di Gestione Driver deve eseguire le operazioni seguenti all'avvio:  
  
-   Allocare un handle di ambiente.  
  
-   Impostare l'attributo dell'ambiente di SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3_80. Se Gestione Driver restituisce SQL_ERROR, Gestione Driver è precedente a 3.8. Reimpostare SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3 o SQL_OV_ODBC2, a seconda dei casi, in modo che corrisponda a Gestione Driver.  
  
-   Allocare un handle di connessione.  
  
-   Stabilite una connessione.  
  
-   Chiamare SQLGetInfo per SQL_DRIVER_ODBC_VER per determinare la versione del driver. Se il driver è un driver ODBC 3.8, è possibile utilizzare tipi C specifici del driver. In caso contrario, non utilizzare tipi di dati C specifici del driver.  
  
 Si noti che un'applicazione ODBC 3.x ricompilata può utilizzare funzionalità ODBC 3.8 diverse dai tipi C specifici del driver senza specificare SQL_OV_ODBC3_80 per SQL_ATTR_ODBC_VERSION. È simile a un'applicazione ODBC 2.x ricompilata che utilizza le funzionalità di ODBC 3.x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Utilizzo di SQLCancelHandle in un'applicazione compatibile con tutti i gestori di driverUsing SQLCancelHandle in an Application Compatible with all Driver Managers  
 Poiché la [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) non è supportata in Gestione driver rilasciati prima di Windows 7, un'applicazione non può essere caricata nelle versioni precedenti di Windows se chiama direttamente **SQLCancelHandle.** Per utilizzare tutte le versioni di Gestione driver e utilizzare **SQLCancelHandle** nelle nuove versioni di Windows, un'applicazione deve chiamare **SQLCancelHandle** indirettamente utilizzando **LoadLibrary** e **GetProcAddress.**  
  
## <a name="see-also"></a>Vedere anche  
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
