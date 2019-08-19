---
title: Supplemento alla privacy di SQL Server | Microsoft Docs
ms.date: 01/19/2019
ms.prod: sql
ms.reviewer: mikeray
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: aliceku
ms.author: aliceku
ms.openlocfilehash: c92eead00b10c4a26a93234c3bbfeebf254f6aff
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028838"
---
# <a name="sql-server-privacy-supplement"></a>Supplemento alla privacy di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo riepiloga le funzionalità abilitate per Internet che consentono di raccogliere e inviare a Microsoft dati anonimi di diagnostica e di utilizzo delle funzionalità. SQL Server può raccogliere informazioni standard sul computer e dati relativi all'uso e alle prestazioni che possono venire trasmessi a Microsoft e analizzati al fine di migliorare la qualità, la sicurezza e l'affidabilità del prodotto. Questo articolo funge da supplemento all'[Informativa sulla privacy di Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839). La classificazione dei dati in questo articolo si applica solo alle versioni del prodotto SQL Server locale. Non si applica agli elementi seguenti:

- Database SQL di Azure
- [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-telemetry-ssms?view=sql-server-2017)
- SQL Server Data Tools (SSDT)
- Azure Data Studio
- Data Migration Assistant
- SQL Server Migration Assistant
- Estensione MS-SQL

Definizione di *scenari di utilizzo consentiti*. Per il contesto di questo articolo, Microsoft definisce "scenari di utilizzo consentiti" le azioni o le attività avviate da Microsoft.

## <a name="access-control"></a>Controllo di accesso

Informazioni correlate alle credenziali usate per proteggere gli account di accesso, gli utenti o gli account all'interno di un'installazione di SQL Server.

### <a name="examples-of-access-control"></a>Esempi di controllo di accesso

- Password
- Certificati

### <a name="permitted-usage-scenarios"></a>Scenari di utilizzo consentiti

|Scenario |Restrizioni di accesso |Requisiti di mantenimento |
|---------|---------|---------|
|Queste credenziali non lasciano mai il computer dell'utente come dati di Utilizzo e diagnostica. |- |- |
|I dump di arresto anomalo del sistema possono contenere dati di controllo di accesso. |- |Dump di arresto anomalo: massimo 30 giorni. |
|Queste credenziali non lasciano mai il computer dell'utente mediante il feedback utente a meno che il cliente non le inserisca manualmente |Limite all'uso interno Microsoft senza accesso per terze parti. |Commenti e suggerimenti degli utenti: massimo 1 anno|
|&nbsp;|&nbsp;|&nbsp;|

## <a name="customer-content"></a>Contenuto del cliente

Si definiscono contenuto del cliente i dati archiviati nelle tabelle utente, direttamente o indirettamente. I dati includono valori letterali o statistiche dell'utente all'interno di testi di query che possono essere archiviati nelle tabelle utente.

### <a name="examples-of-customer-content"></a>Esempi di contenuto del cliente

- Valori di dati archiviati nelle righe di una tabella utente.
- Oggetti di statistiche contenenti le copie di valori nelle righe di una tabella utente.
- Testi di query contenenti valori letterali.

### <a name="permitted-usage-scenarios"></a>Scenari di utilizzo consentiti

|Scenario  |Restrizioni di accesso  |Requisiti di mantenimento |
|---------|---------|---------|
|Questi dati non lasciano il computer dell'utente come dati di Utilizzo e diagnostica. |- |- |
|I dump di arresto anomalo del sistema possono includere contenuto del cliente ed essere inviati a Microsoft. |- |Dump di arresto anomalo: massimo 30 giorni. |
|I clienti possono dare il proprio consenso all'invio a Microsoft di feedback utente che include contenuto del cliente. |Limite all'uso interno Microsoft senza accesso per terze parti. Microsoft può rendere disponibili i dati al cliente originale. |Commenti e suggerimenti degli utenti: massimo 1 anno |

## <a name="end-user-identifiable-information-euii"></a>Informazioni personali dell'utente finale

Dati ricevuti da un utente o generati dall'uso del prodotto.
- Collegabili a un singolo utente.
- Non includono contenuto.

### <a name="examples-of-end-user-identifiable-information"></a>Esempi di informazioni personali dell'utente finale

- Identificazione dell'interfaccia. Indirizzo IP completo
- Nome del computer
- Credenziali di accesso/Nomi utente
- Parte personalizzata dell'indirizzo di posta elettronica (joe@contoso.com)
- Informazioni sulla posizione
- Identificazione del cliente

### <a name="permitted-usage-scenarios"></a>Scenari di utilizzo consentiti

|Scenario  |Restrizioni di accesso  |Requisiti di mantenimento|
|---------|---------|---------|
|Questi dati non lasciano il computer dell'utente come dati di Utilizzo e diagnostica. |- |- |
|I dump di arresto anomalo del sistema possono includere informazioni personali dell'utente finale e possono essere inviati a Microsoft. |- |Dump di arresto anomalo: massimo 30 giorni |
|L'ID di identificazione del cliente può essere inviato a Microsoft per offrire nuove funzionalità ibride e cloud che gli utenti hanno sottoscritto. |- |Attualmente non esiste alcuna funzionalità ibrida o cloud di questo tipo.|
|I clienti possono dare il proprio consenso all'invio a Microsoft di feedback utente che include contenuto del cliente.|Limite all'uso interno Microsoft senza accesso per terze parti. Microsoft può rendere disponibili i dati al cliente originale. |Commenti e suggerimenti degli utenti: massimo 1 anno |

## <a name="internet-based-services-data"></a>Dati dei servizi basati su Internet

Dati necessari per offrire servizi basati su Internet, in base al contratto di licenza con l'utente finale di SQL Server.

### <a name="examples-of-internet-based-services-data"></a>Esempi di dati dei servizi basati su Internet

- Informazioni sulle specifiche del computer
- Nome/versione del browser
- Versione di SQL Server
- Codice lingua
- Un indirizzo IP con determinati ottetti rimossi
- Dati di mapping

### <a name="permitted-usage-scenarios"></a>Scenari di utilizzo consentiti

|Scenario  |Restrizioni di accesso  |Requisiti di mantenimento|
|---------|---------|---------| 
|Possono essere usati da Microsoft per migliorare le funzionalità e/o eliminare bug nelle funzionalità correnti. |Limite all'uso interno Microsoft senza accesso per terze parti. Microsoft può rendere disponibili i dati al cliente originale.  Ad esempio, i dashboard |Minimo 90 giorni - Massimo 3 anni |
|I clienti possono dare il proprio consenso all'invio a Microsoft di feedback utente che include contenuto del cliente. |Limite all'uso interno Microsoft senza accesso per terze parti. |I clienti possono dare il proprio consenso all'invio a Microsoft di feedback utente che include contenuto del cliente. |
|Gli elementi mappa di Power View e di SQL Server Reporting Services possono inviare dati per l'uso delle mappe di Bing. |Limite ai dati della sessione |- |

## <a name="system-metadata"></a>Metadati di sistema

Dati generati nel corso dell'esecuzione del server.  I dati non includono contenuto del cliente.

### <a name="examples-of-system-metadata"></a>Esempi di metadati di sistema

I dati riportati di seguito sono considerati metadati di sistema se non includono contenuto del cliente, metadati oggetto, dati di controllo di accesso del cliente o informazioni personali dell'utente finale:

- GUID del database
- Hash del nome del computer
- Hash del nome dell'istanza
- Nome applicazione
- Dati sul comportamento o l'utilizzo
- Dati relativi al programma Analisi utilizzo software di SQL
- Dati di configurazione del server, ad esempio le impostazioni di sp_configure
- Dati di configurazione delle funzionalità
- Nomi degli eventi e codici di errore
- Impostazioni hardware e identificazione, ad esempio il produttore OEM

Microsoft esamina i valori dei nomi di applicazione impostati da altri programmi che usano SQL Server (ad esempio SharePoint o programmi di terze parti includono queste informazioni nei metadati di sistema inviati Microsoft quando sono abilitati i dati di utilizzo). I clienti non devono inserire dati personali, ad esempio le informazioni personali dell'utente finale, nei campi di metadati di sistema o creare applicazioni progettate per archiviare dati personali in questi campi. 

### <a name="permitted-usage-scenarios"></a>Scenari di utilizzo consentiti

|Scenario  |Restrizioni di accesso  |Requisiti di mantenimento|
|---------|---------|---------|
|Possono essere usati da Microsoft per migliorare le funzionalità e/o eliminare bug nelle funzionalità correnti.|Limite all'uso interno Microsoft senza accesso per terze parti. |Minimo 90 giorni - Massimo 3 anni |
|Possono essere usati per offrire suggerimenti al cliente.  Ad esempio, si può consigliare, in base all'utilizzo del prodotto, di valutare l'uso della funzionalità *X* poiché consentirebbe prestazioni superiori. |Microsoft può rendere disponibili i dati al cliente originale, ad esempio mediante i dashboard. |Registri di protezione dei dati dei clienti: minimo 3 anni, massimo 6 anni |
|Possono essere usati da Microsoft per la pianificazione futura dei prodotti. |Microsoft può condividere queste informazioni con altri fornitori di hardware e software per migliorare il funzionamento dei loro prodotti con il software Microsoft. |Minimo 90 giorni - Massimo 3 anni|
|Possono essere usati da Microsoft per offrire servizi basati su cloud in base ai dati di Utilizzo e diagnostica generati. Ad esempio, un dashboard cliente che illustra l'utilizzo di funzionalità in tutte le installazioni di SQL Server all'interno di un'organizzazione. |Microsoft può rendere disponibili i dati al cliente originale, ad esempio mediante i dashboard. |Minimo 90 giorni - Massimo 3 anni |
|I clienti possono dare il proprio consenso all'invio a Microsoft di feedback utente che include contenuto del cliente. |Limite all'uso interno Microsoft senza accesso per terze parti. Microsoft può rendere disponibili i dati al cliente originale. |Commenti e suggerimenti degli utenti: massimo 1 anno |
|Il nome del database e il nome dell'applicazione possono essere usati per classificare i database e le applicazioni in categorie note, ad esempio quelli che potrebbero eseguire software fornito da Microsoft o da altre società.|Limite all'uso interno Microsoft senza accesso per terze parti.|Minimo 90 giorni - Massimo 3 anni |

## <a name="object-metadata"></a>Metadati degli oggetti

Dati che descrivono o vengono usati per configurare server, database, tabelle e altre risorse.  I metadati degli oggetti includono i nomi delle tabelle e delle colonne del database ma non i contenuti delle righe del database o altri contenuti del cliente. I clienti non devono inserire dati personali, ad esempio le informazioni personali dell'utente finale, nei campi di metadati degli oggetti o creare applicazioni progettate per archiviare dati personali in questi campi. Per lo scenario di utilizzo consentito riportato di seguito, viene usato solo il formato hash per determinare i modelli di utilizzo per migliorare il prodotto. 

### <a name="examples-of-object-metadata"></a>Esempi di metadati degli oggetti

- Nomi di database di SQL Server
- Nomi di tabelle e colonne
- Nomi di statistiche

### <a name="permitted-usage-scenarios"></a>Scenari di utilizzo consentiti

> [!NOTE]
> Prima della raccolta viene eseguito l'hashing di tutti i valori dei metadati degli oggetti.
>

|Scenario  |Restrizioni di accesso  |Requisiti di mantenimento|
|---------|---------|---------|
|Possono essere usati da Microsoft per migliorare le funzionalità e/o eliminare bug nelle funzionalità correnti. |Limite all'uso interno Microsoft senza accesso per terze parti. |Minimo 90 giorni - Massimo 3 anni|

## <a name="telemetry-controls"></a>Controlli di telemetria

Per istruzioni su come attivare/disattivare la telemetria nel prodotto, è possibile fare riferimento a questo articolo: https://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
