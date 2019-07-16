---
title: Verify a Power Pivot for SharePoint Installation | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f047593657806b872aafdda802c9c85ac4526b56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209472"
---
# <a name="verify-a-power-pivot-for-sharepoint-installation"></a>Verificare un'installazione Power Pivot per SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Per amministrare un'istanza di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint installata in una farm di SharePoint, usare Amministrazione centrale SharePoint. Come minimo, è possibile controllare le pagine in Amministrazione centrale e nei siti di SharePoint per verificare che le funzionalità e i componenti server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] siano disponibili. Tuttavia, per verificare completamente un'installazione, è necessario disporre di una cartella di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] pubblicabile in SharePoint e accessibile da una raccolta. A scopo di test, è possibile pubblicare una cartella di lavoro di esempio già contenente dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e usarla per confermare la corretta configurazione dell'integrazione SharePoint.  

  
##  <a name="verifyinstall"></a> Verifica dell'integrazione con Amministrazione centrale  
 Per verificare l'integrazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] con Amministrazione centrale, eseguire queste operazioni:  
  
1.  Nel menu Start fare clic su **Tutti i programmi**, aprire Prodotti Microsoft SharePoint 2016 o Prodotti Microsoft SharePoint 2013 e fare clic su **Amministrazione centrale SharePoint 2016 o Amministrazione centrale SharePoint 2013**.  
  
2.  Immettere il nome utente e la password, quindi fare clic su **OK**.  
  
     Facoltativamente, è possibile modificare le impostazioni del browser per evitare di dover immettere un nome utente e una password a ogni apertura di Amministrazione centrale. Per aggiungere Amministrazione centrale come sito attendibile, effettuare le operazioni seguenti.  
  
    1.  In Internet Explorer fare clic su **Opzioni Internet**dal menu Strumenti.  
  
    2.  Nella scheda Sicurezza della sezione **Selezionare l'area di cui visualizzare o modificare le impostazioni** fare clic su Siti attendibili, quindi su Siti.  
  
    3.  Deselezionare la casella di controllo **Richiedi verifica server (https:) per tutti i siti compresi nell'area** .  
  
    4.  In **Aggiungi il sito Web all'area**digitare l'URL al sito, quindi fare clic su **Aggiungi**.  
  
    5.  Fare clic su **Chiudi**, quindi su **OK**.  
  
        > [!NOTE]  
        >  Nella documentazione di installazione di SharePoint sono incluse istruzioni aggiuntive per risolvere errori del server proxy e per disabilitare Sicurezza avanzata di Internet Explorer, in modo da poter scaricare e installare aggiornamenti. Per altre informazioni, vedere la sezione **Operazioni successive all'installazione** in [Distribuire un server singolo con SQL Server](http://go.microsoft.com/fwlink/?LinkId=177754) sul sito Web Microsoft.  
  
3.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci funzionalità farm**.  
  
4.  Verificare che la **Funzionalità di integrazione[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** sia **Attiva**.  
  
5.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
6.  Verificare che il **Servizio di sistema[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] di SQL Server**  sia avviato.  
  
     In una farm SharePoint a più server potrebbe essere necessario cambiare il server visualizzato per verificare che tutti i server in cui è stato distribuito [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] siano in esecuzione.  
  
7.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
8.  Fare clic su **Applicazione di servizio[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] predefinita** per aprire il dashboard di gestione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per questa applicazione. Al primo utilizzo, il dashboard potrebbe impiegare diversi minuti per il caricamento.  
  
     In alternativa, fare clic sullo spazio vuoto accanto a **Applicazione di servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] predefinita** per selezionare la riga e su **Proprietà** per visualizzare le impostazioni di configurazione per questa applicazione di servizio. È possibile modificare sia le impostazioni di configurazione che le proprietà dell'applicazione per modificare la configurazione del server. Per altre informazioni, vedere [Creare e configurare un'applicazione del servizio Power Pivot](../../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="verify-integration-at-the-site-level"></a>Verifica dell'integrazione a livello di sito  
 Per verificare l'integrazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] con un sito di SharePoint, eseguire queste operazioni:  
  
1.  In un browser aprire l'applicazione Web creata. Se si usa valori predefiniti, è possibile specificare http://\<il nome computer > nell'indirizzo URL.  
  
2.  Verificare che le funzionalità di elaborazione e di accesso ai dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] siano disponibili nell'applicazione. È possibile eseguire questa operazione verificando la presenza di modelli di libreria forniti da [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]:  
  
    1.  Selezionare **Contenuto del sito**.  
  
    2.  L'elenco delle app dovrebbe includere **Libreria feed di dati** e **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Raccolta**. Questi modelli di raccolta vengono forniti dalla funzionalità [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e saranno visibili nell'elenco delle raccolte se la funzionalità è integrata correttamente.  
  
## <a name="verify-data-access-on-the-server"></a>Verifica dell'accesso a dati in un server  
 Per verificare l'accesso ai dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] nel server, eseguire queste operazioni:  
  
1.  [Scaricare](http://go.microsoft.com/fwlink/?LinkID=219108) i dati di esempio Picnic forniti con l'esercitazione Reporting Services. La cartella di lavoro di esempio contenuta in questo download sarà usata per verificare l'accesso ai dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Estrarre i file.  
  
2.  Caricare la cartella di lavoro di Excel (con estensione xlsx) in Documenti condivisi. La cartella di lavoro contiene dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] incorporati.  
  
3.  Fare clic sul documento per aprirlo dalla raccolta.  
  
4.  Fare clic su un filtro dei dati o un filtro nella parte superiore della cartella di lavoro. Mese, colore e tipo sono filtri dei dati in questa cartella di lavoro. Facendo clic su un filtro dei dati viene avviata una query [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , dimostrando che il server è operativo. Il server caricherà i dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in background e restituirà i risultati.  
  
5.  Tornare alla raccolta. Selezionare la freccia in giù a destra della cartella di lavoro, quindi fare clic su **Avvia Power View**. Con questo passaggio viene confermata l'operatività della funzionalità [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] in Reporting Services. Se Reporting Services non è stato installato, ignorare questo passaggio.  
  
     Nel passaggio successivo verrà effettuata la connessione al server in Management Studio per verificare che i dati vengano caricati e memorizzati nella cache.  
  
6.  Avviare SQL Server Management Studio dal gruppo di programmi [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] nel menu Start. Se questo strumento non è installato nel server, è possibile andare all'ultimo passaggio per confermare la presenza di file memorizzati nella cache.  
  
7.  In Tipo di server selezionare **Analysis Services**.  
  
8.  In nome Server immettere  **\<nome-server > \powerpivot.** , dove  **\<server-name >** è il nome del computer in cui è il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint installazione.  
  
9. Fare clic su **Connetti**. Viene verificata la disponibilità del server Analysis Services.  
  
10. In Esplora oggetti è possibile fare clic su **Database** per visualizzare l'elenco di file di dati [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] caricati.  
  
11. Nel file system del computer, controllare la cartella seguente per determinare se i file vengono memorizzati nella cache su disco. La presenza di file memorizzati nella cache è un'ulteriore verifica che la distribuzione è operativa. Per visualizzare la cache dei file, passare alla cartella [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]MSAS13.POWERPIVOT\OLAP\Backup\Sandboxes\Default [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Service Application. Ogni database memorizzato nella cache viene archiviato nella cartella corrispondente, utilizzando una convenzione di denominazione basata su GUID per assicurare un nome univoco.  
  
  
