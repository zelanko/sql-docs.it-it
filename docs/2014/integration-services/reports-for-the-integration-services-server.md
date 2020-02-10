---
title: Report per il server di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa53c012649f983953b61a21901763b9bdd02c8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056437"
---
# <a name="reports-for-the-integration-services-server"></a>Report per il server Integration Services
  Nella versione corrente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]sono disponibili report standard in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per monitorare i progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] distribuiti nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . I report consentono di visualizzare lo stato e la cronologia dei pacchetti e, se necessario, identificare la causa di eventuali errori.  
  
 All'inizio di ogni pagina dei report sono disponibili l'icona che consente di tornare alla pagina precedentemente visualizzata, l'icona tramite cui viene eseguito l'aggiornamento delle informazioni visualizzate nella pagina e l'icona che consente all'utente di stampare la pagina corrente.  
  
 Per informazioni su come distribuire i pacchetti al server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vedere [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
## <a name="integration-services-dashboard"></a>Dashboard Integration Services  
 Nel report **Dashboard Integration Services** è disponibile una panoramica di tutte le esecuzioni dei pacchetti nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per ogni pacchetto eseguito nel server, il dashboard consente all'utente di effettuare un ingrandimento per trovare dettagli specifici sugli errori di esecuzione del pacchetto che potrebbero essersi verificati.  
  
 Nel report sono mostrate le sezioni di informazioni seguenti.  
  
|Sezione|Descrizione|  
|-------------|-----------------|  
|**Informazioni sulle esecuzioni**|Viene mostrato il numero di esecuzioni che si trovano in stati diversi (operazione non riuscita, in esecuzione, operazione riuscita e altri) nelle ultime 24 ore.|  
|**Informazioni sui pacchetti**|Viene mostrato il numero totale di pacchetti eseguiti nelle ultime 24 ore.|  
|**Informazioni di connessione**|Vengono mostrate le connessioni utilizzate nelle esecuzioni non completate correttamente durante le ultime 24 ore.|  
|**Informazioni dettagliate sui pacchetti**|Vengono mostrati i dettagli delle esecuzioni completate durante le ultime 24 ore. In questa sezione viene ad esempio illustrato il numero di esecuzioni non completate rispetto al numero totale di esecuzioni, la durata di un'esecuzione (in secondi) e la durata media delle esecuzioni negli ultimi tre mesi.<br /><br /> È possibile visualizzare altre informazioni per un pacchetto facendo clic su **Panoramica**, **All Messages**(Tutti i messaggi) e **Prestazioni di esecuzione**.<br /><br /> Nel report **Prestazioni di esecuzione** viene visualizzata la durata dell'ultima istanza di esecuzione, nonché l'ora di inizio e di fine e l'ambiente applicato.<br /><br /> Nel grafico e nella tabella associata inclusi nel report **Prestazioni di esecuzione** viene indicata la durata delle ultime 10 esecuzioni completate del pacchetto. Nella tabella viene inoltre illustrata la durata media di esecuzione nell'arco di tre mesi. In fase di esecuzione potrebbero essere stati applicati ambienti e valori letterali diversi per queste 10 esecuzioni completate del pacchetto.<br /><br /> Infine, nel report **Prestazioni di esecuzione** vengono visualizzati il tempo di attività e il tempo totale per i componenti flusso di dati del pacchetto. Il tempo attivo si riferisce alla quantità totale di tempo di esecuzione del componente in tutte le fasi e la durata totale equivale al tempo totale trascorso per un componente. Nel report vengono visualizzate queste informazioni per i componenti del pacchetto solo se il livello di registrazione dell'ultima esecuzione del pacchetto è stato impostato su Prestazioni o Dettagliato.<br /><br /> Nel report **Panoramica** viene mostrato lo stato delle attività del pacchetto. Nel report **Messaggi** vengono visualizzati i messaggi di evento e i messaggi di errore per il pacchetto e le attività, ad esempio per segnalare l'ora di inizio e di fine e il numero di righe scritte.<br /><br /> È anche possibile fare clic su **Visualizzazione messaggi** nel report **Panoramica** per passare al report **Messaggi** . È anche possibile fare clic su **Visualizza panoramica** nel report **Messaggi** per passare al report **Panoramica** .|  
  
 È possibile filtrare la tabella visualizzata in qualsiasi pagina facendo clic su **Filtro** e selezionando i criteri nella finestra di dialogo **Impostazioni filtro** . I criteri di filtro disponibili dipendono dai dati visualizzati. È possibile modificare l'ordinamento del report facendo clic sulla relativa icona nella finestra di dialogo **Impostazioni filtro** .  
  
## <a name="all-executions-report"></a>Report Tutte le esecuzioni  
 Nel report **All Executions** (Tutte le esecuzioni) viene visualizzato un riepilogo di tutte le esecuzioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] effettuate nel server. Possono essere presenti più esecuzioni del pacchetto di esempio. A differenza del report **Dashboard Integration Services** , è possibile configurare il report **All Executions** (Tutte le esecuzioni) per visualizzare le esecuzioni avviate durante un intervallo di date. Le date possono estendersi per più giorni, mesi o anni.  
  
 Nel report sono mostrate le sezioni di informazioni seguenti.  
  
|Sezione|Descrizione|  
|-------------|-----------------|  
|Filtro|Mostra il filtro corrente applicato al report, ad esempio l'intervallo Ora inizio.|  
|Informazioni sulle esecuzioni|Indica l'ora di inizio, l'ora di fine e la durata di ogni esecuzione del pacchetto. È possibile visualizzare un elenco di valori dei parametri utilizzati con l'esecuzione di un pacchetto, ad esempio i valori passati a un pacchetto figlio utilizzando l'attività Esegui pacchetto. Per visualizzare l'elenco dei parametri, fare clic su Panoramica.|  
  
 Per altre informazioni sull'utilizzo dell'attività Esegui pacchetto per rendere disponibili valori a un pacchetto figlio, vedere [Attività Esegui pacchetto](control-flow/execute-package-task.md).  
  
 Per altre informazioni sui parametri, vedere [Parametri di Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="all-connections"></a>Tutte le connessioni  
 Nel report **All Connections** (Tutte le connessioni) sono incluse le informazioni seguenti, relative alle connessioni non riuscite, per le esecuzioni che si sono verificate nell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Nel report sono mostrate le sezioni di informazioni seguenti.  
  
|Sezione|Descrizione|  
|-------------|-----------------|  
|Filtro|Mostra il filtro corrente applicato al report, ad esempio le connessioni con una stringa specificata e il valore di **Intervallo di ore ultimo errore** .<br /><br /> Impostare un valore per **Intervallo di ore ultimo errore** per visualizzare solo gli errori di connessione che si sono verificati durante un intervallo di date. L'intervallo può estendersi per più giorni, mesi o anni.|  
|Dettagli|Mostra la stringa di connessione, il numero di esecuzioni durante le quali una connessione non è riuscita e la data in cui l'ultima connessione non è riuscita.|  
  
## <a name="all-operations-report"></a>Report Tutte le operazioni  
 Nel report **All Operations** (Tutte le operazioni) viene visualizzato un riepilogo di tutte le operazioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] eseguite nel server, incluse la distribuzione, la convalida e l'esecuzione dei pacchetti, nonché altre operazioni amministrative. Come per il Dashboard Integration Services, è possibile applicare un filtro alla tabella per limitare le informazioni visualizzate.  
  
## <a name="all-validations-report"></a>Report Tutte le convalide  
 Nel report **Tutte le convalide** viene visualizzato un riepilogo di tutte le convalide di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] effettuate nel server. Nel riepilogo vengono visualizzate informazioni per ogni convalida, ad esempio, stato, ora di inizio e ora di fine. In ogni voce del riepilogo è incluso un collegamento ai messaggi generati durante la convalida. Come per il Dashboard Integration Services, è possibile applicare un filtro alla tabella per limitare le informazioni visualizzate.  
  
## <a name="custom-reports"></a>Report personalizzati  
 È possibile aggiungere un report personalizzato (file con estensione rdl) al nodo del catalogo **SSISDB** nel nodo **Cataloghi di Integration Services** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Prima di aggiungere il report, verificare che sia in uso una convenzione di denominazione di terze parti per assegnare nomi completi agli oggetti a cui si fa riferimento, ad esempio una tabella di origine. In caso contrario, in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] verrà visualizzato un errore. La convenzione di denominazione è \<database>.\<proprietario>.\<oggetto>. ad esempio SSISDB.internal.executions.  
  
> [!NOTE]  
>  Quando si aggiungono report personalizzati al nodo **SSISDB** nel nodo **Database** , il prefisso SSISDB non è necessario.  
  
 Per istruzioni su come creare e aggiungere un report personalizzato, vedere [Aggiunta di un report personalizzato a Management Studio](../ssms/object/add-a-custom-report-to-management-studio.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Visualizzare i report per il server Integration Services](../../2014/integration-services/view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Monitoraggio per le esecuzioni di pacchetti e altre operazioni](performance/monitor-running-packages-and-other-operations.md)  
  
  
