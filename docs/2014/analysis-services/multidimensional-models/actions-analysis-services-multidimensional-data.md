---
title: Azioni (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- actions [Analysis Services]
- actions [Analysis Services], about actions
- MDX [Analysis Services], actions
- cubes [Analysis Services], actions
- OLAP objects [Analysis Services], actions
ms.assetid: 07229bb2-805c-427e-8455-69c9ca5d01e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ff4e330950a3fca54ba8ab08456157156836c0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077584"
---
# <a name="actions-analysis-services---multidimensional-data"></a>Azioni (Analysis Services - Dati multidimensionali)
  Sono disponibili azioni di diverso tipo, le quali devono pertanto essere create in modo appropriato. Di seguito vengono indicati i diversi tipi di azione.  
  
-   Azioni drill-through, che restituiscono il set di righe che rappresenta i dati sottostanti delle celle selezionate del cubo in cui si verifica l'azione.  
  
-   Azioni report, che restituiscono un report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] associato alla sezione selezionata del cubo in cui si verifica l'azione.  
  
-   Azioni standard, le quali restituiscono l'elemento dell'azione (URL, HTML, DataSet, RowSet e altri elementi) associato alla sezione selezionata del cubo in cui si verifica l'azione.  
  
 Un QI (Query Interface), ad esempio ADOMD.NET, viene utilizzato dall'applicazione client per recuperare le azioni ed esporle all'utente finale. Per altre informazioni, vedere [Sviluppo con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net).  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Action> semplice è composto da informazioni di base, dalla destinazione in cui deve verificarsi l'azione, da una condizione per limitare l'ambito dell'azione e dal tipo. Le informazioni di base includono il nome dell'azione, la descrizione dell'azione, la didascalia consigliata per l'azione e altro.  
  
 La destinazione corrisponde al percorso effettivo nel cubo in cui deve verificarsi l'azione. La destinazione è composta da un tipo di destinazione e da un oggetto di destinazione. Il tipo di destinazione rappresenta il tipo di oggetto all'interno del cubo, in cui l'azione deve essere attivata. Il tipo di destinazione può essere costituito da membri del livello, celle, gerarchia, membri della gerarchia o altro. L'oggetto di destinazione è un oggetto specifico del tipo di destinazione. Se il tipo di destinazione è una gerarchia, l'oggetto di destinazione è una delle gerarchie definite nel cubo.  
  
 La condizione è un'espressione MDX `Boolean` valutata nell'evento relativo all'azione. Se la condizione restituisce `true`, l'azione viene eseguita. In caso contrario, l'azione non viene eseguita.  
  
 Il tipo rappresenta il tipo di azione da eseguire. <xref:Microsoft.AnalysisServices.Action> è una classe astratta, per usarla è necessaria una delle classi derivate. I due tipi di azione drill-through e report sono predefiniti e dispongono delle classi derivate corrispondenti <xref:Microsoft.AnalysisServices.DrillThroughAction> e <xref:Microsoft.AnalysisServices.ReportAction>. Le altre azioni sono incluse nella classe <xref:Microsoft.AnalysisServices.StandardAction> .  
  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]un'azione è un'istruzione MDX archiviata che può essere presentata e utilizzata da applicazioni client. In altre parole, un'azione è un comando client definito e archiviato nel server. Un'azione contiene inoltre informazioni che specificano quando e come l'istruzione MDX dovrà essere visualizzata e gestita dall'applicazione client. L'operazione specificata dall'azione consente di avviare un'applicazione, utilizzando le informazioni dell'azione come parametro, o di recuperare informazioni basate sui criteri indicati dall'azione.  
  
 Le azioni consentono agli utenti aziendali di eseguire operazioni sui risultati delle analisi svolte. Salvando e riutilizzando le azioni, gli utenti finali possono eseguire operazioni aggiuntive rispetto all'analisi tradizionale, che termina in genere con la presentazione dei dati, e avviare soluzioni a problemi o carenze individuate, estendendo in questo modo gli effetti dell'applicazione di Business Intelligence al di fuori del cubo. Le azioni possono trasformare l'applicazione client da un sofisticato strumento di rendering dei dati in una parte integrante del sistema operativo aziendale. Invece di occuparsi dell'invio di tali dati come input ad applicazioni operative, gli utenti finali possono chiudere il ciclo del processo decisionale. Questa possibilità di trasformare i dati analitici in decisioni riveste un'importanza fondamentale per un'efficace applicazione di Business Intelligence.  
  
 Si supponga, ad esempio, che un utente aziendale noti mentre visualizza un cubo che il livello delle scorte corrente di un determinato prodotto sia basso. L'applicazione client fornisce all'utente aziendale un elenco di azioni, tutte relative alle scorte insufficienti di un prodotto, recuperate dal database di Analysis Services. L'utente aziendale seleziona l'azione di ordine per il membro del cubo che rappresenta il prodotto. Viene quindi avviato un nuovo ordine tramite la chiamata nel database operativo di una stored procedure che genera le informazioni appropriate da inviare al sistema di immissione degli ordini.  
  
 Durante la creazione delle azioni è possibile usufruire di una grande flessibilità. Un'azione consente ad esempio di avviare un'applicazione o di recuperare informazioni da un database. È possibile configurare un'azione in modo che venga attivata da quasi qualsiasi parte di un cubo, inclusi le dimensioni, i livelli, i membri e le celle, oppure creare più azioni per una stessa parte di un cubo, nonché passare parametri stringa alle applicazioni avviate e specificare le didascalie da visualizzare agli utenti finali durante l'esecuzione dell'azione.  
  
> [!IMPORTANT]  
>  Affinché un utente aziendale possa utilizzare le azioni, è necessario che le azioni siano supportate dall'applicazione client utilizzata dall'utente aziendale.  
  
## <a name="types-of-actions"></a>Tipi di azioni  
 La tabella seguente elenca i tipi di azioni inclusi in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|Tipo di azione|Descrizione|  
|-----------------|-----------------|  
|CommandLine|Esegue un comando al prompt dei comandi|  
|Set di dati|Restituisce un set di dati a un'applicazione client.|  
|Drill-through|Restituisce un'istruzione drill-through come un'espressione che viene eseguita dal client per restituire un set di righe|  
|Html|Esegue uno script HTML in un browser Internet|  
|Proprietario|Esegue un'operazione utilizzando un'interfaccia diversa da quelle elencate in questa tabella.|  
|Report|Invia una richiesta con parametri basata sull'URL a un server di report e restituisce un report a un'applicazione client.|  
|Set di righe|Restituisce un set di righe a un'applicazione client.|  
|.|Esegue un comando OLE DB.|  
|URL|Visualizza una pagina Web dinamica in un browser Internet|  
  
## <a name="resolving-and-executing-actions"></a>Risoluzione ed esecuzione di azioni  
 Quando un utente aziendale accede all'oggetto per cui l'oggetto comando è stato definito, l'istruzione associata all'azione viene risolta automaticamente, in modo da renderla disponibile all'applicazione client, ma l'azione non viene eseguita automaticamente. L'azione viene eseguita solo quando l'utente finale esegue l'operazione specifica del client che avvia tale azione. In un'applicazione client può ad esempio essere visualizzato un elenco di azioni sotto forma di menu popup quando l'utente aziendale fa clic con il pulsante destro del mouse su un membro o una cella particolare.  
  
## <a name="see-also"></a>Vedere anche  
 [Azioni nei modelli multidimensionali](actions-in-multidimensional-models.md)  
  
  
