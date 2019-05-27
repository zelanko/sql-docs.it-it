---
title: Rappresentazione (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81e8f9ae90db3c7613ccb99039d70d9a28c5a113
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067056"
---
# <a name="impersonation-ssas-tabular"></a>Rappresentazione (SSAS tabulare)
  In questo argomento vengono fornite agli autori di modelli tabulari informazioni sulla modalità di utilizzo delle credenziali di accesso da parte di Analysis Services in caso di connessione a un'origine dati per importare ed elaborare (aggiornare) i dati.  
  
 In questo articolo sono contenute le sezioni seguenti:  
  
-   [Vantaggi](#bkmk_how_imper)  
  
-   [Opzioni](#bkmk_imp_info_options)  
  
-   [Sicurezza](#bkmk_impers_sec)  
  
-   [Rappresentazione in caso di importazione di un modello](#bkmk_imp_newmodel)  
  
-   [Configurazione della rappresentazione](#bkmk_conf_imp_info)  
  
##  <a name="bkmk_how_imper"></a> Vantaggi  
 La*rappresentazione* è la capacità di un'applicazione server, ad esempio Analysis Services, di assumere l'identità di un'applicazione client. Analysis Services viene eseguito utilizzando un account del servizio, tuttavia, quando tramite il server viene stabilita una connessione a un'origine dati, viene utilizzata la rappresentazione in modo che sia possibile eseguire controlli di accesso per l'importazione e l'elaborazione dei dati.  
  
 Le credenziali utilizzate per la rappresentazione sono diverse da quelle dell'utente attualmente connesso. Le credenziali dell'utente che ha effettuato l'accesso vengono utilizzate per particolari operazioni lato client in caso di creazione di un modello.  
  
 È importante comprendere come le credenziali di rappresentazione vengono specificate e protette nonché la differenza tra i contesti in cui le credenziali dell'utente connesso corrente e quando si utilizzano altre credenziali.  
  
 **Informazioni sulle credenziali lato server**  
  
 In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]le credenziali vengono specificate per ogni origine dati tramite la pagina **Impostazioni di rappresentazione** nell'Importazione guidata tabella o modificando una connessione all'origine dati esistente nella finestra di dialogo **Connessioni esistenti** .  
  
 Quando i dati vengono importati o elaborati, le credenziali specificate nella pagina **Impostazioni di rappresentazione** vengono usate per la connessione all'origine dati e per il recupero dei dati. Si tratta di un'operazione *lato server* in esecuzione nel contesto di un'applicazione client in quanto, tramite il server Analysis Services in cui è ospitato il database dell'area di lavoro, viene eseguita la connessione all'origine dati e il recupero dei dati.  
  
 Quando si distribuisce un modello in un server Analysis Services, se il database dell'area di lavoro è in memoria durante la distribuzione del modello, le credenziali vengono passate al server Analysis Services in cui viene distribuito il modello. In nessuna circostanza si stratta di credenziali utente archiviate su disco.  
  
 Quando tramite un modello distribuito vengono elaborati i dati di un'origine dati, le credenziali di rappresentazione, persistenti nel database in memoria, vengono utilizzate per la connessione all'origine dati e per il recupero dei dati. Poiché questo processo viene gestito dal server Analysis Services tramite cui viene gestito il database modello, si tratta nuovamente di un'operazione lato server.  
  
 **Informazioni sulle credenziali lato client**  
  
 In caso di creazione di un nuovo modello o di aggiunta di un'origine dati a un modello esistente, viene utilizzata l'Importazione guidata tabella per la connessione a un'origine dati e per la selezione di tabelle e viste da importare nel modello. Nella pagina **Selezione tabelle e viste** dell'Importazione guidata tabella è possibile usare la funzionalità **Visualizza anteprima e applica filtro** per visualizzare un esempio (limitato a 50 righe) dei dati che verranno importati. Inoltre, è possibile specificare filtri per escludere dati che non devono essere inclusi nel modello.  
  
 Analogamente, per modelli esistenti che sono già stati creati, è possibile usare la finestra di dialogo **Modifica proprietà tabella** per visualizzare in anteprima e filtrare i dati importati in una tabella. Per le funzionalità di anteprima e filtro viene usata la stessa funzionalità **Visualizza anteprima e applica filtro** nella pagina **Selezione tabelle e viste** dell'Importazione guidata tabella.  
  
 La funzionalità **Visualizza anteprima e applica filtro** e le finestre di dialogo **Proprietà tabella** e **Gestione partizioni** sono operazioni *lato client* in-process. Vale a dire che quanto effettuato durante questa operazione differisce dalla modalità con cui viene eseguita la connessione all'origine dati e con cui viene eseguito il recupero dei dati dall'origine dati, ovvero un'operazione lato server. Le credenziali utilizzate per l'anteprima e il filtro dei dati sono quelle dell'utente attualmente connesso. Operazioni lato client usano sempre le credenziali di Windows dell'utente corrente per la connessione all'origine dati.  
  
 Questa separazione di credenziali usate durante le operazioni lato server e lato client può determinare una mancata corrispondenza tra gli elementi visualizzati dall'utente tramite la funzionalità **Visualizza anteprima e applica filtro** o la finestra di dialogo **Proprietà tabella** (operazioni lato client) e i dati che verranno recuperati durante un'importazione o un'elaborazione (operazione lato server). Se le credenziali dell'utente attualmente connesso e quelle di rappresentazione specificate sono diverse, i dati visualizzati nella funzionalità **Visualizza anteprima e applica filtro** o nella finestra di dialogo **Proprietà tabella** e i dati recuperati durante un'importazione o un'elaborazione possono differire a seconda delle credenziali richieste dall'origine dati.  
  
> [!IMPORTANT]  
>  Durante la creazione di un modello, assicurarsi che le credenziali dell'utente attualmente connesso e quelle specificate per la rappresentazione dispongano di diritti sufficienti per il recupero dei dati dall'origine dati.  
  
##  <a name="bkmk_imp_info_options"></a> Opzioni  
 Quando si configura la rappresentazione o si modificano proprietà per una connessione all'origine dati esistente in Analysis Services, è possibile specificare una delle opzioni seguenti:  
  
|Opzione|ImpersonationMode<sup>1</sup>|Descrizione|  
|------------|-----------------------------------|-----------------|  
|**Nome utente di Windows specifico e la password** <sup>2</sup>|ImpersonateWindowsUserAccount|Questa opzione consente di specificare che nel modello viene utilizzato un account utente di Windows per importare o elaborare dati dall'origine dati. Il dominio e il nome dell'account utente nel formato seguente:**\<nome di dominio >\\< nome dell'account utente\>**. Si tratta dell'opzione predefinita per la creazione di un nuovo modello tramite l'Importazione guidata tabella.|  
|**Account servizio**|ImpersonateServiceAccount|Questa opzione consente di specificare che nel modello vengono utilizzate le credenziali di sicurezza associate all'istanza del servizio Analysis Services tramite cui viene gestito il modello.|  
  
 <sup>1</sup>ImpersonationMode consente di specificare il valore per il [elemento DataSourceImpersonationInfo &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) proprietà dell'origine dati.  
  
 <sup>2</sup>quando si utilizza questa opzione, se il database dell'area di lavoro viene rimosso dalla memoria, a causa di un riavvio o il **memorizzazione area di lavoro** è impostata su **Scarica dalla memoria** o  **Elimina dall'area di lavoro**, e il progetto di modello è chiuso, nella sessione successiva, se si tenta di elaborare i dati della tabella, verrà richiesto di immettere le credenziali per ogni origine dati. Analogamente, se un database modello distribuito viene rimosso dalla memoria, verranno richieste le credenziali per ogni origine dati.  
  
##  <a name="bkmk_impers_sec"></a> Sicurezza  
 Le credenziali utilizzate con la rappresentazione sono salvate in modo permanente in memoria dal motore di analisi in memoria xVelocity (VertiPaq™) associato al server Analysis Services tramite cui viene gestito il database dell'area di lavoro o un modello distribuito.  In nessuna circostanza si tratta di credenziali scritte su disco. Se il database dell'area di lavoro non è in memoria quando il modello viene distribuito, all'utente verrà richiesto di immettere le credenziali utilizzate per la connessione all'origine dati e il recupero dei dati.  
  
> [!NOTE]  
>  Si consiglia di specificare un account utente di Windows e una password per le credenziali di rappresentazione. È possibile configurare un account utente di Windows per utilizzare privilegi minimi necessari per la connessione e la lettura dei dati dall'origine dati.  
  
##  <a name="bkmk_imp_newmodel"></a> Rappresentazione in caso di importazione di un modello  
 A differenza dei modelli tabulari in cui è possibile utilizzare molte modalità di rappresentazione diverse per supportare la raccolta dati out-of-process, in PowerPivot viene utilizzata un'unica modalità, ovvero ImpersonateCurrentUser. Poiché PowerPivot viene eseguito sempre in-process, la connessione alle origini dati viene stabilita utilizzando le credenziali dell'utente attualmente connesso. Con i modelli tabulari, le credenziali dell'utente attualmente connesso vengono usate solo con la funzionalità **Visualizza anteprima e applica filtro** nell'Importazione guidata tabella e in caso di visualizzazione di **Proprietà tabella**. Le credenziali di rappresentazione vengono utilizzate durante l'importazione o l'elaborazione di dati nel database dell'area di lavoro o in un modello distribuito.  
  
 In caso di creazione di un nuovo modello importando una cartella di lavoro di PowerPivot esistente, per impostazione predefinita, in Progettazione modelli verrà configurata la rappresentazione per utilizzare l'account del servizio (ImpersonateServiceAccount). Si consiglia di impostare le credenziali di rappresentazione nei modelli importati da PowerPivot su un account utente di Windows. Dopo aver importato la cartella di lavoro di PowerPivot e creare il nuovo modello in Progettazione modelli, è possibile modificare le credenziali usando il **connessioni esistenti** finestra di dialogo.  
  
 In caso di creazione di un nuovo modello importando da un modello esistente in un server Analysis Services, le credenziali di rappresentazione vengono passate dal database modello esistente al nuovo database dell'area di lavoro del modello. Se necessario, è possibile modificare le credenziali nel nuovo modello tramite la finestra di dialogo **Connessioni esistenti** .  
  
##  <a name="bkmk_conf_imp_info"></a> Configurazione della rappresentazione  
 La posizione e il contesto di un modello esistente consentiranno di determinare la modalità di configurazione delle informazioni sulla rappresentazione. Per la creazione di modelli in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], è possibile configurare le informazioni sulla rappresentazione nella pagina **Impostazioni di rappresentazione** dell'Importazione guidata tabella o modificando una connessione all'origine dati nella finestra di dialogo **Connessioni esistenti** . Per visualizzare le connessioni esistenti, nel menu [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]Modello **di** fare clic su **Connessioni esistenti**.  
  
 Per i modelli distribuiti in un server Analysis Services, è possibile configurare le informazioni sulla rappresentazione facendo clic sui puntini di sospensione (...) del **rappresentazione origine dati** proprietà nel **le proprietà del Database** della finestra di dialogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery &#40;SSAS tabulare&#41;](directquery-mode-ssas-tabular.md)   
 [Origini dati &#40;SSAS tabulare&#41;](../data-sources-ssas-tabular.md)   
 [Distribuzione di una soluzione del modello tabulare &#40;SSAS tabulare&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
