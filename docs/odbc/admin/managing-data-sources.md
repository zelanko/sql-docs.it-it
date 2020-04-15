---
title: Gestione delle origini dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307212"
---
# <a name="managing-data-sources"></a>Gestione delle origini dati
Dopo aver installato un driver ODBC dal programma di installazione del driver, è possibile definire una o più origini dati per tale driver. Il nome dell'origine dati (DSN) deve fornire una descrizione univoca dei dati. ad esempio *Retribuzioni* o *Contabilità fornitori*. Le origini dati utente e di sistema definite per tutti i driver attualmente installati sono elencate nelle schede **DSN utente** o **DSN** di sistema della finestra di dialogo **Amministratore origine dati ODBC.** Le origini dati sui file in una determinata directory sono elencate nella scheda **DSN su file.** la directory da visualizzare viene immessa nella casella **Cerca in** nella scheda **DSN su file.**  
  
> [!NOTE]  
>  Per gestire un'origine dati che si connette a un driver a 32 bit nella piattaforma a 64 bit, utilizzare c: Per gestire un'origine dati che si connette a un driver a 64 bit, utilizzare c: In **Strumenti** di amministrazione in un sistema operativo Windows 8 a 64 bit sono disponibili icone per la finestra di dialogo **Amministratore origine dati ODBC** a 32 bit e a 64 bit.  
  
 Se si utilizza odbcad32.exe a 64 bit per configurare o rimuovere un DSN che si connette a un driver a 32 bit, ad esempio **Driver do Microsoft Access (\*.mdb)**, verrà visualizzato il seguente messaggio di errore:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Per risolvere questo errore, utilizzare il file odbcad32.exe a 32 bit per configurare o rimuovere il DSN.  
  
 Un'origine dati associa un driver ODBC specifico ai dati a cui si desidera accedere tramite tale driver. Ad esempio, è possibile creare un'origine dati per utilizzare il driver ODBC dBASE per accedere a uno o più file dBASE trovati in una directory specifica sul disco rigido o in un'unità di rete. Utilizzando Amministrazione origine dati ODBC, è possibile aggiungere, modificare ed eliminare origini dati, come descritto nella tabella seguente.  
  
|Azione|Descrizione|  
|------------|-----------------|  
|Aggiunta di origini dati|È possibile aggiungere più origini dati, ognuna delle quali associa un driver ad alcuni dati a cui si desidera accedere utilizzando tale driver. Assegnare a ogni origine dati un nome che identifichi in modo univoco tale origine dati. Ad esempio, se si crea un'origine dati per un set di file dBASE contenenti informazioni sui clienti, è possibile denominare l'origine dati "Clienti". Le applicazioni in genere visualizzano i nomi delle origini dati tra cui gli utenti possono scegliere.<br /><br /> L'aggiunta di un'origine dati su file è leggermente diversa dall'aggiunta di origini dati utente o di sistema. Per ulteriori informazioni, vedere il file della Guida di Amministrazione origine dati ODBC.|  
|Modifica delle origini dati|A seconda dei requisiti, potrebbe essere necessario riconfigurare le origini dati. È possibile reimpostare le opzioni facendo clic su **Configura** in qualsiasi finestra di dialogo di configurazione del driver.|  
|Eliminazione delle origini dati|Fare clic su **Rimuovi** dopo aver selezionato un'origine dati.|  
  
 Per ulteriori informazioni sulle origini dati su file, vedere [Connessione tramite origini dati file](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) o Funzione [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministratore origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md)
