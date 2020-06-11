---
title: Finestra di dialogo Crea query di elaborazione (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createprocessingquerydialog.f1
ms.assetid: c133d624-f35e-486e-be9f-ceafd906f168
author: minewiskan
ms.author: owend
ms.openlocfilehash: 185ea27c344ccb9e06f914507faca3fea9554dae
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526440"
---
# <a name="create-processing-query-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Crea query di elaborazione (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Crea query di elaborazione** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare una query di elaborazione nella scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione** . Una query di elaborazione è una query che restituisce un set di righe contenente le modifiche apportate a una tabella associata a un oggetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a partire dall'ultimo polling della tabella eseguito per aggiornare in modo incrementale la cache OLAP multidimensionale (MOLAP) dell'oggetto. Per eseguire il polling di una tabella associata a un oggetto e stabilire se la tabella è stata modificata, Analysis Services utilizza un'altra query, definita query di polling. Le query di elaborazione non sono necessarie quando si aggiorna completamente la cache MOLAP relativa all'oggetto.  
  
 In genere, la query di elaborazione contiene parametri, di cui due attualmente supportati:  
  
-   Il valore singleton restituito dalla query di polling durante il polling pianificato precedente.  
  
-   Il valore singleton restituito dalla query di polling durante il polling pianificato corrente.  
  
 Le query incluse nell'elenco della tabella seguente possono ad esempio essere usate per l'aggiornamento incrementale della dimensione Customer nel progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] di esempio Adventure Works DW.  
  
|Tipo di query|Istruzione query|  
|----------------|---------------------|  
|Query di polling|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|Query di elaborazione|`SELECT`<br /><br /> `*`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`<br /><br /> `WHERE`<br /><br /> `(CustomerKey > COALESCE (@Param1, - 1))`<br /><br /> `AND (CustomerKey <= @Param2)`|  
  
 Per altre informazioni sugli aggiornamenti incrementali per le notifiche tramite polling pianificato, vedere [Memorizzazione nella cache attiva &#40;partizioni&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
 Per visualizzare la finestra di dialogo **Crea query di elaborazione**, è possibile fare clic sul pulsante **...** nella colonna **Query di elaborazione** della griglia relativa all'opzione **Polling pianificato** nella scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione**. Per altre informazioni sulla scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione** vedere [Notifiche &#40;finestra di dialogo Opzioni di archiviazione&#41; &#40;Analysis Services - Dati multidimensionali&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).  
  
 La query immessa deve essere un comando di query valido per il provider sottostante. La query viene preparata con il provider sottostante per la convalida e per l'identificazione delle colonne restituite. Sono previste due viste per la finestra di dialogo:  
  
-   Generatore query Visual Database Tools (VDT)  
  
     Per tutti gli utenti, nella vista Generatore query Visual Database Tools è disponibile un set di strumenti di interfaccia utente che consente di costruire e testare visivamente una query SQL.  
  
-   Generatore query generico  
  
     La visualizzazione Generatore query generico offre agli utenti esperti un'interfaccia utente più semplice e diretta per la costruzione e la verifica di una query SQL.  
  
## <a name="options"></a>Opzioni  
 **Origine dati**  
 Consente di specificare l'origine dei dati per la query.  
  
 **Definizione query**  
 Questa opzione mette a disposizione una barra degli strumenti e riquadri in cui è possibile definire e testare la query, a seconda della vista selezionata.  
  
 **Barra degli strumenti**  
 La barra degli strumenti consente di gestire i set di dati, selezionare i riquadri da visualizzare e controllare le varie funzioni di query.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**Passa a Generatore query generico**|Selezionare questo comando per visualizzare solo le opzioni disponibili nella vista Generatore query generico. Verranno visualizzate solo le opzioni seguenti.<br /><br /> **Riquadro SQL**<br /><br /> **Riquadro risultati**<br /><br /> **Barra degli strumenti**, contenente solo **Passa a Generatore query Visual Database Tools** ed **Esegui**<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Passa a Generatore query Visual Database Tools**|Selezionare questo comando per visualizzare tutte le opzioni disponibili nella vista Generatore query Visual Database Tools.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query generico** .|  
|**Mostra/Nascondi riquadro diagramma**|Consente di visualizzare o nascondere il **riquadro diagramma**.<br /><br /> **Nota** Questa opzione viene visualizzata solo se è selezionata l'opzione **passa a visual database tools generatore di query** .|  
|**Mostra/Nascondi riquadro griglia**|Consente di visualizzare o nascondere il **riquadro griglia**.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Mostra/Nascondi riquadro SQL**|Consente di visualizzare o nascondere il **riquadro SQL**.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Mostra/Nascondi riquadro risultati**|Consente di visualizzare o nascondere il riquadro risultati. ****<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Esegui**|Consente di eseguire la query. I risultati verranno visualizzati nell'apposito riquadro ****.|  
|**Verifica istruzione SQL**|Consente di verificare l'istruzione SQL nella query.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Ordinamento crescente**|Consente di disporre in ordine crescente le righe di output della colonna selezionata nel riquadro griglia. ****<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Ordinamento decrescente**|Consente di disporre in ordine decrescente le righe di output della colonna selezionata nel riquadro griglia. ****<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Rimuovi filtro**|Consente di rimuovere i criteri di ordinamento, se applicabili, per la riga selezionata nel riquadro griglia. ****.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Usa Group By**|Consente di aggiungere funzionalità di raggruppamento alla query.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Aggiungi tabella**|Consente di visualizzare la finestra di dialogo **Aggiungi tabella** per aggiungere una nuova tabella o vista alla query. Per altre informazioni sulla finestra di dialogo **Aggiungi tabella**, vedere [Finestra di dialogo Aggiungi tabella &#40;Analysis Services - Dati multidimensionali&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
  
 **Riquadro diagramma**  
 Consente di visualizzare gli oggetti a cui fa riferimento la query sotto forma di diagramma. Nel diagramma vengono visualizzate le tabelle incluse nella query e indicate le relative modalità di unione in join. Selezionare o deselezionare la casella di controllo accanto a una colonna nella tabella per aggiungere o rimuovere la colonna dall'output della query.  
  
 Quando si aggiungono tabelle alla query, vengono creati join tra le tabelle in base alle chiavi della tabella. Per aggiungere un join, trascinare un campo da una tabella in un campo di un'altra tabella. Per gestire un join, fare clic su di esso con il pulsante destro del mouse.  
  
 Fare clic con il pulsante destro del mouse sul **riquadro Diagramma** per aggiungere o rimuovere tabelle, selezionare tutte le tabelle e visualizzare o nascondere i riquadri.  
  
> [!NOTE]  
>   I contenuti del riquadro diagramma ****, del riquadro griglia **** e del riquadro SQL **** sono sincronizzati, pertanto le modifiche apportate in un riquadro vengono aggiornate anche negli altri due riquadri.  
  
> [!IMPORTANT]  
>  Questa finestra di dialogo non supporta la modifica dei tipi di query.  
  
 **Riquadro griglia**  
 Consente di visualizzare gli oggetti a cui fa riferimento la query in una griglia. È possibile utilizzare questo riquadro per aggiungere o rimuovere colonne da un query e modificare le impostazioni per ogni colonna.  
  
> [!NOTE]  
>   I contenuti del riquadro diagramma ****, del riquadro griglia **** e del riquadro SQL **** sono sincronizzati, pertanto le modifiche apportate in un riquadro vengono aggiornate anche negli altri due riquadri.  
  
 **Riquadro SQL**  
 Consente di visualizzare la query come istruzione SQL. Digitare un testo per modificare l'istruzione SQL per la query.  
  
> [!NOTE]  
>   I contenuti del riquadro diagramma ****, del riquadro griglia **** e del riquadro SQL **** sono sincronizzati, pertanto le modifiche apportate in un riquadro vengono aggiornate anche negli altri due riquadri.  
  
 **Riquadro risultati**  
 Consente di visualizzare i risultati della query quando si fa clic su **Esegui** nel riquadro **Barra degli strumenti** .  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
