---
title: Scelta di un'origine dati o di un driver | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303372"
---
# <a name="choosing-a-data-source-or-driver"></a>Scelta di un'origine dati o driver
L'origine dati o il driver utilizzato da un'applicazione è talvolta hardcoded nell'applicazione. Ad esempio, un'applicazione personalizzata scritta da un reparto MIS per trasferire i dati da un'origine dati a un'altra contiene i nomi di tali origini dati. l'applicazione non funziona semplicemente con altre origini dati. Un altro esempio è un'applicazione verticale, ad esempio una utilizzata per l'immissione dell'ordine. Tale applicazione utilizza sempre la stessa origine dati, che dispone di uno schema predefinito noto dall'applicazione.  
  
 Altre applicazioni selezionare l'origine dati o il driver in fase di esecuzione. Si tratta in genere di applicazioni generiche che eseguono query ad hoc, ad esempio un foglio di calcolo che usa ODBC per importare i dati. Tali applicazioni in genere elencano le origini dati o i driver disponibili e consentono agli utenti di scegliere quelli che desiderano utilizzare. Se un'applicazione generica elenca le origini dati, i driver o entrambi spesso dipendono dal fatto che l'applicazione utilizzi driver basati su DBMS o basati su file.  
  
 I driver basati su DBMS richiedono in genere un set complesso di informazioni di connessione, ad esempio l'indirizzo di rete, il protocollo di rete, il nome del database e così via. Lo scopo di un'origine dati è nascondere tutte queste informazioni. Pertanto, il paradigma dell'origine dati si presta a essere utilizzato con i driver basati su DBMS. Un'applicazione può visualizzare un elenco di origini dati per l'utente in uno dei due modi seguenti. Può chiamare **SQLDriverConnect** con la parola chiave **DSN** (Data Source Name) e nessun valore associato. in Gestione driver viene visualizzato un elenco di nomi di origine dati. Se l'applicazione vuole controllare l'aspetto dell'elenco, chiama **SQLDataSources** per recuperare un elenco di origini dati disponibili e costruisce la propria finestra di dialogo. Questa funzione viene implementata da Gestione driver e può essere chiamata prima del caricamento di tutti i driver. L'applicazione chiama quindi una funzione di connessione e la passa al nome dell'origine dati scelta.  
  
 Se non si specifica un'origine dati, viene utilizzata l'origine dati predefinita indicata dalle informazioni di sistema. Per ulteriori informazioni, vedere la [sottochiave default](../../../odbc/reference/install/default-subkey.md). Se **SQLConnect** viene chiamato utilizzando un argomento *ServerName* che non è possibile trovare, è un puntatore null o è "default", gestione driver si connette all'origine dati predefinita. L'origine dati predefinita viene inoltre utilizzata se la stringa di connessione utilizzata in una chiamata a **SQLDriverConnect** o **SQLBrowseConnect** contiene la parola chiave **DSN** impostata su "default" o se l'origine dati specificata non viene trovata. Viene inoltre utilizzata l'origine dati predefinita se la stringa di connessione utilizzata in una chiamata a **SQLDriverConnect** non contiene la parola chiave **DSN** .  
  
 Con i driver basati su file, è possibile usare un paradigma di file. Per i dati archiviati nel computer locale, gli utenti sanno spesso che i dati si trovano in un file specifico, ad esempio Employee. dbf. Anziché selezionare un'origine dati sconosciuta, è più semplice per tali utenti selezionare il file che conoscono. Per implementare questa operazione, l'applicazione chiama innanzitutto **SQLDrivers**. Questa funzione viene implementata da Gestione driver e può essere chiamata prima del caricamento di tutti i driver. **SQLDrivers** restituisce un elenco di driver disponibili. restituisce inoltre i valori per le parole chiave **fileusage** e **FileExtns** . La parola chiave **fileusage** spiega se i driver basati su file gestiscono i file come tabelle, così come Xbase, o come database, così come Microsoft® Access. La parola chiave **FileExtns** elenca le estensioni dei nomi di file riconosciute dal driver, ad esempio DBF per un driver Xbase. Utilizzando queste informazioni, l'applicazione crea una finestra di dialogo tramite la quale l'utente sceglie un file. In base all'estensione del file scelto, l'applicazione si connette al driver chiamando **SQLDriverConnect** con la parola chiave **driver** .  
  
 Non c'è nulla da impedire a un'applicazione di usare un'origine dati con un driver basato su file o chiamare **SQLDriverConnect** con la parola chiave **driver** per connettersi a un driver basato su DBMS. Di seguito sono riportati alcuni usi comuni della parola chiave **driver** per i driver basati su DBMS:  
  
-   **Impossibile creare origini dati.** Ad esempio, un'applicazione personalizzata può usare un driver e un database specifici. Se il nome del driver e tutte le informazioni necessarie per la connessione al database sono hardcoded nell'applicazione, gli utenti non devono creare un'origine dati nel computer per eseguire l'applicazione. È necessario installare l'applicazione e il driver.  
  
     Uno svantaggio di questo metodo è che l'applicazione deve essere ricompilata e ridistribuita se le informazioni di connessione cambiano. Se un nome di origine dati è hardcoded nell'applicazione anziché completare le informazioni di connessione, ogni utente deve modificare solo le informazioni nell'origine dati.  
  
-   **Accesso a un particolare DBMS una sola volta.** Ad esempio, un foglio di calcolo che recupera i dati chiamando le funzioni ODBC può contenere la parola chiave **driver** per identificare un driver specifico. Poiché il nome del driver è significativo per gli utenti che hanno tale driver, il foglio di calcolo potrebbe essere passato tra questi utenti. Se il foglio di calcolo contiene un nome di origine dati, ogni utente dovrà creare la stessa origine dati per utilizzare il foglio di calcolo.  
  
-   **Esplorazione del sistema per tutti i database accessibili a un driver specifico.** Per ulteriori informazioni, vedere [Connecting with SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), più avanti in questa sezione.
