---
title: Creare e gestire origini dati condivise (Reporting Services in modalità integrata SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], shared data sources
- shared data sources [Reporting Services]
ms.assetid: 2d3428e4-a810-4e66-a287-ff18e57fad76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5eedb74dd5a24f40469b3ee6a4a24e97e6e59174
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109626"
---
# <a name="create-and-manage-shared-data-sources-reporting-services-in-sharepoint-integrated-mode"></a>Creare e gestire origini dati condivise (Reporting Services in modalità integrata SharePoint)
  Quando si esegue un report da una raccolta di SharePoint, le informazioni di connessione possono essere definite all'interno del report o in un file esterno collegato al report. Se le informazioni di connessione sono incorporate nel report, si parlerà di origine dati personalizzata. Se le informazioni di connessione sono definite in un file esterno, si parlerà di origine dati condivisa. Il file esterno può essere un file dell'origine dei dati del server di report (con estensione rsds) o un file di connessione dati (con estensione odc).  
  
 Un file rsds è simile a un file rds, ma dispone di uno schema diverso. Per creare un file rsds, è possibile pubblicare un file rds da Progettazione report o Progettazione modelli in una raccolta di SharePoint. Dal file rds originale verrà creato un nuovo file rsds. In alternativa, è possibile creare un nuovo file nella raccolta di un sito di SharePoint.  
  
 Dopo avere creato o pubblicato un'origine dei dati condivisa, è possibile modificare le proprietà di connessione o eliminare il file nel caso non venga più utilizzato. Prima di eliminare un'origine dei dati condivisa, è necessario verificare se viene utilizzata da report e modelli di report. A tale scopo, visualizzare gli elementi dipendenti che fanno riferimento all'origine dei dati condivisa.  
  
 L'elenco degli elementi dipendenti, tuttavia, indica se viene fatto riferimento all'origine dei dati condivisa, ma non se quest'ultima viene utilizzata attivamente. Per determinare se l'origine dati condivisa o il modello viene utilizzato attivamente, è possibile esaminare i file di registro sul server di report. Se non si dispone dell'accesso ai file di log o se tali file non contengono le informazioni desiderate, provare a spostare il report in una cartella inaccessibile mentre se ne determina lo stato effettivo.  
  
### <a name="to-create-a-shared-data-source-rsds-file-sharepoint-2010"></a>Per creare un'origine dati condivisa (file RSDS) (SharePoint 2010)  
  
1.  Nella barra multifunzione della libreria fare clic sulla scheda **Documenti** .  
  
2.  Scegliere **Origine dati report** dal menu **Nuovo documento**.  
  
    > [!NOTE]  
    >  Se la voce **Origine dati report** non compare nel menu, il tipo di contenuto dell'origine dati del report non è stato abilitato. Per ulteriori informazioni, vedere [aggiungere tipi di contenuto del server di report a una raccolta &#40;Reporting Services in modalità integrata SharePoint&#41;](../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  In **Nome**immettere un nome descrittivo per il file con estensione rsds.  
  
4.  Scegliere il tipo di origine dati dall'elenco **Tipo di origine dati**. Per altre informazioni, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
5.  In **Stringa di connessione**specificare un puntatore all'origine dati e qualsiasi altra impostazione necessaria per stabilire una connessione all'origine dati esterna. La sintassi della stringa di connessione è determinata dal tipo di origine dei dati che si sta utilizzando. Per ulteriori informazioni ed esempi, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
6.  In **Credenziali**specificare la modalità con cui il server di report ottiene le credenziali per l'accesso all'origine dati esterna. Le credenziali possono essere archiviate, richieste al momento dell'esecuzione, integrate o configurate per l'elaborazione automatica del report.  
  
    -   Selezionare **Autenticazione di Windows (integrata)** se si desidera accedere ai dati usando le credenziali dell'utente che ha aperto il report. Non selezionare questa opzione se il sito o la farm di SharePoint utilizza l'autenticazione basata su form o si connette al server di report tramite un account attendibile. Non selezionare questa opzione se si desidera pianificare una sottoscrizione o l'elaborazione di dati per il report. È consigliabile utilizzare questa opzione quando per il dominio è abilitata l'autenticazione Kerberos oppure quando l'origine dei dati si trova nello stesso computer del server di report. Se l'autenticazione Kerberos non è attivata, le credenziali di Windows possono essere passate a un solo altro computer. Ciò significa che se l'origine dei dati esterna è in un altro computer, e richiede pertanto una connessione aggiuntiva, al posto dei previsti verrà restituito un errore.  
  
    -   Selezionare **Richiedi credenziali** se si vuole che l'utente immetta le proprie credenziali ogni volta che esegue il report. Non selezionare questa opzione se si desidera pianificare una sottoscrizione o l'elaborazione di dati per il report.  
  
    -   Selezionare **Credenziali archiviate** se si preferisce accedere ai dati usando un unico set di credenziali. Le credenziali vengono crittografate prima dell'archiviazione. È possibile selezionare opzioni che determinano la modalità di autenticazione delle credenziali archiviate. Selezionare Usa come credenziali di Windows se le credenziali archiviate appartengono all'account utente di Windows. Selezionare **Imposta contesto di esecuzione sull'account seguente** se si desidera impostare il contesto di esecuzione sul server di database. Nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] questa opzione consente di impostare la funzione SETUSER. Per altre informazioni, vedere [SETUSER &#40;Transact-SQL&#41;](/sql/t-sql/statements/setuser-transact-sql).  
  
    -   Selezionare **Credenziali non necessarie** se si preferisce specificare le credenziali nella stringa di connessione o eseguire il report usando un account con privilegi minimi configurato nel server di report. Se questo account non è configurato nel server di report, verrà visualizzato un messaggio di richiesta delle credenziali ed eventuali operazioni pianificate definite per il report non verranno eseguite.  
  
7.  Selezionare **Abilita questa origine dati** se si desidera che l'origine dati sia attiva. Se l'origine dati è configurata, ma non attiva, verrà visualizzato un messaggio di errore quando si tenta di utilizzare un report basato sull'origine dati.  
  
8.  Fare clic sul pulsante **Test connessione** per convalidare la configurazione dell'origine dati.  
  
    > [!NOTE]  
    >  Il pulsante Test connessione non è supportato per il tipo di origine dati XML.  
  
9. Fare clic su **OK** per salvare l'origine dati condivisa.  
  
### <a name="to-view-dependent-items"></a>Per visualizzare elementi dipendenti  
  
1.  Aprire la raccolta che contiene il file rsds.  
  
2.  Posizionare il puntatore del mouse sull'origine dei dati condivisa.  
  
3.  Fare clic per visualizzare una freccia verso il basso e quindi selezionare **Visualizza elementi dipendenti**.  
  
     Per i modelli di report, nell'elenco degli elementi dipendenti sono visualizzati i report creati in Generatore report. L'elenco degli elementi dipendenti relativo alle origini dei dati condivise può includere sia i report che i modelli di report.  
  
### <a name="to-delete-a-shared-data-source-rsds-file"></a>Per eliminare il file rsds dell'origine dei dati condivisa  
  
1.  Aprire la raccolta che contiene il file rsds.  
  
2.  Posizionare il puntatore del mouse sull'origine dei dati condivisa.  
  
3.  Fare clic per visualizzare una freccia verso il basso e quindi selezionare **Elimina**.  
  
 Se si elimina accidentalmente un'origine dei dati condivisa che invece si desidera conservare, è possibile crearne una nuova contenente le stesse informazioni di connessione. Dopo avere ricreato l'origine dati condivisa, è necessario aprire tutti i report e i modelli che la utilizzano, quindi selezionarla. Il nome, le credenziali o la sintassi della stringa di connessione della nuova origine dati possono essere diversi da quelli dell'origine dati eliminata. Le proprietà dell'origine dati possono avere valori diversi da quelli originali, purché la connessione venga risolta nella stessa origine dati.  
  
 Quando si elimina un modello di report è necessario prestare molta attenzione. Se si elimina un modello, non sarà più possibile aprire e modificare in Generatore report alcun report basato su tale modello. Se si elimina accidentalmente un modello utilizzato da report esistenti, sarà necessario rigenerare il modello, ricreare e salvare tutti i report che utilizzano il modello, quindi specificare di nuovo le impostazioni di sicurezza di tutti gli elementi del modello che si desidera utilizzare. Non è possibile rigenerare semplicemente il modello e collegarlo a un report esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
