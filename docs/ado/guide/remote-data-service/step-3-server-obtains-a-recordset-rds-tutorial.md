---
description: 'Passaggio 3: Il server ottiene un recordset (esercitazione su RDS)'
title: 'Passaggio 3: il server ottiene un recordset (esercitazione su RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
author: rothja
ms.author: jroth
ms.openlocfilehash: 22664ed2943800702bbb12afe6900c1ca9bac6bd
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759121"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>Passaggio 3: Il server ottiene un recordset (esercitazione su RDS)
Il programma server utilizza la stringa di connessione e il testo del comando per eseguire una query sull'origine dati per le righe desiderate. ADO viene in genere utilizzato per recuperare questo **Recordset**, sebbene sia possibile utilizzare altre interfacce di accesso ai dati Microsoft, ad esempio OLE DB.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Un programma server personalizzato potrebbe essere simile al seguente:  
  
```vb
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 4: il server restituisce il recordset (esercitazione su RDS)](./step-4-server-returns-the-recordset-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](./rds-tutorial-vbscript.md)