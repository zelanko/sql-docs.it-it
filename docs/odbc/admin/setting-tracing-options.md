---
title: Impostazione delle opzioni di traccia | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901627"
---
# <a name="setting-tracing-options"></a>Impostazione delle opzioni di traccia
La scheda **traccia** della finestra di dialogo **Amministrazione origine dati ODBC** consente di configurare il modo in cui vengono tracciate le chiamate alle funzioni ODBC.  
  
## <a name="how-tracing-works"></a>Funzionamento della traccia  
 Quando si avvia la traccia dalla scheda **traccia** , gestione driver registrerà tutte le chiamate di funzione ODBC per tutte le applicazioni eseguite successivamente. Le chiamate di funzione ODBC da applicazioni che vengono eseguite prima dell'avvio della traccia non vengono registrate. Le chiamate di funzione ODBC vengono registrate in un file di log specificato dall'utente.  
  
 La traccia viene arrestata solo dopo aver fatto clic su **Interrompi traccia ora**. Tenere presente che, mentre la traccia è attiva, il file di registro continua ad aumentare e ciò influiscono sulle prestazioni di tutte le applicazioni ODBC.  
  
 Per ulteriori informazioni sulla traccia, vedere la pagina relativa alla [traccia](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Modifiche alla traccia ODBC  
 Prima di MDAC 2,7 SP2, la traccia ODBC era consentita solo a livello di computer, in cui la traccia acquisisce informazioni dettagliate su tutte le applicazioni ODBC eseguite in qualsiasi identità. Inclusa la traccia per le attività correlate a ODBC che possono verificarsi per i processi creati o eseguiti per conto di altri account utente locali e per entità di sicurezza predefinite, ad esempio servizio locale e servizio di rete.  
  
 Per impostazione predefinita, la traccia ODBC ora usa la modalità per utente. Tuttavia, se si è un amministratore locale, è comunque possibile abilitare la traccia a livello di computer tramite Amministrazione origine dati ODBC.  
  
 Per configurare la modalità di traccia ODBC:  
  
1.  Se necessario, accedere utilizzando un account che dispone dell'appartenenza al gruppo Administrators locale.  
  
2.  In strumenti di amministrazione aprire Amministrazione origine dati ODBC.  
  
3.  Fare clic sulla scheda **traccia** .  
  
4.  Configurare la modalità di traccia tramite la casella **di controllo traccia a livello di computer per tutte le identità utente** :  
  
5.  Per abilitare la traccia a livello di computer, selezionare la casella di controllo.  
  
6.  Per tornare alla traccia per utente, deselezionare la casella di controllo.  
  
7.  Fare clic su **Apply**.  
  
> [!NOTE]  
>  Se la traccia è già stata avviata in una modalità, è necessario arrestare la traccia e passare all'altra modalità per la modifica corretta della modalità.  
  
> [!IMPORTANT]  
>  La traccia a livello di computer deve essere abilitata solo quando è necessario; in caso contrario, deve essere lasciato disattivato.  
  
## <a name="visual-studio-analyzer-tracing"></a>Traccia Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  Il supporto per Visual Studio Analyzer è stato rimosso a partire da Windows 8 (Visual Studio Analyzer era incluso solo nelle versioni precedenti di Visual Studio). Per un meccanismo alternativo di risoluzione dei problemi, usare la traccia delle offerte.  
  
 La traccia di Visual Studio® Analyzer fornisce informazioni sulle prestazioni e sul debug del livello ODBC. Tutti gli eventi in uscita verranno attivati nell'interfaccia di livello superiore per presentare un'immagine più accurata possibile riguardo al tempo impiegato nei componenti ODBC. Per eseguire la traccia Visual Studio Analyzer è necessario che tutte le origini eventi siano registrate quando l'origine è configurata. Per ulteriori informazioni su questo tipo di traccia, vedere la documentazione di Visual Studio.
