---
title: Creare un percorso attendibile per siti PowerPivot in Amministrazione centrale | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24a779a751ac93c4c132c2dbf8ae63987de2666a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208227"
---
# <a name="create-a-trusted-location-for-power-pivot-sites-in-central-administration"></a>Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Excel Services consente di specificare i percorsi che rappresentano repository validi per le cartelle di lavoro che vengono aperte in un server SharePoint. Questi percorsi vengono chiamati "percorsi attendibili" ed è possibile utilizzare impostazioni di configurazione diverse per ogni percorso attendibile creato. Per una distribuzione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, può essere utile creare un percorso attendibile per i siti che contengono cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per poter applicare le impostazioni che funzionano meglio per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] mantenendo le impostazioni predefinite per il resto della farm.  
  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario essere un amministratore del servizio o della farm per definire un URL come percorso attendibile.  
  
 È necessario conoscere l'indirizzo URL del sito di SharePoint contenente la raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o un'altra raccolta in cui sono archiviate le cartelle di lavoro. Per ottenere l'indirizzo, aprire il sito che contiene la raccolta, fare clic con il pulsante destro del mouse su **Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** , scegliere **Proprietà** e quindi copiare la prima parte dell'indirizzo (URL) che contiene il nome del server e il percorso del sito.  
  
##  <a name="overview"></a> Panoramica  
 Un'installazione iniziale di Excel Services specifica "http://" come percorso attendibile, pertanto, nel server, possono essere aperte cartelle di lavoro di qualsiasi sito della farm. Se è necessario un controllo più rigido sui percorsi considerati attendibili, è possibile creare nuovi percorsi attendibili che eseguono il mapping a siti specifici della farm, quindi variare le impostazioni e le autorizzazioni per ognuno.  
  
 La creazione di un nuovo percorso attendibile per siti che ospitano cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è utile soprattutto per mantenere i valori predefiniti per il resto della farm e applicare impostazioni diverse ottimali per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Ad esempio, un percorso attendibile ottimizzato per le cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] potrebbe avere una dimensione massima per le cartelle di lavoro pari a 50 MB, mentre il resto della farm usa il valore predefinito di 10 MB.  
  
 La creazione di un percorso attendibile è consigliata se si usano le librerie della raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per visualizzare in anteprima le cartelle di lavoro pubblicate e vengono visualizzati avvisi di aggiornamento dati invece dell'immagine di anteprima prevista. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] La raccolta esegue il rendering delle immagini di anteprima dei report e delle cartelle di lavoro usando i dati e le informazioni di presentazione all'interno del documento. Se l'opzione Avvisa in caso di aggiornamento è abilitata per un percorso attendibile, la raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] potrebbe non avere autorizzazioni sufficienti per eseguire l'aggiornamento, con conseguente visualizzazione di un errore al posto dell'immagine di anteprima. L'aggiunta di un sito che contiene la raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] come nuovo percorso attendibile può risolvere questo problema.  
  
##  <a name="create"></a> Creare un percorso attendibile per l'accesso ai dati Power Pivot  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sull'applicazione di servizio Excel Services.  
  
3.  Fare clic su **Posizioni attendibili file**.  
  
4.  Fare clic su **Aggiungi posizione attendibile file**.  
  
5.  Immettere l'URL di un sito che contiene una libreria della raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
6.  In Tipo percorso selezionare **Microsoft SharePoint Foundation**.  
  
    > [!IMPORTANT]  
    >  I tipi di percorsi UNC e HTTP non sono supportati per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
7.  Accettare tutte le impostazioni predefinite per le proprietà in Gestione sessioni, Proprietà cartella di lavoro e Comportamento calcolo.  
  
8.  In Proprietà cartella di lavoro impostare **Dimensioni massime cartella di lavoro** su **50**. In questo modo, il limite superiore per le dimensioni del file della cartella di lavoro viene allineato al limite superiore per i caricamenti del file nell'applicazione Web padre. Se le dimensioni delle cartelle di lavoro superano i 50 megabyte, è necessario aumentare ulteriormente il limite della dimensione del file. Per altre informazioni, vedere [Configurare le dimensioni massime di caricamento dei file &#40;PowerPivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
9. In Dati esterni verificare che l'opzione Impostazione dati esterni consentiti sia impostata su **Raccolte di connessioni dati attendibili e connessioni incorporate**. Questa impostazione è necessaria per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una cartella di lavoro.  
  
10. Anche in Dati esterni, per Avviso in caso di aggiornamento, deselezionare la casella di controllo **Attiva avviso di aggiornamento**. Se si deseleziona la casella di controllo, la raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] può ignorare i messaggi di avviso di routine e mostrare le immagini di anteprima di una cartella di lavoro.  
  
11. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta Power Pivot](http://msdn.microsoft.com/library/2a0db616-e08e-4062-aac8-979f8cad7794)   
 [Creare e personalizzare la Raccolta Power Pivot](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)   
 [Usare la Raccolta Power Pivot](../../analysis-services/power-pivot-sharepoint/use-power-pivot-gallery.md)  
  
  
