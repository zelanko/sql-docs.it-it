---
title: Modelli DMX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e3bee7fa85c98e50fdb940d2dfb23f76f3a462c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504686"
---
# <a name="dmx-templates"></a>Modelli DMX
  I modelli di data mining consentono di compilare rapidamente query sofisticate. Sebbene la sintassi generale per le query DMX sia ben documentata, l'utilizzo dei modelli semplifica la compilazione delle query facendo clic e scegliendo gli argomenti e le origini dati.  
  
## <a name="using-the-templates"></a>Utilizzo dei modelli  
  
1.  Nel Client di Data Mining per Excel, fare clic su **Query**.  
  
2.  Nella procedura guidata **avviare** pagina, fare clic su **successivo**.  
  
3.  Nella pagina **Seleziona modello**, fare clic su **avanzate**.  
  
     **Suggerimento:** Se si intende creare una query di stima su un modello, è possibile selezionare prima il modello e quindi fare clic su **avanzate**per prepopolare il modello con il nome del modello.  
  
4.  Nel **Advanced Query Editor di Data Mining**, fare clic su **modelli DMX**e selezionare un modello.  
  
5.  Premere INVIO per caricare il modello nel riquadro Query DMX.  
  
6.  Continuare a fare clic sui collegamenti nel modello e quando viene visualizzata la finestra di dialogo, selezionare un output, un modello oppure un parametro appropriato.  
  
     Per le query di stima, scegliere il set di dati di input e successivamente eseguire il mapping delle colonne.  
  
7.  Fare clic su **modifica Query** per passare alla visualizzazione dell'editor di testo e modificare manualmente la query.  
  
     Si noti tuttavia che se si passa a una nuova vista durante l'utilizzo dell'editor di query, le informazioni presenti nella vista precedente verranno cancellate. Prima di cambiare vista, salvare il lavoro svolto copiando e incollando le istruzioni DMX in un file separato.  
  
8.  Scegliere **Fine**. Nel **Scegli destinazione** finestra di dialogo, specificare dove si desidera salvare i risultati. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Se un'istruzione viene eseguita correttamente, l'istruzione DMX che è stato inviato al server verrà inoltre registrata il **traccia** finestra. Per altre informazioni su come usare la funzionalità di traccia, vedere [Trace &#40;Client di Data Mining per Excel&#41;](trace-data-mining-client-for-excel.md).  
  
 Per altre informazioni su come usare il Data Mining avanzato Editor di Query, vedere [Query &#40;componenti aggiuntivi Data Mining di SQL Server&#41; ](query-sql-server-data-mining-add-ins.md) e [avanzato Editor Query di Data Mining](advanced-data-mining-query-editor.md).  
  
## <a name="list-of-dmx-templates"></a>Elenco dei modelli DMX  
 I seguenti modelli DMX sono inclusi nel client di data mining per Excel.  
  
 **Stima**  
  
 Utilizzare tali modelli per creare query di stima avanzate, comprese le query non supportate dalle procedure guidate nei componenti aggiuntivi, ad esempio le query che utilizzano tabelle annidate o origini dati esterne.  
  
-   Stime filtrate  
  
-   Stime nidificate filtrate  
  
-   Stime nidificate  
  
-   Stime singleton  
  
-   Stime standard  
  
-   Stime basate su serie temporali  
  
-   Query di stima TOP  
  
-   Query di stima TOP sulla tabella nidificata  
  
 **Creare**  
  
 Utilizzare tali modelli per compilare modelli o strutture dei dati personalizzati. Non si è limitati ai modelli supportati dalle procedure guidate: è possibile utilizzare qualsiasi algoritmo di data mining supportato dall'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che è connessi, inclusi gli algoritmi plug-in.  
  
-   Modello di data mining  
  
-   Struttura di data mining  
  
-   Struttura di data mining con dati di controllo  
  
-   Modello temporaneo  
  
-   Struttura temporanea  
  
 **Proprietà dei modelli**  
  
 Utilizzare tali modelli per creare query che ottengono i metadati sul modello e il set di training. È inoltre possibile recuperare i dettagli dal contenuto del modello o ottenere un profilo statistico dei dati di training.  
  
-   Contenuto di modelli di data mining  
  
-   Valori di colonna minimo e massimo  
  
-   Case di testing/training struttura di data mining  
  
-   Valori di colonna discreti  
  
 **Gestione**  
  
 Utilizzare tali modelli per eseguire qualsiasi attività di gestione supportata da DMX, tra cui l'importazione e l'esportazione di modelli, l'eliminazione di modelli e la cancellazione di modelli o strutture dei dati.  
  
-   Cancella modello di data mining  
  
-   Cancella struttura e modelli  
  
-   Cancella struttura di data mining  
  
-   Elimina modello di data mining  
  
-   Elimina struttura di data mining  
  
-   Rinomina modello di data mining  
  
-   Rinomina struttura di data mining  
  
-   Training modello di data mining  
  
-   Training struttura di data mining nidificata  
  
-   Training struttura di data mining  
  
### <a name="requirements"></a>Requisiti  
 A seconda del modello utilizzato, potrebbero essere necessarie autorizzazioni amministrative per l'accesso al server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e l'esecuzione della query.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
