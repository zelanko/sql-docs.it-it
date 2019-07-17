---
title: Valutazione degli schemi Oracle per la conversione (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0ff56be1b7da0376250c7ed021ae78d7144a7645
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264547"
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>Valutazione degli schemi Oracle per la conversione (OracleToSQL)
Prima di caricare gli oggetti e la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario determinare come complessa la migrazione sarà e quanto tempo richiederà la migrazione. SSMA è possibile creare un report di valutazione che mostra la percentuale di oggetti che verranno convertite correttamente. SSMA consente inoltre di visualizzare i problemi specifici che provocano errori di conversione.  
  
## <a name="creating-assessment-reports"></a>Creazione di report di valutazione  
Durante la creazione di questo report di valutazione, SSMA converte gli oggetti di database Oracle selezionati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi e illustra i risultati.  
  
**Per creare un report di valutazione**  
  
1.  Nel Visualizzatore metadati Oracle, selezionare gli schemi da valutare.  
  
2.  Per omettere i singoli oggetti, deselezionare le caselle di controllo accanto a quelli.  
  
3.  Fare doppio clic su **schemi**, quindi selezionare **crea Report**.  
  
    È inoltre possibile analizzare singoli oggetti facendo clic su un oggetto, e quindi selezionando **crea Report**.  
  
    SSMA mostrerà lo stato di avanzamento nella barra di stato nella parte inferiore della finestra. Se il riquadro di Output è visibile, si noteranno anche messaggi nel riquadro di Output.  
  
    Una volta completata, la valutazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Oracle: Verrà visualizzata la finestra di Report di valutazione.  
  
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
  
    -   Aggiornare la sintassi di Oracle in SSMA. È possibile aggiornare la sintassi per procedure, funzioni, trigger, funzioni incluse nel pacchetto e le procedure nel pacchetto. Per aggiornare la sintassi, selezionare l'oggetto nel riquadro di esplorazione di metadati di Oracle, scegliere il **SQL** scheda e quindi modificare il codice SQL. Quando ci si sposta dall'elemento, verrà richiesto di salvare la sintassi aggiornata. È possibile visualizzare gli errori segnalati per l'oggetto nella **Report** scheda.  
  
    -   In Oracle, è possibile modificare l'oggetto di Oracle per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [connessione a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
    -   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati ed Esplora i metadati di Oracle, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrare i dati da Oracle.  
  
## <a name="next-step"></a>Passaggio successivo  
[Conversione di schemi Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
