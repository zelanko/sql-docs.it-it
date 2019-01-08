---
title: I messaggi di errore - Parallel Data Warehouse | Microsoft Docs
description: I messaggi di errore Parallel Data Warehouse (PDW) segnalano gli errori e problemi rilevati dai componenti PDW e possono includere anche gli errori di SQL Server rilevati tramite PDW. Questi messaggi di errore usano una sintassi coerente per la presentazione di informazioni. La comprensione di questa sintassi verrà consentono di identificare e risolvere i problemi.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ffc7a097845f4652f56d82c572ecfab868d33f1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419202"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>Messaggi di errore in Parallel Data Warehouse

I messaggi di errore Parallel Data Warehouse (PDW) segnalano gli errori e problemi rilevati dai componenti PDW e possono includere anche gli errori di SQL Server rilevati tramite PDW. Questi messaggi di errore usano una sintassi coerente per la presentazione di informazioni. La comprensione di questa sintassi verrà consentono di identificare e risolvere i problemi su SQL Server PDW.  
  
## <a name="Basics"></a>Nozioni fondamentali di messaggio di errore  
I messaggi di errore vengono restituiti seguono la stessa sintassi.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Questi sono i possibili valori per ogni campo:  
  
|Campo|Descrizione|Esempio|  
|---------|---------------|-----------|  
|*Error_Indicator*|La parola "Errore" o altro testo di avviso all'utente di un problema.|error|  
|*SQL_State_Code*|Codice di stato di SQL, in base alla specifica ODBC. Il driver genera il codice di stato SQL appropriato ogni volta che viene restituito un messaggio a un'applicazione. Il testo "Microsoft" indica l'origine dell'errore.|42000|  
|*Driver_Details*|Dettagli driver dipendente, ad esempio il tipo del driver usato.|Driver ODBC SQL Server 2008 R2 Parallel Data Warehouse|  
|*QueryID*|Identificatore univoco per la query. Utilizzare questo valore per trovare informazioni aggiuntive correlate all'elaborazione della query. Ad esempio, i dettagli di esecuzione di query sono reperibile nella Console di amministrazione usando l'ID di query. Per altre informazioni, vedere [monitorare l'Appliance usando la Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Se un QueryID non è applicabile, il testo "Interno" viene restituito all'utente.|QID2377|  
|*Message_String*|Descrizione leggibile dell'errore o problema. Quando restituisce errori di SQL Server, questo è il testo del messaggio SQL Server.|Può essere visualizzato solo l'assegnazione uguale nell'elenco di set di un'istruzione UPDATE.|  
  
Questi valori di esempio potrebbero essere presentati all'utente simile al seguente:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Informazioni sugli avvisi della Console di amministrazione](understanding-admin-console-alerts.md)  
  
