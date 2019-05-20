---
title: Impostare le opzioni di elaborazione (Reporting Services in modalità integrata SharePoint)| Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 986ae6e89727b0cef59e4d6b3bf7e5d92bd5342b
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580544"
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>Impostare le opzioni di elaborazione (Reporting Services in modalità integrata SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  È possibile impostare le opzioni di elaborazione di un report Reporting Services per determinare il momento in cui deve avvenire l'elaborazione dei dati. È inoltre possibile impostare un valore di timeout per l'elaborazione del report e opzioni che determinano se attivare o meno la cronologia del report per il report corrente.  
  
-   È possibile eseguire un report come snapshot per evitare che venga eseguito in momenti indesiderati, ad esempio durante un backup pianificato. Uno snapshot di report viene in genere creato e in seguito aggiornato in base a una pianificazione, consentendo all'utente di determinare esattamente quando verrà eseguita l'elaborazione del report e dei dati. Se un report si basa su query la cui esecuzione richiede molto tempo oppure su query che utilizzano dati di un'origine dati che non si desidera venga utilizzata in determinati orari, è consigliabile eseguire il report come snapshot.  
  
-   Nel server di report è possibile memorizzare nella cache una copia di un report già elaborato, che verrà utilizzata quando un utente apre il report. La memorizzazione nella cache è una tecnica per il miglioramento delle prestazioni che consente di ridurre il tempo necessario per recuperare i report di grandi dimensioni o che vengono aperti di frequente.  
  
-   La cronologia di un report è costituita dalla raccolta delle copie di un report eseguite in precedenza. È pertanto possibile usare la cronologia di un report per mantenere una registrazione dei diversi risultati dell'esecuzione del report ottenuti durante un determinato periodo di tempo. Non è consigliabile usare la cronologia del report per i report contenenti informazioni riservate e personali. Per questo motivo, la cronologia del report può essere creata solo per i report che eseguono query su origini dati che utilizzano un unico set di credenziali (credenziali archiviate o credenziali utilizzate per l'esecuzione automatica dei report), che sono disponibili a tutti gli utenti che eseguono il report.  

    L'integrazione di Reporting Services con SharePoint usa le caratteristiche di gestione contenuto di estrazione e archiviazione di SharePoint per salvare gli aggiornamenti nei tipi di contenuto di Reporting Services, tra cui la creazione di snapshot dei report. Pertanto se è stato abilitato il controllo delle versioni su una raccolta documenti, verrà visualizzata la versione del report aggiornata quando viene creato un nuovo snapshot di cronologia del report. Si tratta di un effetto collaterale dell'aggiornamento di snapshot. L'aggiornamento di uno snapshot determina la modifica della proprietà LastExecution del report con una conseguente modifica della versione del report.  

-   È possibile specificare valori di timeout per limitare l'utilizzo delle risorse del sistema.  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

## <a name="set-data-refresh-options"></a>Impostazione delle opzioni relative all'aggiornamento dei dati
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  In **Opzioni aggiornamento dati**fare clic su **Usa dati snapshot**. Se viene visualizzato il messaggio "Impossibile eseguire questo report da uno snapshot perché non sono disponibili credenziali archiviate per una o più origini dati", significa che il report non è configurato per l'esecuzione automatica e, prima di impostare questa opzione, sarà necessario modificare le origini dati in modo che utilizzino credenziali archiviate.  
  
4.  In **Opzioni snapshot dati**selezionare **Pianifica elaborazione dati**.  
  
5.  Se si desidera usare una pianificazione condivisa esistente, fare clic su **In base a una pianificazione condivisa** . In caso contrario, fare clic su **In base a una pianificazione personalizzata**, quindi su **Configura**.  
  
6.  Selezionare la frequenza, la pianificazione, nonché le date di inizio e di fine e quindi fare clic su **OK**.  
  
7.  Se si desidera creare immediatamente i dati dello snapshot da usare con il report, senza attendere l'elaborazione pianificata dei dati, in **Opzioni snapshot dati**selezionare **Crea o aggiorna lo snapshot al salvataggio della pagina** .  
  
## <a name="set-report-caching-options"></a>Impostazione delle opzioni relative alla memorizzazione dei report nella cache
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  In **Opzioni aggiornamento dati**fare clic su **Usa dati nella cache**. Se viene visualizzato il messaggio "Impossibile memorizzare il report nella cache perché le credenziali di una o più origini dati non sono archiviate", significa che il report non è configurato per l'esecuzione automatica e, prima di impostare questa opzione, sarà necessario modificare le origini dati in modo che utilizzino credenziali archiviate.  
  
4.  In **Opzioni cache**specificare la modalità di scadenza della cache:  
  
    -   Immettere il numero di minuti dopo il quale la cache scadrà.  
  
    -   Utilizzare una pianificazione per cancellare la cache a orari specifici.  
  
    -   Creare una pianificazione personalizzata per cancellare la cache all'orario desiderato.  
  
## <a name="set-processing-time-out-values"></a>Impostazione dei valori del timeout di elaborazione
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  Se si desidera usare il valore specificato a livello del server di report, selezionare **Usa impostazione predefinita sito**in **Timeout elaborazione** . Se invece si desidera sostituire il valore in questione e non impostare alcun timeout o un valore di timeout diverso, selezionare **Nessun timeout per l'elaborazione del report** o **Limite elaborazione report (in secondi)** .  
  
## <a name="set-report-history-options-and-limits"></a>Impostazione dei limiti e delle opzioni relative alla cronologia di un report
  
1.  Selezionare un report nella raccolta.  
  
2.  Fare clic sulla freccia in giù e selezionare **Gestisci opzioni elaborazione**.  
  
3.  In **Opzioni snapshot cronologia**specificare la modalità e il momento dell'esecuzione e del salvataggio dell'elaborazione dei dati.  
  
4.  Se si desidera usare il valore specificato a livello del server di report, selezionare **Usa impostazione predefinita sito**in **Limiti snapshot cronologia** . In caso contrario, selezionare **Numero di snapshot illimitato** oppure **Numero massimo di snapshot** e specificare un valore personalizzato.  
  
## <a name="set-database-timeout"></a>Impostare il timeout del database
  
*  Usare Windows PowerShell per impostare il timeout del database di un server di report di SharePoint. Per altre informazioni, vedere la sezione "Ottenere e impostare le proprietà del database di un'applicazione Reporting Service" dell'argomento [Cmdlet di PowerShell per la modalità SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="next-steps"></a>Passaggi successivi

 [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Memorizzazione dei report nella cache](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [Impostazione dei valori di timeout per l'elaborazione di report e di set di dati condivisi](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
