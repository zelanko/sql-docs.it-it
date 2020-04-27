---
title: Modelli DMX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bf7682ce42422efb0e47e4272e53933eba92a4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081555"
---
# <a name="dmx-templates"></a>Modelli DMX
  I modelli di data mining consentono di compilare rapidamente query sofisticate. Sebbene la sintassi generale per le query DMX sia ben documentata, l'utilizzo dei modelli semplifica la compilazione delle query facendo clic e scegliendo gli argomenti e le origini dati.  
  
## <a name="using-the-templates"></a>Utilizzo dei modelli  
  
1.  Nel client di data mining per Excel fare clic su **query**.  
  
2.  Nella pagina **iniziale** della procedura guidata fare clic su **Avanti**.  
  
3.  Nella pagina **selezionare modello**, fare clic su **Avanzate**.  
  
     **Suggerimento:** Se si intende creare una query di stima su un modello, è possibile selezionare prima il modello, quindi fare clic su **Avanzate**per popolare il modello con il nome del modello.  
  
4.  Nell' **Editor avanzato query di data mining**fare clic su **modelli DMX**e selezionare un modello.  
  
5.  Premere INVIO per caricare il modello nel riquadro Query DMX.  
  
6.  Continuare a fare clic sui collegamenti nel modello e quando viene visualizzata la finestra di dialogo, selezionare un output, un modello oppure un parametro appropriato.  
  
     Per le query di stima, scegliere il set di dati di input e successivamente eseguire il mapping delle colonne.  
  
7.  Fare clic su **modifica query** per passare alla visualizzazione dell'editor di testo e modificare manualmente la query.  
  
     Si noti tuttavia che se si passa a una nuova vista durante l'utilizzo dell'editor di query, le informazioni presenti nella vista precedente verranno cancellate. Prima di cambiare vista, salvare il lavoro svolto copiando e incollando le istruzioni DMX in un file separato.  
  
8.  Fare clic su **Fine**. Nella finestra di dialogo **Scegli destinazione** specificare il percorso in cui si desidera salvare il risultato. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Se un'istruzione è stata eseguita correttamente, l'istruzione DMX inviata al server viene registrata anche nella finestra di **traccia** . Per ulteriori informazioni sull'utilizzo della funzionalità Trace, vedere [trace &#40;client di data mining per&#41;Excel ](trace-data-mining-client-for-excel.md).  
  
 Per ulteriori informazioni su come utilizzare l'editor avanzato query di data mining, vedere [Query &#40;SQL Server componenti aggiuntivi Data mining&#41;](query-sql-server-data-mining-add-ins.md) e [Editor avanzato query di data mining](advanced-data-mining-query-editor.md).  
  
## <a name="list-of-dmx-templates"></a>Elenco dei modelli DMX  
 I seguenti modelli DMX sono inclusi nel client di data mining per Excel.  
  
 **Previsioni**  
  
 Utilizzare tali modelli per creare query di stima avanzate, comprese le query non supportate dalle procedure guidate nei componenti aggiuntivi, ad esempio le query che utilizzano tabelle annidate o origini dati esterne.  
  
-   Stime filtrate  
  
-   Stime nidificate filtrate  
  
-   Stime nidificate  
  
-   Stime singleton  
  
-   Stime standard  
  
-   Stime basate su serie temporali  
  
-   Query di stima TOP  
  
-   Query di stima TOP sulla tabella nidificata  
  
 **Crea**  
  
 Utilizzare tali modelli per compilare modelli o strutture dei dati personalizzati. Non si è limitati ai modelli supportati dalle procedure guidate: è possibile usare qualsiasi algoritmo data mining supportato dall'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a cui si è connessi, inclusi gli algoritmi plug-in.  
  
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
  
## <a name="see-also"></a>Vedi anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
