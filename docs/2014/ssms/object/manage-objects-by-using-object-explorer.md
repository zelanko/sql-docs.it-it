---
title: Gestire oggetti tramite Esplora oggetti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ffd514fcdf5479f91e31d3bb5f261bba7ab4cd2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52809033"
---
# <a name="manage-objects-by-using-object-explorer"></a>Gestire oggetti tramite Esplora oggetti
  È possibile utilizzare Esplora oggetti per gestire oggetti quali database, tabelle e stored procedure.  
  
## <a name="viewing-objects-in-object-explorer"></a>Visualizzazione di oggetti in Esplora oggetti  
 In Esplora oggetti viene utilizzato un albero per raggruppare le informazioni in cartelle. Per espandere le cartelle, fare clic sul segno più (+) o fare doppio clic sulla cartella. Espandere le cartelle per visualizzare informazioni più dettagliate. Fare clic con il pulsante destro del mouse su cartelle o oggetti per eseguire attività comuni. Fare doppio clic sugli oggetti per eseguire le attività più comuni.  
  
 La prima volta che si espande una cartella, Esplora oggetti chiederà al server le informazioni per popolare l'albero. Durante il popolamento è possibile eseguire altre funzioni, ad esempio, fare clic su **Arresta** per arrestare il processo. Ulteriori azioni, ad esempio l'applicazione di filtri all'elenco, interesseranno solo la parte della cartella popolata, a meno che quest'ultima non venga aggiornata per iniziare di nuovo il popolamento.  
  
 Per risparmiare risorse nel caso in cui vi siano molti oggetti, l'elenco del contenuto delle cartelle nell'albero di Esplora oggetti non viene aggiornato automaticamente. Per aggiornare l'elenco degli oggetti all'interno di una cartella, fare clic con il pulsante destro del mouse sulla cartella e scegliere **Aggiorna**.  
  
 In Esplora oggetti è possibile visualizzare solo 65.536 oggetti. Superato questo limite, per scorrere gli altri oggetti nella visualizzazione dell'albero di Esplora oggetti chiudere i nodi inutilizzati o applicare filtri per ridurre il numero di oggetti.  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>Applicazione di filtri all'elenco degli oggetti in Esplora oggetti  
 Quando una cartella contiene moltissimi oggetti potrebbe essere difficile trovare quello desiderato. In questo caso utilizzare i filtri di Esplora oggetti per ridurre le dimensioni dell'elenco. Per trovare ad esempio un utente specifico di database o la tabella creata più di recente in elenchi che contengono centinaia di oggetti, fare clic sulla cartella alla quale applicare il filtro e sul pulsante del filtro per aprire la finestra di dialogo **Impostazioni filtro** . L'elenco può essere filtrato in base al nome, alla data di creazione e a volte anche in base allo schema. È inoltre possibile specificare altri operatori di filtro, ad esempio **Inizia con**, **Contiene**e **Compreso tra**.  
  
## <a name="multi-select"></a>Selezione multipla  
 In Esplora oggetti è possibile selezionare un solo oggetto alla volta. Per selezionare più elementi, premere **F7** per aprire la **pagina Dettagli di Esplora oggetti**. La **pagina Dettagli di Esplora oggetti** supporta la selezione multipla.  
  
## <a name="register-a-server-from-object-explorer"></a>Registrazione di un server da Esplora oggetti  
 Quando si è connessi a un server è facile registrarlo per utilizzi futuri. In Esplora oggetti fare clic con il pulsante destro del mouse sul nome del server e scegliere **Registra**. Nella finestra di dialogo **Registra server** specificare il punto dell'albero del gruppo in cui inserire il server. Nella casella **Nome server** è possibile sostituire il nome del server con un altro più significativo. Il server **APSQL02** , ad esempio, potrebbe venire registrato con un nome più significativo come "**Contabilità fornitori**".  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>Esecuzione di azioni sui nodi di Esplora oggetti  
 È possibile eseguire azioni sugli oggetti facendo clic con il pulsante destro del mouse sul nodo Esplora oggetti che rappresenta l'oggetto. Ogni tipo di oggetto supporta un set univoco di azioni con il pulsante destro del mouse. Alcuni dei tipi di azioni che è possibile eseguire tramite i menu di scelta rapida includono:  
  
### <a name="open-a-connected-query-editor"></a>Apertura di un editor di query connesso  
 Quando Esplora oggetti è connesso a un server, è possibile aprire una nuova finestra Editor del codice utilizzando le impostazioni di connessione di Esplora oggetti. Per aprire una nuova finestra Editor del codice, fare clic con il pulsante destro del mouse sul nome del server in Esplora oggetti e scegliere **Nuova query**. Per aprire una finestra Editor del codice usando un particolare database, fare clic con il pulsante destro del mouse sul nome del database e scegliere **Nuova query**. Quando viene aperta una nuova query per un server Analysis Services è possibile selezionare query DMX, MDX o XMLA.  
  
### <a name="start-powershell"></a>Avvio di PowerShell  
 È possibile avviare una sessione di PowerShell facendo clic con il pulsante destro del mouse sulla maggior parte delle cartelle e degli oggetti nell'albero di Esplora oggetti e scegliendo **Avvia PowerShell**. Verrà avviata una sessione di PowerShell in cui è abilitato il supporto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell e con il percorso impostato sull'oggetto su cui si è fatto clic con il pulsante destro del mouse in Esplora oggetti. È quindi possibile immettere comandi di PowerShell in un ambiente PowerShell interattivo. Per altre informazioni, vedere [SQL Server PowerShell](../../powershell/sql-server-powershell.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esplora oggetti](object-explorer.md)   
 [Aprire e configurare Esplora oggetti](open-and-configure-object-explorer.md)   
 [Connettersi a un'istanza da Esplora oggetti](connect-to-an-instance-from-object-explorer.md)   
 [Riquadro Dettagli Esplora oggetti](object-explorer-details-pane.md)   
 [Report personalizzati in Management Studio](custom-reports-in-management-studio.md)  
  
  
