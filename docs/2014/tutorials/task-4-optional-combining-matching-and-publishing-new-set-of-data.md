---
title: 'Attività 4 (facoltativa): La combinazione, corrispondenza e pubblicazione di un nuovo Set di dati | Microsoft Docs'
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489277"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Attività 4 (facoltativa): Combinazione, corrispondenza e pubblicazione di un nuovo set di dati
  Con il tempo, sarà necessario aggiungere ulteriori dati al repository MDS. Prima di aggiungere dati, può essere utile confrontare i nuovi dati ai dati già gestiti in MDS, per verificare che non si stiano aggiungendo dati duplicati o non accurati. Nel componente aggiuntivo Master Data Services per Excel è possibile combinare i dati di due fogli di lavoro e confrontarli per identificare e rimuovere i duplicati prima di pubblicare i dati in MDS. Per identificare le corrispondenze nei dati viene utilizzata la funzionalità di corrispondenza di DQS dalla relativa caratteristica del componente aggiuntivo MDS per Excel. In questa attività verranno combinati i dati di due fogli di lavoro in uno e, successivamente, verrà eseguita l'attività di individuazione delle corrispondenze per identificare e rimuovere i duplicati prima della pubblicazione in MDS. Visualizzare [corrispondenza Data Quality nel componente aggiuntivo MDS per Excel](https://msdn.microsoft.com/library/hh548681.aspx) e [combina dati](https://msdn.microsoft.com/library/hh548680.aspx) argomenti per altri dettagli.  
  
1.  Avvia nuova istanza della **Excel**. Fare clic su **avviare**, scegliere **eseguire**, digitare **Excel**, fare clic su **OK**.  
  
2.  Passare al **dati Master** scheda, fare clic su **Master Data** nella barra dei menu.  
  
3.  Fare clic su **Connect** sulla barra multifunzione nel **Connetti e carica** gruppo a cui connettersi per il **server MDS**. Questa connessione è stata configurata in precedenza nel corso della lezione.  
  
     ![Excel - pulsante Esplora Mostra nella scheda dati master Master](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - pulsante Esplora Mostra nella scheda dati master Master")  
  
4.  Dovrebbero vedere le **Esplora dati Master** riquadro a destra. Se non viene visualizzato Esplora dati Master, fare clic su **Mostra Esplora** pulsante della barra multifunzione.  
  
5.  Nel **Esplora dati Master** finestra, selezionare **Suppliers** nell'elenco a discesa per il **modello**. Verificare che il modello disponga di un'entità: **Fornitore**.  
  
     ![Excel - finestra di Esplora dati Master](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - finestra di Esplora dati Master")  
  
6.  Fare doppio clic su **Supplier** nell'elenco delle entità per caricare i membri dell'entità del foglio di lavoro di Excel.  
  
7.  Fare clic su **Foglio2** nella parte inferiore per passare alle **Foglio2** scheda. Se non viene visualizzata **Foglio2**, aggiungere un nuovo foglio di lavoro.  
  
8.  Aprire **Suppliers. xls** file (originale file di input che è incluso nei file dell'esercitazione) e copiare tutte le righe (tre) delle **CombineAndCleanse** foglio di lavoro **Foglio2**.  
  
9. Tornare alla **Supplier** foglio nel **libro 1 - Microsoft Excel** (non il **Cleansed and Matched Supplier List** Excel) che è connesso a **MDS**.  
  
10. Fare clic su **dati Master** nella barra dei menu.  
  
11. Fare clic su **combinare i dati** sulla barra multifunzione. Verrà visualizzato il **combinare i dati** nella finestra di dialogo.  
  
12. Nel **combinare i dati** finestra di dialogo fare clic sul pulsante accanto a **intervallo da combinare con dati MDS** casella di testo, come illustrato nell'immagine seguente.  
  
     ![Excel - finestra di dialogo dati di combinare](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - finestra di dialogo dati di combinare")  
  
13. A questo punto viene visualizzata la finestra di dialogo ridotta. A questo punto, fare clic su **Foglio2** per passare alle **Foglio2** scheda con i nuovi dati fornitore con 4 righe (tra cui riga di uno intestazione).  
  
14. Nel **Foglio2**, selezionare **tutte le righe tra cui la riga di intestazione** (anche se sembrano essere già selezionate). Dovrebbero vedere le **intervallo da combinare con dati MDS** viene aggiornato automaticamente.  
  
     ![Excel - combinare finestra di dialogo dati - ridotta a icona](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - combinare finestra di dialogo dati - ridotta a icona")  
  
15. Tornare al **Suppliers** scheda senza chiudere il **combina dati** nella finestra di dialogo.  
  
16. Fare clic sui **sul pulsante** accanto al **casella di testo**. A questo punto viene visualizzata la finestra di dialogo espansa. Si dovrebbero vedere tutti i mapping tra colonne del **Supplier** MDS **entity** al **Excel** colonne popolate automaticamente.  
  
     ![Excel - finestra di dialogo di dati è occupata dai dati di combinare](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - finestra di dialogo di dati è occupata dai dati di combinare")  
  
17. Assicurarsi che **codice** colonna di entità è mappata al **SupplierID** colonna nel foglio di lavoro e **CAP** colonna di entità è mappata al **CAP** colonne nel foglio di lavoro.  
  
18. Nel **combinare i dati** finestra di dialogo, fare clic su **combinare**.  
  
19. Verificare che nella parte inferiore del foglio di calcolo sono state aggiunte tre righe di dati e che sono codificate tramite colori.  
  
     ![Excel - nuovi elementi dopo la combinazione](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - nuovi elementi dopo la combinazione")  
  
20. Fare clic su **abbina dati** sulla barra multifunzione per identificare i duplicati. Per questa caratteristica viene utilizzata la funzionalità di corrispondenza di DQS.  
  
21. Nel **abbina dati** finestra di dialogo **Suppliers** per **Knowledge Base DQS**.  
  
     ![Excel - finestra di dialogo dati di corrispondenza](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - finestra di dialogo di corrispondenza dei dati")  
  
22. Eseguire il mapping delle colonne del foglio di lavoro ai domini come illustrato nella tabella riportata di seguito.  
  
    |Colonna del foglio di lavoro|Dominio|  
    |----------------------|------------|  
    |Code (è stato caricato Supplier ID come Code per l'entità Supplier in MDS)|Supplier ID|  
    |Name (è stato caricato Supplier Name come Name dell'entità Supplier in MDS)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. Selezionare **prerequisito** per il **codice** mapping delle colonne.  
  
24. Immettere **70%** come la **peso** per **Supplier Name** e **30%** come il **peso** per **Contact Email** come illustrato nell'immagine.  
  
25. Fare clic su **OK**.  
  
26. Il processo di corrispondenza deve essere identificato un duplicato per il fornitore con **codice: S1**.  
  
     ![Excel - risultati corrispondenza](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - risultati corrispondenza")  
  
27. Selezionare il **riga duplicata (arancione)**, pulsante destro del mouse e scegliere **eliminare** per eliminare la riga.  
  
28. Eliminare il **CLUSTER_ID** colonna perché non più necessaria.  
  
29. Fare clic su **Publish** per la pubblicazione di altri due nuovi record con **codici S66** e **S57** a MDS.  
  
30. Nel **pubblicazione e annotazione** finestra di dialogo, aggiungere un' **annotazione**, fare clic su **Publish**.  
  
31. Passare al **applicazione Web gestione dati Master**.  
  
32. Nella home page, assicurarsi che **Suppliers** sia selezionata per il **modello**, fare clic su **Esplora**. Se si dispone già di **Explorer** aprire, aggiornare il browser internet.  
  
33. **Ordinamento** l'elenco in base **codice** e cercare i record con **S57** e **S66** come codici. È anche possibile usare la **filtro** pulsante sulla barra degli strumenti per cercare un record specifico nell'elenco.  
  
34. A questo punto, chiudere **Book1 - Microsoft Excel** finestra senza salvare il file.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 5: Creazione di un attributo basato su dominio da Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
