---
title: Valutare gli oggetti di Database SAP ASE per la conversione (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e7d1b0b68835fe8b909369a87814a3d1c41e07d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240251"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>Valutazione degli oggetti di database SAP ASE per la conversione (SybaseToSQL)
Prima di caricare gli oggetti e la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL di Azure, è necessario determinare come complessità della migrazione e quanto tempo deve durare. SSMA è possibile creare un report di valutazione che mostra la percentuale di oggetti e le procedure che verranno convertite correttamente in [!INCLUDE[tsql](../../includes/tsql-md.md)]. SSMA consente inoltre di visualizzare i problemi specifici che possono causare errori di conversione.  
  
## <a name="create-assessment-reports"></a>Creare report di valutazione  
Quando si crea questo report di valutazione, SSMA converte gli oggetti di database SAP Adaptive Server Enterprise (ASE) selezionati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi SQL di Azure e quindi Mostra i risultati.  
  
**Per creare un report di valutazione**  
  
1.  Nel Visualizzatore metadati Sybase, selezionare i database che si desidera valutare.  
  
2.  Per omettere i singoli oggetti, deselezionare le caselle di controllo accanto agli oggetti che non si desidera valutare.  
  
3.  Fare doppio clic su **database**, quindi selezionare **crea Report**.  
  
    È inoltre possibile analizzare singoli oggetti facendo clic su un oggetto, e quindi selezionando **crea Report**.  
  
    SSMA Mostra lo stato di avanzamento nella barra di stato nella parte inferiore della finestra. Se il riquadro di Output è visibile, si noteranno anche eventuali messaggi correlati.  
  
    Una volta completata, la valutazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Sybase: Verrà visualizzata la finestra di Report di valutazione.  
  
## <a name="use-assessment-reports"></a>Usare i report di valutazione  
La finestra di Report di valutazione contiene tre riquadri:  
  
-   Il riquadro a sinistra contiene la gerarchia degli oggetti inclusi nel report di valutazione. È possibile esplorare la gerarchia e selezionare gli oggetti e categorie degli oggetti per visualizzare codice e le statistiche di conversione.  
  
-   Il contenuto del riquadro di destra varia in base quale elemento è selezionato nel riquadro sinistro.  
  
    Se si seleziona un gruppo di oggetti (ad esempio uno schema) o una tabella, nel riquadro a destra vengono visualizzati due riquadri. Il **statistiche di conversione** riquadro sono indicate le statistiche di conversione per gli oggetti selezionati. Il **oggetti in base a categorie** riquadro sono indicate le statistiche di conversione per l'oggetto o categorie di oggetti.  
  
    Se una stored procedure, una vista o un trigger è selezionata, il riquadro destro contiene le statistiche, il codice sorgente e codice di destinazione.  
  
    -   Nell'area superiore mostra le statistiche generali per l'oggetto. Potrebbe essere necessario espandere **statistiche** per visualizzare queste informazioni. 
    -   L'area di origine Mostra il codice sorgente dell'oggetto selezionato nel riquadro sinistro. Le aree evidenziate mostrano codice sorgente problematico.  
    -   L'area di destinazione Mostra il codice convertito. Testo di colore rosso Mostra messaggi di errore e codice problematici.  
  
-   Nel riquadro inferiore Mostra messaggi di conversione, raggruppati per numero di messaggi. Selezionare **errori**, **avvisi**, o **Info** per visualizzare le categorie di messaggi e quindi espandere un gruppo di messaggi. Fare clic su un singolo messaggio per selezionare l'oggetto nel riquadro sinistro e quindi visualizzare i dettagli nel riquadro di destra.  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>Analizzare i problemi di conversione tramite il report di valutazione  
Il **riquadri di statistiche di conversione** mostrano le statistiche di conversione. Se la percentuale per ogni categoria è inferiore al 100%, è necessario determinare il motivo per cui la conversione non riuscita.  
  
**Per visualizzare i problemi di conversione**  
  
1.  Creare il report di valutazione usando le istruzioni nella procedura precedente.  
  
2.  Nel riquadro sinistro, espandere le cartelle che hanno un'icona rossa di errore o schemi. Continuare a espandere gli elementi fino a quando non si seleziona un singolo elemento che non hanno superato la conversione.  
  
3.  Nella parte superiore del riquadro del codice sorgente, selezionare **problema successivo**.  
    Il codice problematico viene evidenziato, come è riportato il codice correlato nel **navigazione di destinazione** riquadro.  
  
4.  Esaminare i messaggi di errore e quindi determinare ciò che si desidera fare con l'oggetto che ha causato il problema di conversione:  
  
    -   Aggiornare la sintassi di ambiente del servizio App in SSMA. È possibile aggiornare la sintassi solo per le stored procedure e trigger. Per aggiornare la sintassi, selezionare l'oggetto nel riquadro di esplorazione di metadati di Sybase, scegliere il **SQL** scheda e quindi modificare il codice SQL. Quando ci si sposta dall'elemento, viene richiesto di salvare la sintassi aggiornata. Visualizzare gli errori segnalati per l'oggetto nel **Report** scheda.  
  
    -   Nell'ambiente del servizio App, è possibile modificare l'oggetto di ambiente del servizio app da rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [la connessione a Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL metadati Explorer e Visualizzatore metadati Sybase, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL di Azure ed eseguire la migrazione dei dati dall'ambiente del servizio app.
  
## <a name="next-steps"></a>Passaggi successivi  
[Conversione di oggetti di Database di ASE SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database SAP ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
