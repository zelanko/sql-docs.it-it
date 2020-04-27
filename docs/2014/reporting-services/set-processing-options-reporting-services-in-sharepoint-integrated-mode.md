---
title: Impostare le opzioni di elaborazione (Reporting Services in modalità integrata SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- snapshots [Reporting Services], creating
ms.assetid: 453b19a1-739a-4b67-aeea-2069b52204e1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5d64015e0b1756033f3a3a0b7caf90262d7d43f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101341"
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>Impostare le opzioni di elaborazione (Reporting Services in modalità integrata SharePoint)
  È possibile impostare le opzioni di elaborazione di un report [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per determinare il momento in cui deve avvenire l'elaborazione dei dati. È inoltre possibile impostare un valore di timeout per l'elaborazione del report e opzioni che determinano se attivare o meno la cronologia del report per il report corrente.  
  
-   È possibile eseguire un report come snapshot per evitare che venga eseguito in momenti indesiderati, ad esempio durante un backup pianificato. Uno snapshot di report viene in genere creato e in seguito aggiornato in base a una pianificazione, consentendo all'utente di determinare esattamente quando verrà eseguita l'elaborazione del report e dei dati. Se un report si basa su query la cui esecuzione richiede molto tempo oppure su query che utilizzano dati di un'origine dati che non si desidera venga utilizzata in determinati orari, è consigliabile eseguire il report come snapshot.  
  
-   Nel server di report è possibile memorizzare nella cache una copia di un report già elaborato, che verrà utilizzata quando un utente apre il report. La memorizzazione nella cache è una tecnica per il miglioramento delle prestazioni che consente di ridurre il tempo necessario per recuperare i report di grandi dimensioni o che vengono aperti di frequente.  
  
-   La cronologia di un report è costituita dalla raccolta delle copie di un report eseguite in precedenza. È pertanto possibile usare la cronologia di un report per mantenere una registrazione dei diversi risultati dell'esecuzione del report ottenuti durante un determinato periodo di tempo. Non è consigliabile usare la cronologia del report per i report contenenti informazioni riservate e personali. Per questo motivo, la cronologia del report può essere creata solo per i report che eseguono query su origini dati che utilizzano un unico set di credenziali (credenziali archiviate o credenziali utilizzate per l'esecuzione automatica dei report), che sono disponibili a tutti gli utenti che eseguono il report.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] con SharePoint utilizza le caratteristiche di gestione contenuto di estrazione e archiviazione di SharePoint per salvare gli aggiornamenti nei tipi di contenuto di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , tra cui la creazione di snapshot dei report. Pertanto se è stato abilitato il controllo delle versioni su una raccolta documenti, verrà visualizzata la versione del report aggiornata quando viene creato un nuovo snapshot di cronologia del report. Si tratta di un effetto collaterale dell'aggiornamento di snapshot. L'aggiornamento di uno snapshot determina la modifica della proprietà LastExecution del report con una conseguente modifica della versione del report.  
  
-   È possibile specificare valori di timeout per limitare l'utilizzo delle risorse del sistema.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Modalità SharePoint|  
  
 **Contenuto dell'argomento:**  
  
-   [Per impostare le opzioni relative all'aggiornamento dei dati](#bkmk_set_data_refresh)  
  
-   [Per impostare le opzioni relative alla memorizzazione dei report nella cache](#bkmk_set_report_caching)  
  
-   [Per impostare i valori del timeout di elaborazione](#bkmk_set_processing)  
  
-   [Per impostare limiti e opzioni relativi alla cronologia del report](#bkmk_set_report_history)  
  
-   [Impostare il timeout del database](#bkmk_set_database_timeout)  
  
##  <a name="to-set-data-refresh-options"></a><a name="bkmk_set_data_refresh"></a>Per impostare le opzioni di aggiornamento dati  
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  In **Opzioni aggiornamento dati**fare clic su **Usa dati snapshot**. Se viene visualizzato il messaggio "Impossibile eseguire questo report da uno snapshot perché non sono disponibili credenziali archiviate per una o più origini dati", significa che il report non è configurato per l'esecuzione automatica e, prima di impostare questa opzione, sarà necessario modificare le origini dati in modo che utilizzino credenziali archiviate.  
  
4.  In **Opzioni snapshot dati**selezionare **Pianifica elaborazione dati**.  
  
5.  Se si desidera usare una pianificazione condivisa esistente, fare clic su **In base a una pianificazione condivisa** . In caso contrario, fare clic su **In base a una pianificazione personalizzata**, quindi su **Configura**.  
  
6.  Selezionare la frequenza, la pianificazione, nonché le date di inizio e di fine e quindi fare clic su **OK**.  
  
7.  Se si desidera creare immediatamente i dati dello snapshot da usare con il report, senza attendere l'elaborazione pianificata dei dati, in **Opzioni snapshot dati**selezionare **Crea o aggiorna lo snapshot al salvataggio della pagina** .  
  
##  <a name="to-set-report-caching-options"></a><a name="bkmk_set_report_caching"></a>Per impostare le opzioni di memorizzazione nella cache del report  
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  In **Opzioni aggiornamento dati**fare clic su **Usa dati nella cache**. Se viene visualizzato il messaggio "Impossibile memorizzare il report nella cache perché le credenziali di una o più origini dati non sono archiviate", significa che il report non è configurato per l'esecuzione automatica e, prima di impostare questa opzione, sarà necessario modificare le origini dati in modo che utilizzino credenziali archiviate.  
  
4.  In **Opzioni cache**specificare la modalità di scadenza della cache:  
  
    -   Immettere il numero di minuti dopo il quale la cache scadrà.  
  
    -   Utilizzare una pianificazione per cancellare la cache a orari specifici.  
  
    -   Creare una pianificazione personalizzata per cancellare la cache all'orario desiderato.  
  
##  <a name="to-set-processing-time-out-values"></a><a name="bkmk_set_processing"></a>Per impostare i valori di timeout di elaborazione  
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  Se si desidera usare il valore specificato a livello del server di report, selezionare **Usa impostazione predefinita sito**in **Timeout elaborazione** . Se invece si desidera sostituire il valore in questione e non impostare alcun timeout o un valore di timeout diverso, selezionare **Nessun timeout per l'elaborazione del report** o **Limite elaborazione report (in secondi)** .  
  
##  <a name="to-set-report-history-options-and-limits"></a><a name="bkmk_set_report_history"></a>Per impostare limiti e opzioni per la cronologia dei report  
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  In **Opzioni snapshot cronologia**specificare la modalità e il momento dell'esecuzione e del salvataggio dell'elaborazione dei dati.  
  
4.  Se si desidera usare il valore specificato a livello del server di report, selezionare **Usa impostazione predefinita sito**in **Limiti snapshot cronologia** . In caso contrario, selezionare **Numero di snapshot illimitato** oppure **Numero massimo di snapshot** e specificare un valore personalizzato.  
  
##  <a name="set-database-timeout"></a><a name="bkmk_set_database_timeout"></a>Imposta timeout database  
  
1.  Usare Windows PowerShell per impostare il timeout del database di un server di report di SharePoint. Per altre informazioni, vedere la sezione "Ottenere e impostare le proprietà del database di un'applicazione Reporting Service" dell'argomento [Cmdlet di PowerShell per la modalità SharePoint di Reporting Services](../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Impostare le proprietà di elaborazione dei report](report-server/set-report-processing-properties.md)   
 [Memorizzazione dei report nella cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Impostazione dei valori di timeout per l'elaborazione di report e di set di dati condivisi &#40;SSRS&#41;](report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
  
  
