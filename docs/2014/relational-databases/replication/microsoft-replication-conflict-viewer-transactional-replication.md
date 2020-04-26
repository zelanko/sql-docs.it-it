---
title: Visualizzatore conflitti di replica Microsoft (replica transazionale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.cvqueued.f1
ms.assetid: eec59d8e-cadb-4623-a31f-9f42ec09c97f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 293048b191fff03b11b7e28d7778a34793b4c7f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62714868"
---
# <a name="microsoft-replication-conflict-viewer-transactional-replication"></a>Visualizzatore conflitti di replica Microsoft (replica transazionale)
  Il Visualizzatore conflitti di replica consente di visualizzare conflitti che si sono verificati durante la sincronizzazione per la replica transazionale peer-to-peer e la replica transazionale con sottoscrizioni ad aggiornamento in coda. Per altre informazioni, vedere [Visualizzare i conflitti di dati per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
> [!NOTE]  
>  Il Visualizzatore conflitti di replica consente di visualizzare i conflitti che si verificano nella replica di tipo merge e nella replica transazionale. Per la replica transazionale, è possibile utilizzare il Visualizzatore conflitti di replica per visualizzare i dati in conflitto, ma non è possibile scegliere una diversa risoluzione del conflitto.  
  
## <a name="options"></a>Opzioni  
 Il Visualizzatore conflitti di replica è suddiviso in due sezioni. Nella sezione superiore della finestra di dialogo vengono elencati i conflitti relativi alla tabella selezionata. Quando si fa clic su un elemento incluso nell'elenco dei conflitti, nella sezione inferiore della finestra di dialogo vengono visualizzati i dettagli del conflitto.  
  
 I dati del conflitto vengono visualizzati nella sezione inferiore in due colonne corrispondenti, ovvero**Riga in conflitto confermata** e **Riga in conflitto ignorata**. Se il conflitto si verifica tra dati aggiornati e dati eliminati, questi ultimi potrebbero non venire visualizzati. In questo caso, in una delle due colonne verrà visualizzato un messaggio per segnalare che la riga è stata eliminata in una posizione e aggiornata nell'altra. Verrà inoltre indicata la risoluzione suggerita.  
  
 **Database**  
 Consente di scegliere un database contenente pubblicazioni con conflitti.  
  
 **Pubblicazione**  
 Consente di scegliere una pubblicazione contenente tabelle con conflitti.  
  
 **tavolo**  
 Consente di scegliere una tabella contenente conflitti.  
  
 **Definisci filtro**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Definisci filtri** .  
  
 **Applica o rimuovi filtro**  
 Fare clic su questo pulsante per applicare o rimuovere un filtro definito nella finestra di dialogo **Definisci filtri** .  
  
 **Seleziona tutto**  
 Fare clic su questo pulsante per selezionare tutti i conflitti elencati nella griglia.  
  
 **Deseleziona tutto**  
 Fare clic su questo pulsante per deselezionare tutti i conflitti elencati nella griglia.  
  
 **Rimuovi**  
 Fare clic su questo pulsante per rimuovere i conflitti selezionati dal visualizzatore e i relativi metadati associati dalle tabelle del sistema di replica.  
  
 **Mostra tutte le colonne**  
 Selezionare questa opzione per visualizzare tutte le colonne della tabella.  
  
 **Mostra le prime cinque colonne e le altre colonne con dati in conflitto**  
 Selezionare questa opzione per visualizzare le prime cinque colonne e tutte le colonne contenenti conflitti. Questa opzione risulta utile quando nella tabella sono presenti numerose colonne, ma si desidera visualizzare solo le colonne più significative per la risoluzione dei conflitti. Le prime cinque colonne vengono sempre visualizzate perché i campi di identificazione di una riga, ad esempio i campi del nome o della chiave primaria, sono solitamente inclusi tra le prime colonne della tabella.  
  
 **Visualizza informazioni sulla colonna** (**...**)  
 Fare clic per visualizzare le informazioni sulla colonna, ovvero **Nome tabella**, **Nome colonna**, **Tipo di dati**e **Valore colonna**.  
  
 **Registra informazioni dettagliate sul conflitto**  
 Selezionare questa casella per registrare le informazioni dettagliate sul conflitto in un file. Per specificare il percorso del file, scegliere **Opzioni** dal menu **Visualizza**. Immettere un valore oppure fare clic sul pulsante **...** e spostarsi sul file appropriato. Fare clic su **OK** per chiudere la finestra di dialogo **Opzioni** .  
  
## <a name="see-also"></a>Vedi anche  
 [Rilevamento dei conflitti nella replica peer-to-peer](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Visualizzare i conflitti di dati per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
  
