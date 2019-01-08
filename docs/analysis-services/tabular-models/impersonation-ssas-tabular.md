---
title: Rappresentazione nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 724d9220f156cb9b2a00e3bd12a15f35750de652
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416023"
---
# <a name="impersonation"></a>Rappresentazione 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo fornisce agli autori di modelli tabulari la comprensione del modo in cui le credenziali di accesso vengono utilizzate da Analysis Services quando ci si connette a un'origine dati per importare ed elaborare (aggiornare) i dati.  

##  <a name="bkmk_conf_imp_info"></a> Configurazione della rappresentazione  
 La posizione e in quale contesto di un modello esistente determina la configurazione di impostazioni di rappresentazione. Quando si crea un nuovo progetto di modello, la rappresentazione è configurata in SQL Server Data Tools (SSDT) quando ci si connette a un'origine dati per importare i dati. Dopo aver distribuito un modello, la rappresentazione configurabili nelle proprietà di stringa di connessione del database modello tramite SQL Server Management Studio (SSMS). Per i modelli tabulari in Azure Analysis Services, è possibile usare SQL Server Management Studio o **Visualizza come: Script** modalità nella finestra di progettazione basata su browser per modificare il file Model. bim in formato JSON.
  
##  <a name="bkmk_how_imper"></a> Utilizzo della rappresentazione  
 La*rappresentazione* è la capacità di un'applicazione server, ad esempio Analysis Services, di assumere l'identità di un'applicazione client. Analysis Services viene eseguito utilizzando un account del servizio, tuttavia, quando il server viene stabilita una connessione a un'origine dati, viene utilizzata la rappresentazione in modo che i controlli di accesso per l'importazione di dati e l'elaborazione può essere eseguita.  
  
 Credenziali utilizzate per la rappresentazione sono diverse da quelle che attualmente è connessi con. L'accesso utente vengono usate per le operazioni lato client specifiche durante la creazione di un modello.  
  
 È importante comprendere come le credenziali di rappresentazione vengono specificate e protetto, nonché la differenza tra i contesti in cui sia quello usato in vengono utilizzate le credenziali utente e quando altre credenziali di rappresentazione vengono utilizzate.  
  
 **Informazioni sulle credenziali lato server**  
 
Quando i dati vengono importati o elaborati, credenziali di rappresentazione vengono utilizzate per connettersi all'origine dati e recuperare i dati. Si tratta di un *sul lato server* operazione in esecuzione nel contesto di un'applicazione client poiché il server di Analysis Services che ospita il database dell'area di lavoro si connette all'origine dati e vengono recuperati i dati.  
  
 Quando si distribuisce un modello in un server Analysis Services, se il database dell'area di lavoro è in memoria durante la distribuzione del modello, le credenziali vengono passate al server Analysis Services in cui viene distribuito il modello. In nessuna circostanza si stratta di credenziali utente archiviate su disco.  
  
 Quando un modello distribuito vengono elaborati i dati da un'origine dati, le credenziali di rappresentazione, persistente nel database in memoria, vengono utilizzate per connettersi all'origine dati e recuperare i dati. Poiché questo processo viene gestito dal server di Analysis Services gestito il database modello, si tratta nuovamente di un'operazione lato server.  
  
 **Informazioni sulle credenziali lato client**  
  
 Quando un nuovo modello di creazione o l'aggiunta di un'origine dati a un modello esistente, connettersi a un'origine dati e selezionare le tabelle e viste da importare nel modello. Nelle funzionalità di anteprima e filtro importazione guidata tabella o la finestra di progettazione Data\Query ottenere, vedrai un campione di dati che importati. Inoltre, è possibile specificare filtri per escludere dati che non devono essere inclusi nel modello.  
  
 Analogamente, per modelli esistenti che sono già stati creati, si usa la **le proprietà della tabella** finestra di dialogo Anteprima e filtrare i dati importati in una tabella.  
  
 Le funzionalità di anteprima e Applica filtro **le proprietà della tabella**, e **gestione partizioni** finestre di dialogo sono un in-process *lato client* operazione, vale a dire, ciò che avviene durante questo operazione sono diverse dalla modalità di connessione per l'origine dati e i dati vengono recuperati dall'origine dati; un'operazione lato server. Le credenziali utilizzate per l'anteprima e il filtro dei dati sono quelle dell'utente attualmente connesso. In effetti, le credenziali. 
  
 La separazione di credenziali utilizzato sul lato server e le operazioni lato client possono causare una mancata corrispondenza tra ciò che viene visualizzato e quali dati vengono recuperati durante un'importazione o l'elaborazione (operazione lato server). Se le credenziali attualmente connessi con le credenziali di rappresentazione specificate sono diverse, i dati presenti le funzionalità di anteprima e filtro o la **le proprietà della tabella** finestra di dialogo e i dati recuperati durante un'importazione o processo può essere diverso, a seconda delle credenziali richieste dall'origine dati.  
  
> [!IMPORTANT]  
>  Quando si crea un modello, assicurarsi è connessi con credenziali e le credenziali specificate per la rappresentazione dispongano di diritti sufficienti per recuperare i dati dall'origine dati.  
  
##  <a name="bkmk_imp_info_options"></a> Opzioni  
 Quando si configura la rappresentazione o si modificano proprietà per una connessione all'origine dati esistente, specificare una delle opzioni seguenti:  
  
**Modelli tabulari 1400 e versioni successive**
 
|Opzione|Descrizione|  
|------------|-----------------|  
|**Rappresenta l'Account**|Specifica il modello viene utilizzato un account utente di Windows per importare o elaborare i dati dall'origine dati. Il dominio e il nome dell'account utente nel formato seguente:**\<nome di dominio >\\< nome dell'account utente\>**.|  
|**Rappresentare l'utente corrente**|Specifica che devono accedere ai dati dall'origine dati usando l'identità dell'utente che ha inviato la richiesta. Questa modalità si applica solo alla modalità DirectQuery.|  
|**Rappresenta identità**|Specifica un nome utente per accedere a origine dati, ma non è necessario specificare la password dell'account. Questa modalità si applica solo quando la delega Kerberos è abilitata e specifica che l'autenticazione S4U deve essere utilizzato.|  
|**Rappresenta l'Account del servizio**|Specifica l'utilizzo di modello le credenziali di sicurezza associate all'istanza del servizio Analysis Services che gestisce il modello.|  
|**Rappresenta Account automatico**|Specifica che il motore Analysis Services deve utilizzare un account automatico preconfigurato per accedere ai dati.|  


**I modelli tabulari 1200**
 
|Opzione|Descrizione|  
|------------|-----------------|  
|**Specifica nome utente di Windows e password**|Questa opzione specifica il modello viene utilizzato un account utente di Windows per importare o elaborare i dati dall'origine dati. Il dominio e il nome dell'account utente nel formato seguente:**\<nome di dominio >\\< nome dell'account utente\>**. Si tratta dell'opzione predefinita per la creazione di un nuovo modello tramite l'Importazione guidata tabella.|  
|**Account servizio**|Questa opzione consente di specificare che nel modello vengono utilizzate le credenziali di sicurezza associate all'istanza del servizio Analysis Services tramite cui viene gestito il modello.|  
  
##  <a name="bkmk_impers_sec"></a> Sicurezza  
 Le credenziali utilizzate con la rappresentazione sono persistenti in memoria dal motore di VertiPaq™. Credenziali non vengono mai scritti su disco. Se il database dell'area di lavoro non è in memoria quando il modello viene distribuito, l'utente viene chiesto di immettere le credenziali usate per connettersi ai dati dell'origine dati e fetch.  
  
> [!NOTE]  
>  Si consiglia di specificare un account utente di Windows e una password per le credenziali di rappresentazione. Un account utente di Windows può essere configurato per l'uso dei privilegi minimi necessari per connettersi e leggere i dati dall'origine dati.  
  

  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Origini dati](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Distribuzione di una soluzione del modello tabulare](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
