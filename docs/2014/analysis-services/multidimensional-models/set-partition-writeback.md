---
title: Imposta writeback partizione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], writeback
- partitions [Analysis Services], write-enabled
- writeback [Analysis Services], partitions
ms.assetid: 38bb09cc-2652-4971-8373-0cf468cdc7a6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3359e26ace467bbf8446aac6b68a0ef2716d09a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072898"
---
# <a name="set-partition-writeback"></a>Impostare tabelle writeback delle partizioni
  Se si abilita un gruppo di misure per la scrittura, gli utenti finali possono modificare i dati del cubo durante la relativa esplorazione; tuttavia, le modifiche vengono salvate in una tabella separata denominata tabella writeback, non nei dati del cubo o nei dati di origine. Gli utenti finali che esplorano una partizione abilitata per la scrittura visualizzano il risultato finale di tutte le modifiche nella tabella writeback per la partizione.  
  
 È possibile esplorare o eliminare i dati writeback, nonché convertirli in una partizione. In una partizione abilitata per la scrittura, è possibile utilizzare i ruoli dei cubi per concedere l'accesso in lettura/scrittura a singoli utenti e gruppi di utenti, nonché per limitare l'accesso a celle o gruppi di celle specifici nella partizione.  
  
 Per un breve video introduttivo al writeback, vedere quello relativo al [writeback in Excel 2010 per Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=394951). Un'analisi più dettagliata di questa funzionalità è disponibile tramite questa serie di post di blog relativi alla [compilazione di un'applicazione di writeback con Analysis Services (blog)](https://go.microsoft.com/fwlink/?LinkId=394977).  
  
> [!NOTE]  
>  Il writeback è supportato solo per i database relazionali e i data mart di SQL Server e solo per i modelli multidimensionali di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="how-to-write-enable-a-partition"></a>Come abilitare una partizione per la scrittura  
 È possibile abilitare per la scrittura i gruppi di misure di una partizione abilitando per la scrittura la partizione stessa in Progettazione cubi in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Nella scheda Partizioni di Progettazione cubi fare clic con il pulsante destro del mouse su una partizione e scegliere **Impostazioni writeback**.  
  
-   In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]espandere il database | cubo | gruppo di misure, quindi fare clic con il pulsante destro del mouse su **Writeback** e scegliere **Abilita writeback**.  
  
 Il writeback è supportato solo per le misure che utilizzano l'aggregazione SUM. Nel database di esempio AdventureWorks è possibile utilizzare il gruppo di misure Sales Targets per testare i comportamenti del writeback.  
  
 Quando si abilita una partizione per la scrittura, è necessario specificare una tabella e un'origine dei dati per l'archiviazione della tabella di writeback. Le eventuali modifiche apportate successivamente al gruppo di misure vengono registrate in questa tabella.  
  
## <a name="browse-writeback-data-in-a-partition"></a>Esplorare i dati writeback in una partizione  
 È possibile visualizzare il contenuto di una tabella writeback di un cubo nella finestra di dialogo **Visualizza dati** , a cui è possibile accedere facendo clic sul pulsante destro del mouse su una partizione abilitata per la lettura nella scheda **Partizioni** di Progettazione cubi.  
  
## <a name="delete-writeback-data-or-disable-writeback"></a>Eliminare i dati writeback o disabilitare il writeback  
 Eliminando i dati writeback si cancella la cache writeback. Non appena i dati vengono eliminati, nello stato pulito vengono eseguite ulteriori operazioni di writeback. Disabilitando il writeback per una partizione del cubo si disattiva semplicemente il writeback per tale partizione.  
  
## <a name="convert-writeback-data-to-a-partition"></a>Convertire i dati writeback in una partizione  
 È possibile convertire i dati della tabella writeback di una partizione in una nuova partizione. Questa procedura consente di trasformare la tabella writeback nella tabella dei fatti della nuova partizione.  
  
> [!CAUTION]  
>  Un utilizzo non corretto delle partizioni può generare dati non accurati nel cubo. Per altre informazioni, vedere [Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md).  
  
 Se si converte la tabella di dati writeback in una partizione, quest'ultima verrà inoltre disabilitata per la scrittura. Tutti i criteri di lettura/scrittura senza restrizioni e le autorizzazioni di lettura/scrittura per le celle della partizione verranno disabilitati e gli utenti finali non potranno modificare i dati del cubo visualizzati. Gli utenti finali con i criteri di lettura/scrittura senza restrizioni disabilitati o le autorizzazioni di lettura/scrittura disabilitate potranno comunque esplorare il cubo. Le autorizzazioni di lettura e di lettura condizionale rimarranno invariate.  
  
 Per convertire i dati writeback in una partizione, usare la finestra di dialogo **Converti in partizione** , a cui è possibile accedere facendo clic con il pulsante destro del mouse sulla tabella writeback di una partizione abilitata per la scrittura in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È possibile specificare il nome della partizione e quindi progettare la relativa aggregazione durante la creazione della partizione stessa o in un secondo momento. Per creare l'aggregazione quando si seleziona la partizione, è necessario scegliere di copiare la progettazione dell'aggregazione da una partizione esistente, che in genere, ma non necessariamente, corrisponde alla partizione writeback corrente. È inoltre possibile scegliere di elaborare la partizione durante la creazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni abilitate per la scrittura](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Abilitazione del writeback in un cubo OLAP a livello di cella in Excel 2010](https://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [Abilitazione e protezione dell'immissione di dati con Analysis Services writeback](https://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
