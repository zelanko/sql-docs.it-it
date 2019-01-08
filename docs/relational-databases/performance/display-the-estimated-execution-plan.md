---
title: Visualizzare il piano di esecuzione stimato | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f5f10a0a0fb1ce80ad8d6bc5018362669e7f26b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373003"
---
# <a name="display-the-estimated-execution-plan"></a>Visualizzazione del piano di esecuzione stimato
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento viene descritta la procedura per generare rappresentazioni grafiche di piani di esecuzione stimati mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando si generano piani di esecuzione stimati, le query o i batch [!INCLUDE[tsql](../../includes/tsql-md.md)] non vengono eseguiti. Un piano di esecuzione stimato non include quindi alcuna informazione di runtime, ad esempio le metriche relative all'utilizzo effettivo delle risorse o avvisi sul runtime. Il piano di esecuzione generato mostra invece le query che verrebbero usate con maggiore probabilità da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in caso di effettiva esecuzione e mostra le righe stimate esaminate dai diversi operatori nel piano.  
  
 Per utilizzare questa funzionalità, è necessario che gli utenti dispongano delle autorizzazioni appropriate relative all'esecuzione delle query [!INCLUDE[tsql](../../includes/tsql-md.md)] per le quali verrà generato un piano di esecuzione grafico, nonché dell'autorizzazione SHOWPLAN per tutti i database a cui fa riferimento la query.  
  
## <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Per visualizzare il piano di esecuzione stimato di una query  
  
1.  Scegliere **Query del Motore di database**nella barra degli strumenti. Per aprire una query esistente e visualizzare il piano di esecuzione stimato, è inoltre possibile fare clic sul pulsante **Apri file** della barra degli strumenti e individuare la query.  
  
2.  Immettere la query di cui si desidera visualizzare il piano di esecuzione stimato.  
  
3.  Scegliere **Visualizza piano di esecuzione stimato** dal menu **Query** oppure fare clic sul pulsante **Visualizza piano di esecuzione stimato** della barra degli strumenti. Il piano di esecuzione stimato verrà visualizzato nel riquadro Risultati della scheda **Piano di esecuzione** . 

    ![Pulsante del piano di esecuzione stimato nella barra degli strumenti](../../relational-databases/performance/media/estimatedexecplantoolbar.png "Pulsante del piano di esecuzione stimato nella barra degli strumenti")    

    Per visualizzare informazioni aggiuntive, posizionare il mouse sulle icone degli operatori logici e fisici e visualizzare la descrizione e le proprietà dell'operatore nella descrizione comando. In alternativa, è possibile visualizzare le proprietà dell'operatore nella finestra Proprietà. Se tale finestra non è visibile, fare clic con il pulsante destro del mouse su un operatore e scegliere **Proprietà**. Selezionare un operatore e visualizzare le relative proprietà.  

    ![Fare clic con il pulsante destro del mouse sull'operatore del piano per visualizzarne le proprietà](../../relational-databases/performance/media/planproperties.png "Fare clic con il pulsante destro del mouse sull'operatore del piano per visualizzarne le proprietà")    
  
4.  Per modificare la visualizzazione del piano di esecuzione, fare clic con il pulsante destro del mouse sul piano di esecuzione e scegliere **Zoom avanti**, **Zoom indietro**, **Personalizza zoom**o **Adatta alla finestra**. **Zoom avanti** e **Zoom indietro** consentono rispettivamente di ingrandire o ridurre il piano di esecuzione in base a valori di percentuale predefiniti. **Personalizza zoom** consente di definire un ingrandimento personalizzato per la visualizzazione, ad esempio 80 percento. **Adatta alla finestra** consente di ingrandire il piano di esecuzione per adattarlo al riquadro Risultati. In alternativa, usare una combinazione di tasto CTRL e rotellina del mouse per attivare lo **zoom dinamico**.  

5.  Per esplorare la visualizzazione del piano di esecuzione, usare le barre di scorrimento verticale e orizzontale oppure **fare clic e tenere premuto il pulsante del mouse su qualsiasi area vuota** del piano di esecuzione e **trascinare il mouse**. In alternativa, fare clic e tenere premuto il pulsante del mouse sul segno più (+) nell'angolo inferiore destro della finestra del piano di esecuzione per visualizzare una mappa in miniatura dell'intero piano di esecuzione.
 
> [!NOTE] 
> In alternativa, usare [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md) per restituire le informazioni del piano di esecuzione per ogni istruzione senza eseguirlo. Se usata in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], la scheda *Risultati* includerà un collegamento per l'apertura del piano di esecuzione in formato grafico.   
