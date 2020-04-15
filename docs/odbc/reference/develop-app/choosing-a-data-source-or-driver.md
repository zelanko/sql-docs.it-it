---
title: Scelta di un'origine dati o di un driver Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303372"
---
# <a name="choosing-a-data-source-or-driver"></a>Scelta di un'origine dati o driver
L'origine dati o il driver utilizzato da un'applicazione è talvolta hardcoded nell'applicazione. Ad esempio, un'applicazione personalizzata scritta da un reparto MIS per trasferire dati da un'origine dati a un'altra conterrebbe i nomi di tali origini dati: l'applicazione semplicemente non funzionerebbe con altre origini dati. Un altro esempio è un'applicazione verticale, ad esempio un'applicazione utilizzata per l'inserimento di ordini. Tale applicazione utilizza sempre la stessa origine dati, che dispone di uno schema predefinito noto dall'applicazione.  
  
 Altre applicazioni selezionano l'origine dati o il driver in fase di esecuzione. In genere, si tratta di applicazioni generiche che eseguono query ad hoc, ad esempio un foglio di calcolo che utilizza ODBC per importare i dati. Tali applicazioni di solito elencano le origini dati o i driver disponibili e consentono agli utenti di scegliere quelli con cui vogliono lavorare. Il fatto che un'applicazione generica elenchi origini dati, driver o entrambi di spesso tipo a seconda che l'applicazione utilizzi driver basati su DBMS o su file.  
  
 I driver basati su DBMS richiedono in genere un insieme complesso di informazioni di connessione, ad esempio l'indirizzo di rete, il protocollo di rete, il nome del database e così via. Lo scopo di un'origine dati è nascondere tutte queste informazioni. Pertanto, il paradigma dell'origine dati si presta all'utilizzo con i driver basati su DBMS. Un'applicazione può visualizzare un elenco di origini dati per l'utente in uno dei due modi. Può chiamare **SQLDriverConnect** con la parola chiave **DSN** (Data Source Name) e nessun valore associato; Gestione Driver visualizzerà un elenco di nomi di origini dati. Se l'applicazione desidera il controllo sull'aspetto dell'elenco, chiama **SQLDataSources** per recuperare un elenco di origini dati disponibili e costruisce la propria finestra di dialogo. Questa funzione viene implementata da Gestione Driver e può essere chiamata prima del caricamento di qualsiasi driver. L'applicazione chiama quindi una funzione di connessione e le passa il nome dell'origine dati scelta.  
  
 Se non viene specificata un'origine dati, viene utilizzata l'origine dati predefinita indicata dalle informazioni di sistema. Per ulteriori informazioni, vedere [Sottochiave predefinita.](../../../odbc/reference/install/default-subkey.md) Se **SQLConnect** viene chiamato utilizzando un *ServerName* argomento che non è possibile trovare, è un puntatore null o è "DEFAULT", Gestione Driver si connette all'origine dati predefinita. L'origine dati predefinita viene utilizzata anche se la stringa di connessione utilizzata in una chiamata a **SQLDriverConnect** o **SQLBrowseConnect** contiene la parola chiave **DSN** impostata su "DEFAULT" o se l'origine dati specificata non viene trovata. Inoltre, l'origine dati predefinita viene utilizzata se la stringa di connessione utilizzata in una chiamata a **SQLDriverConnect** non contiene la parola chiave **DSN.**  
  
 Con i driver basati su file, è possibile utilizzare un paradigma di file. Per i dati archiviati nel computer locale, gli utenti spesso sanno che i dati si trova in un file specifico, ad esempio Employee.dbf. Invece di selezionare un'origine dati sconosciuta, è più facile per tali utenti selezionare il file che conoscono. Per implementare questo, l'applicazione chiama prima **SQLDrivers**. Questa funzione viene implementata da Gestione Driver e può essere chiamata prima del caricamento di qualsiasi driver. **SQLDrivers** restituisce un elenco di driver disponibili; restituisce inoltre i valori per le parole chiave **FileUsage** e **FileExtns.** La parola chiave **FileUsage** spiega se i driver basati su file trattano i file come tabelle, così come Xbase o come database, come Microsoft® Access. La parola chiave **FileExtns** elenca le estensioni di file riconosciute dal driver, ad esempio dbf per un driver Xbase. Utilizzando queste informazioni, l'applicazione crea una finestra di dialogo tramite la quale l'utente sceglie un file. In base all'estensione del file scelto, l'applicazione si connette al driver chiamando **SQLDriverConnect** con la parola chiave **DRIVER.**  
  
 Non c'è nulla per impedire a un'applicazione di utilizzare un'origine dati con un driver basato su file o chiamare **SQLDriverConnect** con la parola chiave **DRIVER** per connettersi a un driver basato su DBMS. Di seguito sono riportati diversi utilizzi comuni della parola chiave **DRIVER** per i driver basati su DBMS:  
  
-   **Non creazione di origini dati.** Ad esempio, un'applicazione personalizzata potrebbe utilizzare un driver e un database specifici. Se il nome del driver e tutte le informazioni necessarie per connettersi al database sono hardcoded nell'applicazione, gli utenti non devono creare un'origine dati nel computer per eseguire l'applicazione. Tutto quello che devono fare è installare l'applicazione e il driver.  
  
     Uno svantaggio di questo metodo è che l'applicazione deve essere ricompilata e ridistribuita se le informazioni di connessione vengono modificate. Se il nome di un'origine dati è hardcoded nell'applicazione anziché informazioni di connessione complete, ogni utente deve modificare solo le informazioni nell'origine dati.  
  
-   **Accesso a un determinato DBMS una sola volta.** Ad esempio, un foglio di calcolo che recupera i dati chiamando le funzioni ODBC potrebbe contenere la parola chiave **DRIVER** per identificare un driver specifico. Poiché il nome del driver è significativo per tutti gli utenti che dispongono di tale driver, il foglio di calcolo potrebbe essere passato tra tali utenti. Se il foglio di calcolo contiene un nome di origine dati, ogni utente dovrà creare la stessa origine dati per utilizzare il foglio di calcolo.  
  
-   **Esplorazione del sistema per tutti i database accessibili a un driver specifico.** Per ulteriori informazioni, vedere [Connessione con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)più avanti in questa sezione.
