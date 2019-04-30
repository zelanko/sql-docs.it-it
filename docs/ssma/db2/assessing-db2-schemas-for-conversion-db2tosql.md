---
title: Valutazione degli schemi DB2 per la conversione (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8892f5a4-72ba-4406-8649-7a9d67f4c1d9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fe66ff5b8902a737ff9a2ac0815069a4f01ea129
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63453428"
---
# <a name="assessing-db2-schemas-for-conversion-db2tosql"></a>Valutazione degli schemi DB2 per la conversione (DB2ToSQL)
Prima di caricare gli oggetti e la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario determinare come complessa la migrazione sarà e quanto tempo richiederà la migrazione. SSMA è possibile creare un report di valutazione che mostra la percentuale di oggetti che verranno convertite correttamente. SSMA consente inoltre di visualizzare i problemi specifici che provocano errori di conversione.  
  
## <a name="creating-assessment-reports"></a>Creazione di report di valutazione  
Durante la creazione di questo report di valutazione, SSMA converte gli oggetti di database DB2 selezionati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi e illustra i risultati.  
  
**Per creare un report di valutazione**  
  
1.  Nel Visualizzatore metadati DB2, selezionare gli schemi da valutare.  
  
2.  Per omettere i singoli oggetti, deselezionare le caselle di controllo accanto a quelli.  
  
3.  Fare doppio clic su **schemi**, quindi selezionare **crea Report**.  
  
    È inoltre possibile analizzare singoli oggetti facendo clic su un oggetto, e quindi selezionando **crea Report**.  
  
    SSMA mostrerà lo stato di avanzamento nella barra di stato nella parte inferiore della finestra. Se il riquadro di Output è visibile, si noteranno anche messaggi nel riquadro di Output.  
  
    Una volta completata, la valutazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per DB2: Verrà visualizzata la finestra di Report di valutazione.  
  
## <a name="using-assessment-reports"></a>Uso dei report di valutazione  
La finestra di Report di valutazione contiene tre riquadri:  
  
-   Il riquadro a sinistra contiene la gerarchia degli oggetti inclusi nel report di valutazione. È possibile esplorare la gerarchia e selezionare gli oggetti e le categorie degli oggetti da visualizzare codice e le statistiche di conversione.  
  
-   Il contenuto del riquadro di destra dipende dall'elemento selezionato nel riquadro sinistro.  
  
    Se si seleziona un gruppo di oggetti, tale schema, o se viene selezionata una tabella, il riquadro destro contiene un riquadro delle statistiche di conversione e un oggetti dal riquadro delle categorie. Riquadro statistiche di conversione sono indicate le statistiche di conversione per gli oggetti selezionati. Gli oggetti dal riquadro delle categorie sono indicate le statistiche di conversione per l'oggetto o categorie di oggetti.  
  
    Se è selezionata una funzione, pacchetto, procedure, sequenza o visualizzazione, il riquadro destro contiene le statistiche, il codice sorgente e codice di destinazione.  
  
    -   Nell'area superiore mostra le statistiche generali per l'oggetto. Potrebbe essere necessario espandere **statistiche** per visualizzare queste informazioni.  
  
    -   L'area di origine Mostra il codice sorgente dell'oggetto selezionato nel riquadro sinistro. Le aree evidenziate mostrano codice sorgente problematico.  
  
    -   L'area di destinazione Mostra il codice convertito. Testo di colore rosso Mostra messaggi di errore e codice problematici.  
  
-   Nel riquadro inferiore Mostra messaggi di conversione, raggruppati per numero di messaggi. È possibile fare clic su **errori**, **avvisi**, o **Info** per visualizzare le categorie di messaggi e quindi espandere un gruppo di messaggi. Fare clic su un singolo messaggio per selezionare l'oggetto nel riquadro sinistro e visualizzarne i dettagli nel riquadro di destra.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>L'analisi dei problemi di conversione tramite il Report di valutazione  
Riquadro statistiche di conversione sono indicate le statistiche di conversione. Se la percentuale per ogni categoria è inferiore al 100%, è necessario determinare il motivo per cui la conversione non riuscita.  
  
**Per visualizzare i problemi di conversione**  
  
1.  Creare il report di valutazione usando le istruzioni nella procedura precedente.  
  
2.  Nel riquadro sinistro, espandere le cartelle che hanno un'icona rossa di errore o schemi. Continuare a espandere gli elementi fino a quando non si seleziona un singolo elemento che non hanno superato la conversione.  
  
3.  Nella parte superiore del riquadro del codice sorgente, fare clic su **problema successivo**.  
  
    Il codice problematico viene evidenziato, come è riportato il codice correlato nel riquadro di navigazione di destinazione.  
  
4.  Esaminare i messaggi di errore e quindi determinare ciò che si desidera fare con l'oggetto che ha causato il problema di conversione:  
  
    -   Aggiornare la sintassi di DB2 in SSMA. È possibile aggiornare la sintassi per procedure, funzioni, trigger, funzioni incluse nel pacchetto e le procedure nel pacchetto. Per aggiornare la sintassi, selezionare l'oggetto nel riquadro di esplorazione di metadati di DB2, scegliere il **SQL** scheda e quindi modificare il codice SQL. Quando ci si sposta dall'elemento, verrà richiesto di salvare la sintassi aggiornata. È possibile visualizzare gli errori segnalati per l'oggetto nella **Report** scheda.  
  
    -   In DB2, è possibile modificare l'oggetto di DB2 per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [ci si connette al Database DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
    -   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati ed Esplora i metadati di DB2, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire la migrazione dei dati da DB2.  
  
## <a name="next-step"></a>Passaggio successivo  
[Converting DB2 Schemas &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
