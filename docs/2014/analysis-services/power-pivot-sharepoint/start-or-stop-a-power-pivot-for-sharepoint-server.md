---
title: Avviare o arrestare un server di PowerPivot per SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e38e6366-9f20-4db0-b2a8-da7d5adf00eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 312afc0336405ca530f731ad4fec55a26a960e7a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071053"
---
# <a name="start-or-stop-a-powerpivot-for-sharepoint-server"></a>Avviare o arrestare un server PowerPivot per SharePoint
  Servizio di sistema PowerPivot e un' [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] istanza operano insieme nello stesso server applicazioni locale per supportare l'elaborazione di dati e richieste coordinata in una farm di SharePoint.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Dipendenze del servizio](#dependencies)  
  
 [Avviare o arrestare i servizi](#startstop)  
  
 [Effetti dell'arresto di un server PowerPivot](#effects)  
  
##  <a name="service-dependencies"></a><a name="dependencies"></a>Dipendenze del servizio  
 Il servizio di sistema PowerPivot presenta una dipendenza sull'istanza del server Analysis Services locale installata con il servizio nello stesso server fisico. Se si arresta il servizio di sistema PowerPivot, è necessario arrestare manualmente l'istanza del server Analysis Services locale. Se un servizio viene eseguito senza l'altro, si verificheranno errori di allocazione richieste per l'elaborazione dei dati PowerPivot.  
  
 Il server Analysis Services deve essere eseguito in modalità autonoma durante la diagnostica o la risoluzione di un problema. In tutti gli altri casi, il server richiede che il servizio di sistema PowerPivot venga eseguito in locale nello stesso server.  
  
##  <a name="start-or-stop-the-services"></a><a name="startstop"></a>Avviare o arrestare i servizi  
 Utilizzare sempre Amministrazione centrale per avviare o arrestare il servizio di sistema PowerPivot o l'istanza del server Analysis Services. Amministrazione centrale consente di avviare o arrestare insieme i servizi dalla stessa pagina. In Amministrazione centrale viene inoltre usato un processo timer denominato **Uno o più servizi sono stati avviati o arrestati** per riavviare servizi che dovrebbero essere in esecuzione. Se si arresta Analysis Services o il servizio di sistema PowerPivot utilizzando uno strumento non SharePoint, i servizi verranno riavviati durante l'esecuzione del processo timer.  
  
 L'avvio e l'arresto dei servizi sono azioni che vengono applicate a un'istanza del servizio fisico. Se nella farm sono presenti più server PowerPivot per SharePoint, gli altri server della farm continueranno ad accettare le richieste di dati PowerPivot.  
  
 Non è possibile avviare o arrestare simultaneamente tutti i servizi fisici nella farm. È necessario selezionare ciascun server e avviare o arrestare un determinato servizio.  
  
 Non è possibile avviare, mettere in pausa o arrestare un servizio di sistema PowerPivot per un'applicazione Web specifica, ma è possibile rimuovere un servizio dall'elenco predefinito di connessioni per renderlo non disponibile. Per ulteriori informazioni, vedere [connettere un'applicazione del servizio PowerPivot a un'applicazione Web di SharePoint in Amministrazione centrale](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
1.  In **Impostazioni di sistema**di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
2.  In Server, nella parte superiore della pagina, fare clic sulla freccia giù, quindi scegliere **Cambia server**.  
  
3.  Selezionare il server SharePoint contenente il servizio di sistema PowerPivot o l'istanza di [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] che si desidera avviare o arrestare.  
  
4.  Selezionare il servizio, quindi fare clic sull'azione. Ricordarsi di avviare o arrestare i servizi come coppia. Se si avvia o arresta il servizio di sistema PowerPivot, assicurarsi di avviare o arrestare anche l'istanza del server Analysis Services in esecuzione nello stesso computer.  
  
##  <a name="effects-of-stopping-a-powerpivot-server"></a><a name="effects"></a>Effetti dell'arresto di un server PowerPivot  
 Nella tabella seguente vengono descritti gli effetti dell'arresto del servizio di sistema PowerPivot e del servizio Analysis Services in un server SharePoint.  
  
|Effetto su|Descrizione|  
|---------------|-----------------|  
|Query esistenti|Le query in esecuzione in un server Analysis Services verranno arrestate immediatamente. L'utente otterrà un errore di dati non trovati o di connessione all'origine dati non trovata.|  
|Processi di aggiornamento dati esistenti in fase di elaborazione|I processi in esecuzione nel server Analysis Services corrente verranno arrestati immediatamente. L'aggiornamento dati avrà esito negativo e un errore verrà registrato nella cronologia dell'aggiornamento dati.<br /><br /> È possibile visualizzare lo stato dei processi correnti prima di arrestare il servizio tramite la pagina Controlla stato processo in Amministrazione centrale SharePoint.<br /><br /> Anche se è possibile conoscere quali processi sono in fase di elaborazione, non vi è modo di visualizzare la coda per verificare se stanno per essere avviati altri processi.|  
|Richieste di aggiornamento dati esistenti nella coda|Le richieste di aggiornamento dati pianificate rimarranno nella coda di elaborazione per un ciclo completo della pianificazione, ovvero resteranno nella coda fino all'ora di avvio successiva. Se il servizio di sistema PowerPivot non viene riavviato entro tale ora, la richiesta di aggiornamento dati verrà eliminata e verrà registrato un errore.|  
|Nuove richieste di query o aggiornamento dati|Se si arresta l'unico server PowerPivot per SharePoint nella farm, non verranno gestite nuove richieste di dati PowerPivot e una richiesta di dati causerà un errore di dati non trovati.<br /><br /> Se si dispone di più server PowerPivot per SharePoint, la richiesta verrà inviata a uno dei server disponibili.|  
|Dati sull'utilizzo|I dati sull'utilizzo non verranno raccolti durante l'arresto dei servizi.|  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare gli account del servizio PowerPivot](configure-power-pivot-service-accounts.md)  
  
  
