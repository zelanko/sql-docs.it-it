---
title: Valutazione dei database MySQL per la conversione (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9983edb500e424be6bbb4f85ff005af00fd65aaf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253245"
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>Valutazione dei database MySQL per la conversione (MySQLToSQL)
Prima di caricare gli oggetti e la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è necessario determinare come complessa la migrazione sarà e quanto tempo richiederà la migrazione. SSMA è possibile creare un report di valutazione che mostra la percentuale di oggetti che verranno convertite correttamente. SSMA consente inoltre di visualizzare i problemi specifici che provocano errori di conversione.  
  
## <a name="creating-assessment-reports"></a>Creazione di report di valutazione  
Durante la creazione di questo report di valutazione, SSMA converte gli oggetti di database MySQL selezionati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di SQL Azure e quindi Mostra i risultati.  
  
**Per creare un report di valutazione**  
  
1.  Nel Visualizzatore metadati di MySQL, selezionare gli schemi da valutare.  
  
2.  Per omettere i singoli oggetti, deselezionare le caselle di controllo accanto a quelli.  
  
3.  Fare doppio clic su **schemi**, quindi selezionare **crea Report**.  
  
    Fare doppio clic su un oggetto per analizzare singoli oggetti. Quindi, selezionare **crea Report**.  
  
    SSMA mostrerà lo stato di avanzamento nella barra di stato nella parte inferiore della finestra. Se il riquadro di Output è visibile, si noteranno anche messaggi nel riquadro di Output.  
  
    Una volta completata, la valutazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per MySQL, finestra di Report di valutazione verrà visualizzato.  
  
## <a name="using-assessment-reports"></a>Uso dei report di valutazione  
La finestra di Report di valutazione contiene tre riquadri:  
  
-   Il riquadro a sinistra contiene la gerarchia degli oggetti inclusi nel report di valutazione. È possibile esplorare la gerarchia e selezionare gli oggetti e le categorie degli oggetti da visualizzare codice e le statistiche di conversione.  
  
-   Il contenuto del riquadro di destra dipende l'elemento selezionato nel riquadro sinistro.  
  
    Se si seleziona un gruppo di oggetti, ad esempio lo schema, il riquadro destro contiene un riquadro delle statistiche di conversione e gli oggetti dal riquadro delle categorie. Riquadro statistiche di conversione sono indicate le statistiche di conversione per gli oggetti selezionati. Gli oggetti dal riquadro delle categorie sono indicate le statistiche di conversione per l'oggetto o categorie di oggetti.  
  
    Se è selezionata una funzione, procedura, vista o tabella, il riquadro destro contiene le statistiche, il codice sorgente e codice di destinazione.  
  
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
  
4.  Esaminare eventuali messaggi di errore e quindi determinare ciò che si desidera fare con l'oggetto che ha causato il problema di conversione.  
  
-   Aggiornare la sintassi di MySQL in SSMA. È possibile aggiornare la sintassi solo per procedure e funzioni. Per aggiornare la sintassi, selezionare l'oggetto nel riquadro di esplorazione di metadati di MySQL, scegliere il **SQL** scheda e quindi modificare il codice SQL. Quando ci si sposta dall'elemento, verrà richiesto di salvare la sintassi aggiornata. È possibile visualizzare gli errori segnalati per l'oggetto nella **Report** scheda.  
  
-   In MySQL, è possibile modificare l'oggetto di MySQL per rimuovere o modificare il codice problematico. Per caricare il codice aggiornato in SSMA, è necessario aggiornare i metadati. Per altre informazioni, vedere [connessione a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   È possibile escludere l'oggetto dalla migrazione. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure i metadati Explorer e Visualizzatore metadati di MySQL, deselezionare la casella di controllo accanto all'elemento prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure ed eseguire la migrazione dei dati da MySQL.  
  
## <a name="next-step"></a>Passaggio successivo  
[Conversione dei database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
