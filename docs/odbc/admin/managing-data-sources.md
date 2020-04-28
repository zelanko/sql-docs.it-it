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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307212"
---
# <a name="managing-data-sources"></a>Gestione delle origini dati
Dopo aver installato un driver ODBC dal programma di installazione del driver, è possibile definire una o più origini dati. Il nome dell'origine dati (DSN) deve fornire una descrizione univoca dei dati; ad esempio, le *retribuzioni* o gli *account pagabili*. Le origini dati utente e di sistema definite per tutti i driver attualmente installati sono elencate nelle schede **DSN utente** o **DSN di sistema** della finestra di dialogo **Amministrazione origine dati ODBC** . Le origini dati dei file in una determinata directory sono elencate nella scheda **DSN del file** . la directory da visualizzare viene immessa nella casella **Cerca in** nella scheda **DSN del file** .  
  
> [!NOTE]  
>  Per gestire un'origine dati che si connette a un driver a 32 bit nella piattaforma a 64 bit, usare c:\windows\sysWOW64\odbcad32.exe. Per gestire un'origine dati che si connette a un driver a 64 bit, utilizzare c:\windows\system32\odbcad32.exe. In **strumenti di amministrazione** in un sistema operativo Windows 8 a 64 bit sono disponibili icone per la finestra di dialogo **Amministrazione origine dati ODBC** a 32 bit e 64 bit.  
  
 Se si usa odbcad32. exe a 64 bit per configurare o rimuovere un DSN che si connette a un driver a 32 bit, ad esempio, il **driver esegue Microsoft Access\*(MDB)**, verrà visualizzato il messaggio di errore seguente:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Per correggere l'errore, utilizzare odbcad32. exe a 32 bit per configurare o rimuovere il DSN.  
  
 Un'origine dati associa un determinato driver ODBC ai dati a cui si desidera accedere tramite tale driver. Ad esempio, è possibile creare un'origine dati per utilizzare il driver dBASE ODBC per accedere a uno o più file dBASE trovati in una directory specifica del disco rigido o di un'unità di rete. Utilizzando Amministrazione origine dati ODBC, è possibile aggiungere, modificare ed eliminare origini dati, come descritto nella tabella seguente.  
  
|Azione|Descrizione|  
|------------|-----------------|  
|Aggiunta di origini dati|È possibile aggiungere più origini dati, ognuna delle quali associa un driver ad alcuni dati a cui si desidera accedere usando tale driver. Assegnare a ogni origine dati un nome che identifichi in modo univoco l'origine dati. Se, ad esempio, si crea un'origine dati per un set di file dBASE contenenti informazioni sul cliente, è possibile denominare l'origine dati "Customers". Le applicazioni in genere visualizzano i nomi delle origini dati da cui gli utenti possono scegliere.<br /><br /> L'aggiunta di un'origine dati di file è leggermente diversa dall'aggiunta di origini dati utente o di sistema. Per ulteriori informazioni, vedere il file della Guida dell'amministratore dell'origine dati ODBC.|  
|Modifica di origini dati|A seconda dei requisiti, potrebbe essere necessario riconfigurare le origini dati. È possibile reimpostare le opzioni facendo clic su **Configura** nella finestra di dialogo configurazione driver.|  
|Eliminazione di origini dati|Fare clic su **Rimuovi** dopo aver selezionato un'origine dati.|  
  
 Per ulteriori informazioni sulle origini dati dei file, vedere [connessione tramite origini dati file](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) o la [funzione SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministratore origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md)
