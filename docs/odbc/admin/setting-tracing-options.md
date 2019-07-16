---
title: Impostazione opzioni di traccia | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13e8caf9f3a9643f8063d6227258245a603f1665
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901627"
---
# <a name="setting-tracing-options"></a>Impostazione delle opzioni di traccia
Il **Tracing** scheda della finestra di **Amministrazione origine dati ODBC** nella finestra di dialogo consente di configurare la modalità di chiamate di funzione ODBC vengono tracciate.  
  
## <a name="how-tracing-works"></a>Funzionamento di traccia  
 Quando si avvia la traccia dal **traccia** scheda, gestione Driver registreranno tutte le chiamate di funzione ODBC per tutto successivamente eseguire le applicazioni. Chiamate di funzione ODBC da applicazioni in esecuzione prima che venga avviata la traccia non vengono registrate. Chiamate di funzione ODBC vengono registrate in un file di log specificato.  
  
 Traccia viene arrestata solo dopo aver fatto clic **Interrompi analisi**. Tenere presente che mentre traccia è attiva, il file di log continua ad aumentare e che questo influisce sulle prestazioni di tutte le applicazioni ODBC.  
  
 Per ulteriori informazioni sulla traccia, vedere [traccia](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Modifiche in una traccia ODBC  
 Prima di MDAC 2.7 SP2, traccia ODBC è stata consentita solo in base a livello di computer, in cui traccia acquisisce esposte informazioni dettagliate su tutte le applicazioni ODBC in esecuzione con identità. Questo incluso traccia per attività correlate a ODBC che potrebbero verificarsi per i processi creati o eseguiti per conto di altri account utente locali e l'entità di sicurezza predefinite, ad esempio il servizio locale e il servizio di rete.  
  
 Per impostazione predefinita, ODBC traccia ora Usa la modalità per utente. Se sei un amministratore locale, tuttavia, è ancora possibile abilitare la traccia a livello di computer con l'amministratore dell'origine dati ODBC.  
  
 Per configurare la modalità di analisi ODBC:  
  
1.  Se necessario, accedere usando un account con appartenenza al gruppo degli amministratori locali.  
  
2.  Strumenti di amministrazione aprire Amministrazione origine dati ODBC.  
  
3.  Scegliere il **traccia** scheda.  
  
4.  Configurare la modalità di analisi tramite il **traccia a livello di computer per tutte le identità utente** casella di controllo:  
  
5.  Per abilitare la traccia a livello di computer, selezionare la casella di controllo.  
  
6.  Per tornare alla traccia di ogni utente, deselezionare la casella di controllo.  
  
7.  Fare clic su **Applica**.  
  
> [!NOTE]  
>  Se è stata ancora avviata la traccia in una modalità, è necessario arrestare la traccia e passare in altra modalità per la modalità di modifica completata.  
  
> [!IMPORTANT]  
>  Traccia a livello di computer deve essere abilitata solo quando necessario; in caso contrario, è opportuno lasciare disattivato.  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer traccia  
  
> [!IMPORTANT]  
>  Supporto per Visual Studio Analyzer è stata rimossa a partire da Windows 8 (Visual Studio Analyzer è stato incluso solo nelle versioni precedenti di Visual Studio). Per una meccanismo di risoluzione dei problemi in alternativa, usare l'analisi BID.  
  
 Visual Studio® analizzatore traccia offre prestazioni e le informazioni di debug sul livello di ODBC. Tutti gli eventi in uscita verranno generati l'interfaccia di livello superiore di presentare accurata un'immagine minor relativa a tempo impiegato per i componenti ODBC. Visual Studio Analyzer traccia richiede qualsiasi origine evento per registrare quando viene configurato l'origine. Per altre informazioni su questo tipo di traccia, vedere la documentazione di Visual Studio.
