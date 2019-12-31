---
title: messaggi di errore
description: I messaggi di errore di Parallel data warehouse (PDW) segnalano gli errori e i problemi riscontrati dai componenti di PDW e possono includere anche errori di SQL Server emersi tramite PDW. Questi messaggi di errore utilizzano una sintassi coerente per la presentazione delle informazioni. La comprensione di questa sintassi consente di identificare e correggere i problemi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401158"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>Messaggi di errore in parallelo data warehouse

I messaggi di errore di Parallel data warehouse (PDW) segnalano gli errori e i problemi riscontrati dai componenti di PDW e possono includere anche errori di SQL Server emersi tramite PDW. Questi messaggi di errore utilizzano una sintassi coerente per la presentazione delle informazioni. La comprensione di questa sintassi consente di identificare e correggere i problemi in SQL Server PDW.  
  
## <a name="Basics"></a>Nozioni di base sui messaggi di errore  
I messaggi di errore restituiti seguono la stessa sintassi.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Questi sono i valori potenziali per ogni campo:  
  
|Campo|Description|Esempio|  
|---------|---------------|-----------|  
|*Error_Indicator*|La parola "errore" o altro testo che avvisa l'utente di un problema.|ERRORE|  
|*SQL_State_Code*|Codice di stato SQL, in base alla specifica ODBC. Il driver genera il codice di stato SQL appropriato ogni volta che viene restituito un messaggio a un'applicazione. Il testo "Microsoft" indica l'origine dell'errore.|42000|  
|*Driver_Details*|Dettagli dipendenti dal driver, ad esempio il tipo di driver utilizzato.|Driver data warehouse parallelo di ODBC SQL Server 2008 R2|  
|*QueryID*|Identificatore univoco per la query. Utilizzare questo valore per trovare informazioni aggiuntive correlate all'elaborazione della query. Ad esempio, i dettagli sull'esecuzione della query sono disponibili nella console di amministrazione usando l'ID di query. Per altre informazioni, vedere [monitorare l'appliance usando la console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Se un QueryID non è applicabile, viene restituito all'utente il testo "Internal".|QID2377|  
|*Message_String*|Descrizione leggibile dell'errore o del problema. Quando si restituiscono SQL Server errori, questo è il testo del messaggio di SQL Server.|Nell'elenco set di un'istruzione UPDATE è possibile visualizzare solo l'assegnazione uguale.|  
  
Questi valori di esempio vengono presentati all'utente come segue:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Informazioni sugli avvisi della console di amministrazione](understanding-admin-console-alerts.md)  
  
