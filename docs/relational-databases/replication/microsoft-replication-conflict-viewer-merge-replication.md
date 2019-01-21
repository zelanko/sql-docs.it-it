---
title: Visualizzatore conflitti di replica Microsoft (replica di tipo merge) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.cvmerge.f1
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d27c90646aa8bae800780af97f9100427ccc06b6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124481"
---
# <a name="microsoft-replication-conflict-viewer-merge-replication"></a>Visualizzatore conflitti di replica Microsoft (Merge repliche)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Il Visualizzatore conflitti di replica consente di visualizzare tutti i conflitti verificatisi durante la sincronizzazione di repliche. Si verifica una situazione di conflitto quando gli stessi dati vengono modificati in due server distinti, ad esempio in un server di pubblicazione e in un Sottoscrittore oppure in due Sottoscrittori distinti. La replica risolve i conflitti automaticamente tramite il sistema di risoluzione dei conflitti selezionato al momento della creazione dell'articolo. Il Visualizzatore conflitti di replica consente tuttavia di scegliere una risoluzione dei conflitti diversa, se necessario. È possibile che si verifichino i conflitti seguenti:  
  
-   Conflitti di aggiornamento. Si verificano se vengono modificati gli stessi dati in due posizioni diverse. In questo caso, vengono confermate solo le modifiche apportate in una posizione. È possibile scegliere di mantenere i dati esistenti, ovvero i dati confermati, sovrascrivere i dati esistenti con quelli in conflitto, ovvero con i dati che non sono stati confermati, oppure unire i dati confermati e non confermati e aggiornare quelli esistenti.  
  
-   Conflitti di inserimento. Si verificano se viene inserita una riga in una posizione che viola una regola di coerenza dei dati al momento dell'unione con le modifiche apportate in altre posizioni. È possibile scegliere di mantenere i dati esistenti, ovvero i dati confermati, sovrascrivere i dati esistenti con quelli in conflitto, ovvero con i dati che non sono stati confermati, oppure unire i dati confermati e non confermati e aggiornare quelli esistenti.  
  
-   Conflitti di eliminazione. Si verificano se la stessa riga viene eliminata in una posizione e modificata in un'altra.  
  
 Se i conflitti vengono risolti durante la sincronizzazione, i dati della riga non confermata verranno scritti in una tabella di conflitti. La riga in conflitto registrata viene eliminata dalla tabella dei conflitti sia se si accetta la risoluzione dei conflitti originale, sia se si sceglie una risoluzione alternativa. È opportuno esaminare periodicamente i conflitti in modo da ridurre la dimensione delle tabelle di rivelamento dei conflitti.  
  
> [!NOTE]  
>  I conflitti a livello di record logici non vengono visualizzati nel Visualizzatore conflitti. Per visualizzare informazioni relative a questi conflitti, utilizzare le stored procedure di replica. Per altre informazioni, vedere [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
## <a name="options"></a>Opzioni  
 Il Visualizzatore conflitti di replica è suddiviso in due sezioni. Nella sezione superiore della finestra di dialogo vengono elencati i conflitti relativi alla tabella selezionata. Quando si fa clic su un elemento incluso nell'elenco dei conflitti, nella sezione inferiore della finestra di dialogo vengono visualizzati i dettagli del conflitto.  
  
 Le informazioni che descrivono la causa del conflitto, ad esempio, l'aggiornamento di una stessa riga sia nel server di pubblicazione che nel Sottoscrittore, vengono visualizzate nella sezione inferiore della finestra di dialogo. I dati del conflitto vengono visualizzati nella sezione inferiore in due colonne corrispondenti, ovvero**Riga in conflitto confermata** e **Riga in conflitto ignorata**. Se il conflitto si verifica tra dati aggiornati e dati eliminati, questi ultimi potrebbero non venire visualizzati. In questo caso, in una delle due colonne verrà visualizzato un messaggio per segnalare che la riga è stata eliminata in una posizione e aggiornata nell'altra. Verrà inoltre indicata la risoluzione suggerita.  
  
 I dati che non possono essere modificati nel Visualizzatore conflitti di replica, ad esempio i dati **rowguid** , vengono visualizzati in modalità di sola lettura con la casella inattiva.  
  
 **Database**  
 Consente di scegliere un database contenente pubblicazioni con conflitti.  
  
 **Pubblicazione**  
 Consente di scegliere una pubblicazione contenente tabelle con conflitti.  
  
 **Tabella**  
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
 Fare clic su questo pulsante per rimuovere i conflitti selezionati dal visualizzatore e i relativi metadati associati dalle tabelle del sistema di replica. Questa opzione è equivalente a fare clic sul pulsante Invia riga in conflitto confermata, senza alcuna modifica dei dati, per ogni conflitto selezionato.  
  
 **Mostra tutte le colonne**  
 Selezionare questa opzione per visualizzare tutte le colonne della tabella.  
  
 **Mostra le prime cinque colonne e le altre colonne con dati in conflitto**  
 Selezionare questa opzione per visualizzare le prime cinque colonne e tutte le colonne contenenti conflitti. Questa opzione risulta utile quando nella tabella sono presenti numerose colonne, ma si desidera visualizzare solo le colonne più significative per la risoluzione dei conflitti. Le prime cinque colonne vengono sempre visualizzate perché i campi di identificazione di una riga, ad esempio i campi del nome o della chiave primaria, sono solitamente inclusi tra le prime colonne della tabella.  
  
 **Visualizza informazioni sulla colonna** (**…**)  
 Fare clic per visualizzare le informazioni sulla colonna: **Nome tabella**, **Nome colonna**, **Tipo di dati** e **Valore colonna**. È possibile modificare**Valore colonna** , purché il valore non sia visualizzato in modalità di sola lettura.  
  
 **Invia riga in conflitto confermata**  
 Fare clic su questo pulsante per mantenere la riga confermata dal sistema di risoluzione dei conflitti. Prima di fare clic su questo pulsante, è possibile modificare il valore di ogni colonna non visualizzata come di sola lettura.  
  
 **Invia riga in conflitto ignorata**  
 Fare clic su questo pulsante per accettare la riga ignorata dal sistema di risoluzione dei conflitti. Prima di fare clic su questo pulsante, è possibile modificare il valore di ogni colonna non visualizzata come di sola lettura.  
  
 **Registra informazioni dettagliate sul conflitto**  
 Selezionare questa casella per registrare le informazioni dettagliate sul conflitto in un file. Per specificare il percorso del file, scegliere **Opzioni** dal menu **Visualizza**. Immettere un valore oppure fare clic sul pulsante **...** e spostarsi sul file appropriato. Fare clic su **OK** per chiudere la finestra di dialogo **Opzioni** .  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e risolvere i conflitti di dati per le pubblicazioni di tipo merge &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
