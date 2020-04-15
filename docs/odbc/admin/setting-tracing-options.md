---
title: Impostazione delle opzioni di tracciamento Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21bee5d903459423a134389e62db844f5f63c9c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307198"
---
# <a name="setting-tracing-options"></a>Impostazione delle opzioni di traccia
La scheda **Traccia** della finestra di dialogo **Amministratore origine dati ODBC** consente di configurare la modalità di traccia delle chiamate alle funzioni ODBC.  
  
## <a name="how-tracing-works"></a>Funzionamento della traccia  
 Quando si avvia la traccia dalla scheda **Traccia** , Gestione Driver registrerà tutte le chiamate di funzione ODBC per tutte le applicazioni eseguite successivamente. Le chiamate di funzione ODBC da applicazioni in esecuzione prima dell'avvio della traccia non vengono registrate. Le chiamate di funzione ODBC vengono registrate in un file di registro specificato.  
  
 La traccia si interrompe solo dopo aver fatto clic su **Interrompi traccia ora**. Tenere presente che mentre la traccia è attivata, il file di registro continua ad aumentare e che ciò influisce sulle prestazioni di tutte le applicazioni ODBC.  
  
 Per ulteriori informazioni sull'analisi, vedere [Traccia](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Modifiche nella traccia ODBCChanges in ODBC tracing  
 Prima di MDAC 2.7 SP2, la traccia ODBC era consentita solo a livello di computer, in cui la traccia acquisisce i dettagli esposti su tutte le applicazioni ODBC in esecuzione con qualsiasi identità. Ciò includeva la traccia per le attività correlate a ODBC che potrebbero verificarsi per i processi creati o eseguiti per conto di altri account utente locali e delle entità di sicurezza incorporate, ad esempio il servizio locale e il servizio di rete.  
  
 Per impostazione predefinita, la traccia ODBC ora utilizza la modalità per utente. Se si è un amministratore locale, tuttavia, è comunque possibile abilitare la traccia a livello di computer utilizzando L'Amministratore origine dati ODBC.  
  
 Per configurare la modalità di traccia ODBC:  
  
1.  Se necessario, accedere utilizzando un account che appartenenza al gruppo Administrators locale.  
  
2.  Da Strumenti di amministrazione aprire Amministrazione origine dati ODBC.  
  
3.  Fare clic sulla scheda **Traccia.**  
  
4.  Configurare la modalità di traccia utilizzando la casella di controllo Traccia a livello di computer **per tutte le identità utente:**  
  
5.  Per abilitare la traccia a livello di computer, selezionare la casella di controllo.  
  
6.  Per tornare alla traccia per utente, deselezionare la casella di controllo.  
  
7.  Fare clic su **Applica**.  
  
> [!NOTE]  
>  Se la traccia è già stata avviata in una modalità, è necessario interrompere la traccia e passare all'altra modalità affinché la modalità venga modificata correttamente.  
  
> [!IMPORTANT]  
>  La traccia a livello di macchina deve essere abilitata solo quando è necessaria; in caso contrario, deve essere lasciato disattivato.  
  
## <a name="visual-studio-analyzer-tracing"></a>Traccia di Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  Il supporto per Visual Studio Analyzer è stato rimosso a partire da Windows 8 (Visual Studio Analyzer è stato incluso solo nelle versioni precedenti di Visual Studio.). Per un meccanismo di risoluzione dei problemi alternativo, usare la traccia BID.  
  
 Visual Studio® Analyzer Tracing fornisce informazioni sulle prestazioni e sul debug del livello ODBC. Tutti gli eventi in uscita verranno generati nell'interfaccia di primo livello per presentare un'immagine il più accurata possibile relativa al tempo trascorso nei componenti ODBC. Visual Studio Analyzer Tracing richiede qualsiasi origine eventi per la registrazione quando l'origine è impostata. Per altre informazioni su questo tipo di traccia, vedere la documentazione di Visual Studio.For more information about this kind of tracing, see the Visual Studio documentation.
