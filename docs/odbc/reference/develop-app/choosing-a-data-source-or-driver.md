---
title: Scelta dei dati di un'origine o il Driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9aac31af80ff5774d464f76f130d2d113002e60a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001394"
---
# <a name="choosing-a-data-source-or-driver"></a>Scelta di un'origine dati o driver
L'origine dati o il driver utilizzato da un'applicazione a volte è hardcoded nell'applicazione. Ad esempio, un'applicazione personalizzata scritta da un reparto MIS per trasferire dati da un'origine dati a un altro che contengono nomi di tali dati di origini: l'applicazione semplicemente non funziona con tutte le altre origini dati. Un altro esempio è un'applicazione verticale, ad esempio un oggetto utilizzato per l'inserimento dell'ordine. Tale applicazione sempre Usa la stessa origine dati, che ha uno schema predefinito noto con l'applicazione.  
  
 Altre applicazioni selezionare l'origine dati o il driver in fase di esecuzione. In genere, queste sono applicazioni generiche che eseguire query ad hoc, ad esempio un foglio di calcolo che usa ODBC per importare i dati. Tali applicazioni in genere elencare le origini dati disponibili o i driver e consentono agli utenti di scegliere i clienti che desiderano utilizzare. Indica se un'applicazione generica sono elencate le origini dati, i driver o entrambi spesso varia a seconda che l'applicazione usi driver basati su DBMS o basate su file.  
  
 Driver basati su DBMS richiedono in genere un set complesso di informazioni di connessione, ad esempio l'indirizzo di rete, protocollo di rete, nome del database e così via. Lo scopo di un'origine dati è nascondere tutte queste informazioni. Pertanto, il paradigma di origine dati si presta da usare con driver basati su DBMS. Un'applicazione può visualizzare un elenco delle origini dati per l'utente in uno dei due modi. Può chiamare **SQLDriverConnect** con il **DSN** parola chiave (Data Source Name) e nessun valore associato; il Driver visualizzerà un elenco di nomi delle origini dati. Se l'applicazione deve controllare l'aspetto dell'elenco, chiama il metodo **SQLDataSources** per recuperare un elenco di disponibili origini dati e crea una finestra di dialogo. Questa funzione è implementata da Gestione Driver e può essere chiamata prima di qualsiasi driver sono stati caricati. Quindi, l'applicazione chiama una funzione di connessione e lo passa il nome dell'origine dati scelto.  
  
 Se un'origine dati non viene specificata, viene utilizzata l'origine dati predefinito indicato dalle informazioni sul sistema. (Per altre informazioni, vedere [sottochiave Default](../../../odbc/reference/install/default-subkey.md).) Se **SQLConnect** viene chiamato con un *ServerName* argomento che non è stata trovata, è un puntatore null o è "DEFAULT", gestione Driver si connette all'origine dati predefinita. L'impostazione predefinita l'origine dati viene usata anche se la stringa di connessione viene usato in una chiamata a **SQLDriverConnect** oppure **SQLBrowseConnect** contiene il **DSN** (parola chiave) impostata sul valore predefinito" "o se l'origine dati specificata non viene trovato. Inoltre, l'impostazione predefinita l'origine dati viene usata se la stringa di connessione viene utilizzato in una chiamata a **SQLDriverConnect** non contiene il **DSN** (parola chiave).  
  
 Con i driver basati su file, è possibile utilizzare un paradigma di file. Per i dati archiviati nel computer locale, gli utenti spesso sapere che i dati in un determinato file, ad esempio Employee. dbf. Invece di selezionare un'origine dati sconosciuti, risulta più semplice per tali utenti selezionare il file conosciuti. Per implementare questa operazione, viene chiamato **SQLDrivers**. Questa funzione è implementata da Gestione Driver e può essere chiamata prima di qualsiasi driver sono stati caricati. **SQLDrivers** restituisce un elenco dei driver disponibili; restituisce inoltre i valori per il **FileUsage** e **FileExtns** parole chiave. Il **FileUsage** (parola chiave) viene spiegato se driver basati su file considera i file come tabelle, non Xbase oppure come database, come invece avviene in Microsoft® Access. Il **FileExtns** (parola chiave) Elenca le estensioni del nome file driver riconosce, ad esempio file con estensione dbf per ottenere un driver Xbase. Utilizzando queste informazioni, l'applicazione crea una finestra di dialogo tramite il quale l'utente sceglie un file. In base all'estensione del file selezionato, quindi l'applicazione si connette al driver chiamando **SQLDriverConnect** con il **DRIVER** (parola chiave).  
  
 Non c'è niente per interrompere un'applicazione utilizzando un'origine dati con un driver basati su file o la chiamata **SQLDriverConnect** con il **DRIVER** parola chiave per la connessione a un driver basati su DBMS. Ecco alcuni usi comuni del **DRIVER** (parola chiave) di driver basati su DBMS:  
  
-   **Non creare origini dati.** Ad esempio, un'applicazione personalizzata potrebbe utilizzare un driver specifico e un database. Se il nome del driver e tutte le informazioni necessarie per connettersi al database è hardcoded nell'applicazione, gli utenti non devono creare un'origine dati nel proprio computer per eseguire l'applicazione. Tutto deve essere eseguito è installare l'applicazione e i driver.  
  
     Uno svantaggio di questo metodo è che l'applicazione deve essere ricompilata e ridistribuito se le informazioni di connessione viene modificata. Se un nome dell'origine dati è hardcoded nell'applicazione anziché le informazioni di connessione completa, ogni utente deve modificare solo le informazioni nell'origine dati.  
  
-   **L'accesso a un determinato DBMS una sola volta.** Ad esempio, potrebbe contenere un foglio di calcolo che recupera i dati tramite una chiamata di funzioni di ODBC di **DRIVER** parola chiave per identificare un driver specifico. Poiché il nome del driver è significativo per gli utenti che dispongono di tale driver, il foglio di calcolo potrebbe essere passato tra tali utenti. Se il foglio di calcolo contiene un nome dell'origine dati, ogni utente dovrà creare la stessa origine dati per l'uso del foglio di calcolo.  
  
-   **Esplorazione del sistema per tutti i database accessibili a un driver specifico.** Per altre informazioni, vedere [connessione con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), più avanti in questa sezione.
