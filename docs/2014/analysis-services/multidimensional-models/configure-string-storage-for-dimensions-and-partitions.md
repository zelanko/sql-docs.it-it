---
title: Configurare l'archiviazione di stringhe per dimensioni e partizioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
author: minewiskan
ms.author: owend
ms.openlocfilehash: cbac2e675a08bbcdba6a43727e3de6896a52e56c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536944"
---
# <a name="configure-string-storage-for-dimensions-and-partitions"></a>Configurare l'archivio di stringhe per dimensioni e partizioni
  È possibile riconfigurare l'archiviazione di stringhe per contenere stringhe molto grandi in attributi di dimensione o partizioni che superano il limite di dimensioni del file di 4 GB impostato per gli archivi di stringhe. Se nelle dimensioni o partizioni sono inclusi archivi di stringhe di queste dimensioni, è possibile risolvere il problema del vincolo delle dimensioni file modificando la proprietà **StringStoresCompatibilityLevel** a livello di dimensione o di partizione, per oggetti locali nonché collegati (locali o remoti).  
  
 Si noti che è possibile aumentare l'archivio di stringhe solo per gli oggetti che richiedono una capacità aggiuntiva. Nella maggior parte dei modelli multidimensionali i dati di tipo stringa sono associati alle dimensioni. Tuttavia, anche le partizioni che contengono misure totale valori distinti basate su stringhe possono trarre vantaggio da questa impostazione. Poiché l'impostazione è relativa alle stringhe, i dati numerici non sono interessati.  
  
 Tra i valori validi per questa proprietà sono inclusi i seguenti:  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**1050**|Viene specificata l'architettura dell'archivio di stringhe predefinita, soggetta a dimensioni del file massime di 4 GB per archivio.|  
|**1100**|Viene specificato un archivio di stringhe più ampio in grado di supportare fino a 4 miliardi di stringhe univoche per archivio.|  
  
> [!IMPORTANT]  
>  La modifica delle impostazioni dell'archivio di stringhe di un oggetto richiede la rielaborazione dell'oggetto stesso e di qualsiasi oggetto dipendente. L'elaborazione è necessaria per completare la routine.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Informazioni sugli archivi di stringhe](#bkmk_background)  
  
-   [Prerequisiti](#bkmk_prereq)  
  
-   [Passaggio 1: Impostare la proprietà StringStoreCompatiblityLevel in SQL Server Data Tools](#bkmk_step1)  
  
-   [Passaggio 2: Elaborazione degli oggetti](#bkmk_step2)  
  
##  <a name="about-string-stores"></a><a name="bkmk_background"></a>Informazioni sugli archivi di stringhe  
 La configurazione dell'archiviazione di stringhe è facoltativa, pertanto anche nei nuovi database creati viene usata l'architettura predefinita soggetta al limite massimo di 4 GB per le dimensioni dei file. L'utilizzo di questa architettura più ampia comporta un lieve ma percettibile impatto sulle prestazioni. È necessario utilizzarla solo se le dimensioni dei file dell'archivio di stringhe sono prossime o al limite massimo di 4 GB.  
  
> [!NOTE]  
>  Questa impostazione non si applica ai modelli di data mining. Attualmente è comunque possibile riscontrare il limite delle dimensioni dei file di GB nei modelli contenenti strutture di data mining.  
  
 In un database multidimensionale di Analysis Services le stringhe vengono archiviate separatamente dai dati numerici per consentire l'ottimizzazione in base alle caratteristiche dei dati. I dati in formato stringa sono contenuti in genere negli attributi di dimensione che rappresentano nomi o descrizioni, ma possono essere presenti anche nelle misure totale valori distinti o essere utilizzati nelle chiavi.  
  
 È possibile identificare un archivio di stringhe in base all'estensione file (ad esempio, file con estensione asstore, bstore, ksstore o string). Per impostazione predefinita, ognuno di questi file è soggetto a un limite massimo di 4 GB. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]è possibile ignorare le dimensioni massime del file specificando un meccanismo di archiviazione alternativo che consente di aumentare le dimensioni dell'archivio di stringhe in base alle necessità.  
  
 Diversamente dall'architettura dell'archivio di stringhe predefinita che comporta un limite delle dimensioni fisiche del file, l'archivio di stringhe più ampio è basato su un numero massimo di stringhe. Il limite massimo per questo tipo di archivio è 4 miliardi di stringhe univoche o 4 miliardi di record, a seconda della condizione che si verifica per prima. L'archivio di stringhe più ampio consente di creare record di dimensioni pari, dove ogni record corrisponde a una pagina di 64 KB. Se si dispone di stringhe molto lunghe che non rientrano in un solo record, il limite effettivo sarà minore di 4 miliardi di stringhe.  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> Prerequisiti  
 È necessario disporre della versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]o di una versione successiva.  
  
 Per le dimensioni e le partizioni deve essere utilizzata l'archiviazione MOLAP.  
  
 Il livello di compatibilità del database deve essere impostato su 1100. Se è stato creato o distribuito un database usando [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] e la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]o una versione successiva, il livello di compatibilità del database è già impostato su 1100. Se è stato spostato un database creato in una versione precedente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in ssSQL11 o versione successiva, è necessario aggiornare il livello di compatibilità. Per database spostati ma non ridistribuiti è possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per impostare il livello di compatibilità. Per ulteriori informazioni, vedere [impostare il livello di compatibilità di un database multidimensionale &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
##  <a name="step-1-set-the-stringstorecompatiblitylevel-property-in-sql-server-data-tools"></a><a name="bkmk_step1"></a>Passaggio 1: impostare la proprietà StringStoreCompatiblityLevel in SQL Server Data Tools  
  
1.  Se si usa [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto contenente le dimensioni o le partizioni che si desidera modificare.  
  
2.  Per modificare l'archivio di stringhe per le dimensioni, aprire Esplora soluzioni. Fare doppio clic sulla dimensione per cui modificare l'archivio di stringhe.  
  
3.  Nel riquadro Attributi di Progettazione dimensioni assicurarsi che sia selezionato il nodo padre della dimensione, ad esempio, se la dimensione è Customers, selezionare Customers e non uno degli attributi figlio.  
  
4.  Nel riquadro Proprietà della sezione Avanzate impostare **StringStoresCompatibilityLevel** su **1100**. Ripetere questa procedura per le altre dimensioni che richiedono un archivio più ampio. In caso contrario, lasciare le dimensioni rimanenti sul valore **1050** .  
  
5.  Per le partizioni, aprire un cubo da Esplora soluzioni.  
  
6.  Fare clic sulla scheda Partizioni.  
  
7.  Espandere la partizione, selezionare la partizione che richiede capacità di memoria aggiuntiva, quindi modificare la proprietà **StringStoresCompatibilityLevel** .  
  
8.  Salvare il file.  
  
##  <a name="step-2-process-the-objects"></a><a name="bkmk_step2"></a>Passaggio 2: elaborare gli oggetti  
 La nuova architettura di archiviazione verrà utilizzata dopo l'elaborazione degli oggetti. Questa operazione consente di dimostrare anche la corretta risoluzione del problema relativo al vincolo dell'archivio in quanto l'errore, tramite cui era stata segnalata una precedente condizione di overflow dell'archivio di stringhe, non verrà più generato.  
  
-   In Esplora soluzioni fare clic con il pulsante destro del mouse sulla dimensione appena modificata e selezionare **Elabora**.  
  
 È necessario utilizzare l'opzione Elaborazione completa su ogni oggetto in cui viene utilizzata la nuova architettura dell'archivio di stringhe. Prima dell'elaborazione, assicurarsi di eseguire un'analisi di impatto sulla dimensione per controllare se anche per gli oggetti dipendenti è necessaria la rielaborazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti e approcci per l'elaborazione di &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)   
 [Elaborazione e modalità di archiviazione delle partizioni](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)   
 [Archiviazione di dimensioni](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)  
  
  
