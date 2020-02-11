---
title: Impostare le proprietà di un componente flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc360da93b905bed20f118812898b5c029c570cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770747"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>Impostazione delle proprietà di un componente del flusso di dati
  Per impostare le proprietà dei componenti flusso di dati, tra cui origini, destinazioni e trasformazioni, utilizzare una delle funzionalità seguenti:  
  
-   Editor dei componenti forniti da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Gli editor includono solo le proprietà personalizzate di ogni componente flusso di dati.  
  
-   Nella finestra **Proprietà** sono elencate sia le proprietà personalizzate a livello di componente per ogni elemento, sia le proprietà comuni a tutti gli elementi del flusso di dati.  
  
-   La finestra di dialogo **Editor avanzato** consente l'accesso alle proprietà personalizzate di ciascun componente. La finestra di dialogo **Editor avanzato** consente anche di accedere alle proprietà comuni a tutti i componenti flusso di dati, ossia le proprietà degli input, degli output, degli output degli errori, delle colonne e delle colonne esterne.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>Per impostare le proprietà di un componente flusso di dati utilizzando l'editor del componente  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il flusso di dati con il componente di cui si desidera visualizzare e modificare le proprietà.  
  
4.  Fare doppio clic sul componente del flusso di dati.  
  
5.  Nell'editor del componente visualizzare o modificare i valori delle proprietà e quindi chiudere l'editor.  
  
6.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>Per impostare le proprietà di un componente flusso di dati utilizzando la finestra delle proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il componente di cui si desidera visualizzare e modificare le proprietà.  
  
4.  Fare clic con il pulsante destro del mouse sul componente flusso di dati, quindi scegliere **Proprietà**.  
  
5.  Visualizzare o modificare i valori delle proprietà, quindi chiudere la finestra **Proprietà** .  
  
    > [!NOTE]  
    >  Molte proprietà sono in sola lettura e non possono essere modificate.  
  
6.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>Per impostare le proprietà di un componente flusso di dati utilizzando l'editor avanzato  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il componente che si desidera visualizzare o modificare.  
  
4.  Nella finestra di progettazione del flusso di dati fare clic con il pulsante destro del mouse sul componente flusso di dati, quindi scegliere **Visualizza editor avanzato**.  
  
    > [!NOTE]  
    >  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]non è possibile utilizzare la finestra di dialogo **Editor avanzato**per i componenti flusso di dati che supportano più input.  
  
5.  Nella finestra di dialogo **Editor avanzato** eseguire una delle operazioni seguenti:  
  
    -   Fare clic sulla scheda **Gestioni connessioni** per visualizzare e specificare la connessione usata dal componente.  
  
        > [!NOTE]  
        >  La scheda **Gestioni connessioni** è disponibile solo per i componenti flusso di dati che utilizzano gestioni connessioni per connettersi a origini dati quali file e database.  
  
    -   Fare clic sulla scheda **Proprietà componente** per visualizzare e modificare le proprietà a livello di componente.  
  
    -   Fare clic sulla scheda **Mapping colonne** per visualizzare e modificare i mapping tra le colonne esterne e l'output disponibile.  
  
        > [!NOTE]  
        >  La scheda **Mapping colonne** è disponibile solo durante la visualizzazione o la modifica di origini o destinazioni.  
  
    -   Per visualizzare un elenco delle colonne di input disponibili e aggiornare i nomi delle colonne di output, fare clic sulla scheda **Colonne di input** .  
  
        > [!NOTE]  
        >  La scheda Colonne di input è disponibile solo quando si utilizzano trasformazioni o destinazioni. Per altre informazioni, vedere [Trasformazioni di Integration Services](transformations/integration-services-transformations.md).  
  
    -   Fare clic sulla scheda **Proprietà input e output** per visualizzare e modificare le proprietà degli input, degli output e degli output degli errori, nonché le proprietà delle colonne che contengono.  
  
        > [!NOTE]  
        >  Le origini non includono input, mentre le destinazioni non includono output, ad eccezione di un output degli errori facoltativo.  
  
6.  Visualizzare o modificare i valori delle proprietà.  
  
7.  Fare clic su **OK**.  
  
8.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazioni di Integration Services](transformations/integration-services-transformations.md)  
  
  
