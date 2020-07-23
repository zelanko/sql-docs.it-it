---
title: "Passaggio 4: Aggiungere un'attività Flusso di dati al pacchetto | Microsoft Docs"
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ba3ef8fe03b0f3057dbb443dfbf5ab257a70983
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917387"
---
# <a name="lesson-1-4-add-a-data-flow-task-to-the-package"></a>Lezione 1-4: Aggiungere un'attività Flusso di dati al pacchetto

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Dopo aver creato le gestioni connessioni per i dati di origine e di destinazione, è possibile aggiungere un'attività Flusso di dati al pacchetto. L'attività Flusso di dati definisce il motore del flusso di dati che gestisce lo spostamento dei dati tra origini e destinazioni, offrendo funzionalità di trasformazione, pulitura e modifica dei dati durante lo spostamento. Nell'attività Flusso di dati avviene gran parte del lavoro di un processo ETL (Extract, Transform and Load).  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa il flusso di dati dal flusso di controllo.  
  
## <a name="add-a-data-flow-task"></a>Aggiungere un'attività Flusso di dati  
  
1.  Selezionare la scheda **Flusso di controllo**.  
  
2.  Nel riquadro **Casella degli strumenti SSIS** espandere **Preferiti**, quindi trascinare un'**Attività Flusso di dati** sull'area di progettazione della scheda **Flusso di controllo**.  
  
    > [!NOTE]  
    > Se la casella degli strumenti SSIS non è disponibile, selezionare il menu **SSIS** e quindi selezionare **Casella degli strumenti SSIS** per visualizzarla.  

3.  Nell'area di progettazione **Flusso di controllo** fare clic con il pulsante destro del mouse sulla nuova **Attività Flusso di dati**, scegliere **Rinomina** e modificare il nome in **Extract Sample Currency Data**.  
  
    Specificare nomi univoci per tutti i componenti aggiunti a un'area di progettazione. Per facilità d'uso e manutenzione, i nomi dovrebbero descrivere la funzione di ogni componente. Se vengono applicate queste linee guida per la denominazione, i pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] avranno un nome descrittivo. Come descrizione dei pacchetti è inoltre possibile utilizzare le annotazioni. Per altre informazioni sulle annotazioni, vedere [Usare le annotazioni nei pacchetti](../integration-services/use-annotations-in-packages.md).  
  
4.  Fare clic con il pulsante destro del mouse sull'attività Flusso di dati, scegliere **Proprietà** e verificare che la proprietà **LocaleID** sia impostata su **Inglese (Stati Uniti)** nella finestra Proprietà.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 5: Aggiungere e configurare l'origine file flat](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Vedere anche  
[Attività Flusso di dati](../integration-services/control-flow/data-flow-task.md)  
  
  
  
