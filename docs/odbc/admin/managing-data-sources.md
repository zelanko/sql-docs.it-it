---
title: Gestione delle origini dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a1f8893351ceb68ebd7c42e3ac82c876c01c10b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198761"
---
# <a name="managing-data-sources"></a>Gestione delle origini dati
Dopo aver installato un driver ODBC dal programma di installazione del driver, è possibile definire uno o più origini dati per tale. Il nome di origine dati (DSN) deve fornire una descrizione univoca dei dati. ad esempio, *Payroll* oppure *contabilità fornitori*. Sono elencate le origini dati utente e di sistema definiti per tutti attualmente installati i driver nel **DSN utente** o **DSN di sistema** schede della finestra di **Amministrazione origine dati ODBC**finestra di dialogo. Vengono elencate le origini di dati file in una determinata directory nel **DSN su File** scheda; la directory da visualizzare viene immesso nel **Cerca in** nella casella il **DSN su File** scheda.  
  
> [!NOTE]  
>  Per gestire un'origine dati che si connette a un driver a 32 bit in piattaforme a 64 bit, utilizzare c:\windows\sysWOW64\odbcad32.exe. Per gestire un'origine dati che si connette a un driver a 64 bit, utilizzare c:\windows\system32\odbcad32.exe. Nelle **strumenti di amministrazione** in un sistema operativo Windows 8 a 64 bit, sono presenti icone per 32 bit e 64 bit **Amministrazione origine dati ODBC** nella finestra di dialogo.  
  
 Se si usa il odbcad32.exe a 64 bit per configurare o rimuovere un DSN che si connette a un driver a 32 bit, ad esempio, **Driver è Microsoft Access (\*mdb)**, si riceverà il messaggio di errore seguente:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Per risolvere questo errore, usare il odbcad32.exe 32 bit per configurare o rimuovere il DSN.  
  
 Un'origine dati consente di associare un driver ODBC specifico con i dati che si desidera accedere tramite tale driver. Ad esempio, è possibile creare un'origine dati per utilizzare il driver dBASE ODBC per accedere a uno o più file dBASE trovati in una directory specifica sul disco rigido o un'unità di rete. Tramite Amministrazione origine dati ODBC, è possibile aggiungere, modificare ed eliminare origini dati, come descritto nella tabella seguente.  
  
|Azione|Descrizione|  
|------------|-----------------|  
|Aggiunta di origini dati|È possibile aggiungere più origini dati, ognuno di essi l'associazione di un driver con alcuni dati che si desidera accedere utilizzando tale driver. Assegnare un nome che identifica in modo univoco tale origine dati di ogni origine dati. Ad esempio, se si crea un'origine dati per un set di file dBASE che contengono informazioni sul cliente, è possibile denominare l'origine dati "Customers". Le applicazioni in genere visualizzare nomi di origine dati per gli utenti scelgano da.<br /><br /> Aggiunta di un'origine dati file è leggermente diversa dall'aggiunta di origini dati di sistema o utente. Per altre informazioni, vedere l'amministratore dell'origine dati ODBC file della Guida.|  
|Modifica delle origini dati|A seconda dei requisiti, si potrebbe essere necessario riconfigurare le origini dati. È possibile reimpostare le opzioni facendo **configura** in qualsiasi finestra di dialogo programma di installazione di driver.|  
|Eliminazione di origini dati|Fare clic su **rimuovere** dopo aver selezionato un'origine dati.|  
  
 Per altre informazioni sulle origini dati dei file, vedere [ci si connette tramite File Zdroje dat](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) o nella [funzione SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministratore origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md)
