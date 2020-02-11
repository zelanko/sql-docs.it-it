---
title: Finestra di dialogo Crea query di polling (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createpollingquerydialog.f1
ms.assetid: 0f2902b5-796a-4eb0-be03-01514dc01b9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: faf96ad02005c0385ec56e1f8763da2e82f093ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086829"
---
# <a name="create-polling-query-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Crea query di polling (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Crea query di polling** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare una query di polling nella scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione** . Una query di polling è in genere una query singleton che restituisce un valore utilizzabile da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per determinare se sono state apportate modifiche a una tabella o a un altro oggetto relazionale. Per visualizzare la finestra di dialogo **Crea query di polling**, è possibile fare clic sul pulsante con i puntini di sospensione (**...**) nella colonna **Query di polling** della griglia relativa all'opzione **Polling pianificato** nella scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione**. Per altre informazioni sulla scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione** vedere [Notifiche &#40;finestra di dialogo Opzioni di archiviazione&#41; &#40;Analysis Services - Dati multidimensionali&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).  
  
 Il tipo di valore restituito dalla query di polling dipende dal tipo di aggiornamenti pianificati per la cache OLAP multidimensionale (MOLAP) dell'oggetto in base alla tabella su cui viene eseguita la query.  
  
-   Se l'opzione **Attiva aggiornamenti incrementali** non è selezionata nella scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione** , in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene eseguito l'aggiornamento completo della cache MOLAP dell'oggetto se viene rilevata una modifica durante il polling pianificato. Mediante la query di polling deve essere determinato se sono stati aggiunti record alla tabella dall'ultimo periodo di polling.  
  
-   Se l'opzione **Attiva aggiornamenti incrementali** è selezionata nella scheda **Notifiche** della finestra di dialogo **Opzioni di archiviazione** , in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene eseguito l'aggiornamento incrementale della cache MOLAP dell'oggetto se viene rilevata una modifica durante il polling pianificato. Mediante la query di polling utilizzata deve essere individuato l'ultimo record nella tabella.  
  
 Ad esempio, è possibile utilizzare le query di polling seguenti per fornire aggiornamenti completi o incrementali relativi alla dimensione Customer nel database di esempio di [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Tipo di aggiornamento|Query di polling|  
|-----------------|-------------------|  
|Aggiornamento completo|`SELECT`<br /><br /> `COUNT(*) AS TotalCount`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|Aggiornamento incrementale|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
  
 Per altre informazioni sugli aggiornamenti completi e incrementali per le notifiche tramite polling pianificato, vedere [Memorizzazione nella cache attiva &#40;partizioni&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
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
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Passa a Generatore query generico**|Selezionare questo comando per visualizzare solo le opzioni disponibili nella vista Generatore query generico. Verranno visualizzate solo le opzioni seguenti.<br /><br /> **Riquadro SQL**<br /><br /> **Riquadro risultati**<br /><br /> **Barra degli strumenti**, contenente solo il **passaggio a Visual Database Tools Generatore di query** ed **eseguire**<br /><br /> <br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Passa a Generatore query Visual Database Tools**|Selezionare questo comando per visualizzare tutte le opzioni disponibili nella vista Generatore query Visual Database Tools.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query generico** .|  
|**Mostra/Nascondi riquadro diagramma**|Consente di visualizzare o nascondere il **riquadro diagramma**.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Mostra/Nascondi riquadro griglia**|Consente di visualizzare o nascondere il **riquadro griglia**.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Mostra/Nascondi riquadro SQL**|Consente di visualizzare o nascondere il **riquadro SQL**.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Mostra/Nascondi riquadro risultati**|Consente di visualizzare o nascondere il riquadro risultati. ****<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Esegui**|Consente di eseguire la query. I risultati verranno visualizzati nell'apposito riquadro ****.|  
|**Verifica SQL**|Consente di verificare l'istruzione SQL nella query.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Ordinamento crescente**|Consente di disporre in ordine crescente le righe di output della colonna selezionata nel riquadro griglia. ****<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Ordinamento decrescente**|Consente di disporre in ordine decrescente le righe di output della colonna selezionata nel riquadro griglia. ****<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Rimuovi filtro**|Consente di rimuovere i criteri di ordinamento, se applicabili, per la riga selezionata nel riquadro griglia. ****.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**USA Group by**|Consente di aggiungere funzionalità di raggruppamento alla query.<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Aggiungi tabella**|Consente di visualizzare la finestra di dialogo **Aggiungi tabella** per aggiungere una nuova tabella o vista alla query. Per altre informazioni sulla finestra di dialogo **Aggiungi tabella**, vedere [Finestra di dialogo Aggiungi tabella &#40;Analysis Services - Dati multidimensionali&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Nota: questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
  
 **Riquadro diagramma**  
 Consente di visualizzare gli oggetti a cui fa riferimento la query sotto forma di diagramma. Nel diagramma vengono visualizzate le tabelle incluse nella query e indicate le relative modalità di unione in join. Selezionare o deselezionare la casella di controllo accanto a una colonna nella tabella per aggiungere o rimuovere la colonna dall'output della query.  
  
 Quando si aggiungono tabelle alla query, vengono creati join tra le tabelle in base alle chiavi della tabella. Per aggiungere un join, trascinare un campo da una tabella in un campo di un'altra tabella. Per gestire un join, fare clic su di esso con il pulsante destro del mouse.  
  
 Fare clic con il pulsante destro del mouse sul **riquadro Diagramma** per aggiungere o rimuovere tabelle, selezionare tutte le tabelle e visualizzare o nascondere i riquadri.  
  
> [!NOTE]  
>  Il contenuto del riquadro **diagramma**, del **riquadro griglia**e del **riquadro SQL** sono sincronizzati, in modo che le modifiche apportate in un riquadro siano riflesse negli altri due riquadri.  
  
> [!IMPORTANT]  
>  Questa finestra di dialogo non supporta la modifica dei tipi di query.  
  
 **Riquadro griglia**  
 Consente di visualizzare gli oggetti a cui fa riferimento la query in una griglia. È possibile utilizzare questo riquadro per aggiungere o rimuovere colonne da un query e modificare le impostazioni per ogni colonna.  
  
> [!NOTE]  
>  Il contenuto del riquadro **diagramma**, del **riquadro griglia**e del **riquadro SQL** sono sincronizzati, in modo che le modifiche apportate in un riquadro siano riflesse negli altri due riquadri.  
  
 **Riquadro SQL**  
 Consente di visualizzare la query come istruzione SQL. Digitare un testo per modificare l'istruzione SQL per la query.  
  
> [!NOTE]  
>  Il contenuto del riquadro **diagramma**, del **riquadro griglia**e del **riquadro SQL** sono sincronizzati, in modo che le modifiche apportate in un riquadro siano riflesse negli altri due riquadri.  
  
 **Riquadro risultati**  
 Consente di visualizzare i risultati della query quando si fa clic su **Esegui** nel riquadro **Barra degli strumenti** .  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
