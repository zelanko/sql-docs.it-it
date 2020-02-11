---
title: Verificare un'installazione di PowerPivot per SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 855bd055-5ad3-493f-9c5b-1f5297b2e6e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4ce1b1485885719bcd31cb085d43379239612d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079872"
---
# <a name="verify-a-powerpivot-for-sharepoint-installation"></a>Verifica di un'installazione PowerPivot per SharePoint
  Un'istanza di PowerPivot per SharePoint installata in una farm di SharePoint viene amministrata tramite Amministrazione centrale SharePoint. Come minimo, è possibile controllare le pagine in Amministrazione centrale e nei siti di SharePoint per verificare che le funzionalità e i componenti server PowerPivot siano disponibili. Tuttavia, per verificare completamente un'installazione, è necessario disporre di una cartella di lavoro di PowerPivot pubblicabile in SharePoint e accessibile da una raccolta. A scopo di test, è possibile pubblicare una cartella di lavoro di esempio contenente già dati PowerPivot e utilizzarla per confermare la corretta configurazione dell'integrazione SharePoint.  
  
##  <a name="verifyinstall"></a>Verificare l'integrazione di amministrazione centrale  
 Per verificare l'integrazione di PowerPivot con Amministrazione centrale, effettuare le operazioni seguenti:  
  
1.  Dal menu Start fare clic su **tutti i programmi**, aprire prodotti Microsoft SharePoint 2010, quindi fare clic su **amministrazione centrale SharePoint 2010**.  
  
2.  Immettere il nome utente e la password, quindi fare clic su **OK**.  
  
     Facoltativamente, è possibile modificare le impostazioni del browser per evitare di dover immettere un nome utente e una password a ogni apertura di Amministrazione centrale. Per aggiungere Amministrazione centrale come sito attendibile, effettuare le operazioni seguenti.  
  
    1.  In Internet Explorer scegliere **Opzioni Internet**dal menu strumenti.  
  
    2.  Nella scheda Sicurezza della sezione **Selezionare l'area di cui visualizzare o modificare le impostazioni** fare clic su Siti attendibili, quindi su Siti.  
  
    3.  Deselezionare la casella di controllo **Richiedi verifica server (https:) per tutti i siti compresi nell'area** .  
  
    4.  In **Aggiungi il sito Web all'area**digitare l'URL al sito, quindi fare clic su **Aggiungi**.  
  
    5.  Fare clic su **Chiudi** e quindi su **OK**.  
  
        > [!NOTE]  
        >  Nella documentazione di installazione di SharePoint sono incluse istruzioni aggiuntive per risolvere errori del server proxy e per disabilitare Sicurezza avanzata di Internet Explorer, in modo da poter scaricare e installare aggiornamenti. Per altre informazioni, vedere la sezione **Operazioni successive all'installazione** in [Distribuire un server singolo con SQL Server](https://go.microsoft.com/fwlink/?LinkId=177754) sul sito Web Microsoft.  
  
3.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci funzionalità farm**.  
  
4.  Verificare che **Funzionalità integrazione PowerPivot** sia **Attiva**.  
  
5.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
6.  Verificare che **SQL Server Analysis Services** e **Servizio di sistema PowerPivot di SQL Server** siano avviati.  
  
7.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
8.  Fare clic su **applicazione di servizio PowerPivot predefinita** per aprire il dashboard di gestione PowerPivot per questa applicazione. Al primo utilizzo, il dashboard potrebbe impiegare diversi minuti per il caricamento.  
  
     In alternativa, fare clic sullo spazio vuoto accanto a **applicazione di servizio PowerPivot predefinita** per selezionare la riga e fare clic su **Proprietà** per visualizzare le impostazioni di configurazione per questa applicazione di servizio. È possibile modificare sia le impostazioni di configurazione che le proprietà dell'applicazione per modificare la configurazione del server. Per ulteriori informazioni su queste impostazioni, vedere [creare e configurare un'applicazione di servizio PowerPivot in Amministrazione centrale](../../power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="verify-integration-at-the-site-level"></a>Verifica dell'integrazione a livello di sito  
 Per verificare l'integrazione di PowerPivot con un sito di SharePoint, effettuare le operazioni seguenti:  
  
1.  In un browser aprire l'applicazione Web creata. Se sono stati usati i valori predefiniti, è possibile\<specificare http://il nome del computer> nell'indirizzo URL.  
  
2.  Verificare che le funzionalità di elaborazione e di accesso ai dati PowerPivot siano disponibili nell'applicazione. È possibile effettuare questa operazione verificando la presenza di modelli di libreria forniti da PowerPivot:  
  
    1.  In azioni sito fare clic su **altre opzioni.**..  
  
    2.  Nelle librerie dovrebbero essere visualizzate la **libreria di feed di dati** e la **raccolta PowerPivot**. Questi modelli di raccolta vengono forniti dalla funzionalità PowerPivot e saranno visibili nell'elenco delle raccolte se la funzionalità è integrata correttamente.  
  
## <a name="verify-data-access-on-the-server"></a>Verifica dell'accesso a dati in un server  
 Per verificare l'accesso ai dati PowerPivot nel server, effettuare le operazioni seguenti:  
  
1.  [Scaricare](https://go.microsoft.com/fwlink/?LinkID=219108) l'esempio di dati picnic che accompagna un'esercitazione Reporting Services. La cartella di lavoro di esempio contenuta in questo download sarà utilizzata per verificare l'accesso ai dati PowerPivot. Estrarre i file.  
  
2.  Caricare la cartella di lavoro di Excel (con estensione xlsx) in Documenti condivisi. La cartella di lavoro contiene dati PowerPivot incorporati.  
  
3.  Fare clic sul documento per aprirlo dalla raccolta.  
  
4.  Fare clic su un filtro dei dati o un filtro nella parte superiore della cartella di lavoro. Mese, colore e tipo sono filtri dei dati in questa cartella di lavoro. Facendo clic su un filtro dei dati viene avviata una query PowerPivot, dimostrando che il server è operativo. I dati PowerPivot verranno caricati in background e verranno restituiti i risultati.  
  
5.  Tornare alla raccolta. Selezionare la freccia in giù a destra della cartella di lavoro, quindi fare clic su **Avvia Power View**. Con questo passaggio viene confermata l'operatività della funzionalità [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] in Reporting Services. Se Reporting Services non è stato installato, ignorare questo passaggio.  
  
     Nel passaggio successivo verrà effettuata la connessione al server in Management Studio per verificare che i dati vengano caricati e memorizzati nella cache.  
  
6.  Avviare SQL Server Management Studio dal gruppo di programmi [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] nel menu Start. Se questo strumento non è installato nel server, è possibile andare all'ultimo passaggio per confermare la presenza di file memorizzati nella cache.  
  
7.  In Tipo di server selezionare **Analysis Services**.  
  
8.  In nome server immettere ** \<nome-server> \powerpivot**, dove ** \<Server-Name>** è il nome del computer in cui è installato PowerPivot per SharePoint.  
  
9. Fare clic su **Connetti**. Viene verificata la disponibilità del server Analysis Services.  
  
10. In Esplora oggetti, è possibile fare clic su **database** per visualizzare l'elenco dei file di dati PowerPivot caricati.  
  
11. Nel file system del computer, controllare la cartella seguente per determinare se i file vengono memorizzati nella cache su disco. La presenza di file memorizzati nella cache è un'ulteriore verifica che la distribuzione è operativa. Per visualizzare la cache dei file, passare all' \<unità>: \Programmi\microsoft SQL Server\MSAS11. POWERPIVOT\OLAP\Backup\Sandboxes\Default cartella dell'applicazione di servizio PowerPivot. Ogni database memorizzato nella cache viene archiviato nella cartella corrispondente, utilizzando una convenzione di denominazione basata su GUID per assicurare un nome univoco.  
  
  
