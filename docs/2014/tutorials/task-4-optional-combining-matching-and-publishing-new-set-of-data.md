---
title: 'Attività 4 (facoltativo): combinazione, corrispondenza e pubblicazione di un nuovo set di dati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2d27a5bcd87ffd84b33de229d955dc9494846a72
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489277"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Attività 4 (facoltativa): Combinazione, corrispondenza e pubblicazione di un nuovo set di dati
  Con il tempo, sarà necessario aggiungere ulteriori dati al repository MDS. Prima di aggiungere i dati, può essere utile confrontare i nuovi dati con quelli già gestiti in MDS, per assicurarsi che non si stiano aggiungendo dati duplicati o non accurati. Nel componente aggiuntivo Master Data Services per Excel è possibile combinare i dati di due fogli di lavoro e confrontarli per identificare e rimuovere i duplicati prima di pubblicare i dati in MDS. Per identificare le corrispondenze nei dati viene utilizzata la funzionalità di corrispondenza di DQS dalla relativa caratteristica del componente aggiuntivo MDS per Excel. In questa attività verranno combinati i dati di due fogli di lavoro in uno e, successivamente, verrà eseguita l'attività di individuazione delle corrispondenze per identificare e rimuovere i duplicati prima della pubblicazione in MDS. Per ulteriori informazioni, vedere la pagina relativa alla [corrispondenza Data Quality nell'componente aggiuntivo MDS per Excel](https://msdn.microsoft.com/library/hh548681.aspx) e [combinare i dati](https://msdn.microsoft.com/library/hh548680.aspx) .  
  
1.  Avviare una nuova istanza di **Excel**. Fare clic sul pulsante **Start**, scegliere **Esegui**, digitare **Excel**, quindi fare clic su **OK**.  
  
2.  Passare alla scheda **dati master** facendo clic su **dati master** sulla barra dei menu.  
  
3.  Fare clic su **Connetti** sulla barra multifunzione nel gruppo **Connetti e carica** per connettersi al **Server MDS**. Questa connessione è stata configurata in precedenza nel corso della lezione.  
  
     ![Excel - Pulsante Esplora dati master nella scheda Dati master](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - Pulsante Esplora dati master nella scheda Dati master")  
  
4.  Il riquadro **Esplora dati master** verrà visualizzato a destra. Se il Esplora dati master non viene visualizzato, fare clic sul pulsante **Mostra Esplora** sulla barra multifunzione.  
  
5.  Nella finestra **Esplora dati master** selezionare **Suppliers** nell'elenco a discesa del **modello**. Si noterà che il modello ha un'entità: **Supplier**.  
  
     ![Excel - Finestra Esplora dati master](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - Finestra Esplora dati master")  
  
6.  Fare doppio clic su **Supplier** nell'elenco di entità per caricare i membri dell'entità nel foglio di lavoro di Excel.  
  
7.  Fare clic su **Sheet2** nella parte inferiore per passare alla scheda **Sheet2** . Se **Sheet2**non è visualizzato, aggiungere un nuovo foglio di foglio.  
  
8.  Aprire il file **Suppliers. xls** (il file di input originale incluso nei file dell'esercitazione) e copiare tutte le righe (tre) dal foglio di **CombineAndCleanse** in **Sheet2**.  
  
9. Tornare alla scheda **Supplier** nel **libro 1-Microsoft Excel** (non l'elenco dei **fornitori puliti e corrispondenti** Excel) connesso a **MDS**.  
  
10. Fare clic su **dati master** sulla barra dei menu.  
  
11. Fare clic su **combina dati** sulla barra multifunzione. Viene visualizzata la finestra di dialogo **combina dati** .  
  
12. Nella finestra di dialogo **combina dati** fare clic sul pulsante accanto alla casella **di testo intervallo da combinare con dati MDS** , come illustrato nella figura seguente.  
  
     ![Excel - Finestra di dialogo Combina dati](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - Finestra di dialogo Combina dati")  
  
13. A questo punto viene visualizzata la finestra di dialogo ridotta. A questo punto, fare clic su **Sheet2** per passare alla scheda **Sheet2** con i nuovi dati fornitore con 4 righe (inclusa una riga di intestazione).  
  
14. In **Sheet2**, selezionare **tutte le righe che includono la riga di intestazione** (anche se sembrano essere già selezionate). Si noterà che l' **intervallo da combinare con i dati MDS** viene aggiornato automaticamente.  
  
     ![Excel - Finestra di dialogo Combina dati - Ridotta](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - Finestra di dialogo Combina dati - Ridotta")  
  
15. Tornare alla scheda **Suppliers** senza chiudere la finestra di dialogo **combina dati** .  
  
16. Fare clic sul **pulsante** accanto alla **casella di testo**. A questo punto viene visualizzata la finestra di dialogo espansa. Si noterà che tutti i mapping tra le colonne dell' **entità** MDS **Supplier** e le colonne di **Excel** vengono popolati automaticamente.  
  
     ![Excel - Finestra di dialogo Combina dati con dati inclusi](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - Finestra di dialogo Combina dati con dati inclusi")  
  
17. Verificare che sia stato eseguito il mapping della colonna entità **codice** alla colonna **SupplierID** del foglio di codice e che sia stato eseguito il **mapping della colonna** di **entità Cap alla** colonna CAP del foglio di file.  
  
18. Nella finestra di dialogo **combina dati** fare clic su **combina**.  
  
19. Verificare che nella parte inferiore del foglio di calcolo sono state aggiunte tre righe di dati e che sono codificate tramite colori.  
  
     ![Excel - Nuovi elementi dopo la combinazione](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - Nuovi elementi dopo la combinazione")  
  
20. Fare clic su **dati matematici** sulla barra multifunzione per identificare i duplicati. Per questa caratteristica viene utilizzata la funzionalità di corrispondenza di DQS.  
  
21. Nella finestra di dialogo **corrispondenza dati** selezionare **Suppliers** per la **Knowledge Base DQS**.  
  
     ![Excel - Finestra di dialogo Abbina dati](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - Finestra di dialogo Abbina dati")  
  
22. Eseguire il mapping delle colonne del foglio di lavoro ai domini come illustrato nella tabella riportata di seguito.  
  
    |Colonna del foglio di lavoro|Dominio|  
    |----------------------|------------|  
    |Code (è stato caricato Supplier ID come Code per l'entità Supplier in MDS)|Supplier ID|  
    |Name (è stato caricato Supplier Name come Name dell'entità Supplier in MDS)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. Selezionare **prerequisito** per il mapping delle colonne di **codice** .  
  
24. Immettere il **70%** come **peso** per **il nome del fornitore** e il **30%** come **peso** per il **messaggio di posta elettronica di contatto** , come illustrato nell'immagine.  
  
25. Fare clic su **OK**.  
  
26. Il processo di corrispondenza dovrebbe identificare un duplicato per il fornitore con **codice: S1**.  
  
     ![Excel - Risultati corrispondenti](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - Risultati corrispondenti")  
  
27. Selezionare la **riga duplicata (arancione)**, fare clic con il pulsante destro del mouse e scegliere **Elimina** per eliminare la riga.  
  
28. Eliminare la colonna **CLUSTER_ID** perché non è più necessaria.  
  
29. Fare clic su **pubblica** per pubblicare gli altri due nuovi record con i **codici S66** e **S57** in MDS.  
  
30. Nella finestra di dialogo **pubblica e annota** aggiungere un' **annotazione**e fare clic su **pubblica**.  
  
31. Passa all' **applicazione Web gestione dati master**.  
  
32. Nella home page verificare che **Suppliers** sia selezionato per il **modello**, quindi fare clic su **Esplora**. Se **Esplora risorse** è già aperto, aggiornare il browser Internet.  
  
33. **Ordinare** l'elenco in base al **codice** e cercare i record con **S57** e **S66** come codici. È anche possibile usare il pulsante **filtro** sulla barra degli strumenti per cercare un record specifico nell'elenco.  
  
34. A questo punto, chiudere la finestra **di Book1-Microsoft Excel** senza salvare il file.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 5: Creazione di un attributo basato su dominio di Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
