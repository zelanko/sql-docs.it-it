---
title: Usare una connessione BI Semantic Model in Excel o Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 486195ca-530f-49e8-b40d-0f817db159ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a8e2b976fca00293d93cbf1e9987e115631bd81
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070924"
---
# <a name="use-a-bi-semantic-model-connection-in-excel-or-reporting-services"></a>Utilizzare una connessione BISM (BI Semantic Model) in Excel o Reporting Services
  In questo argomento viene illustrato come utilizzare le connessioni BISM create utilizzando le istruzioni in altri argomenti. Se non è ancora stato creato un modello BI Semantic Model, vedere [creare una connessione BI Semantic Model a una cartella di lavoro di PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md) e [creare una connessione BI Semantic Model a un database modello tabulare](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="connect-from-excel"></a><a name="bkmk_connect"></a> Connessione da Excel  
 È possibile specificare una connessione BISM come origine dati in Excel o in qualsiasi altra applicazione business in cui vengono utilizzati dati del modello tabulare di Analysis Services. In questa sezione vengono illustrati i due approcci per la connessione ai dati BISM utilizzando Excel.  
  
 Le connessioni BISM da Excel richiedono l'installazione di Excel 2010 e del provider OLE DB MSOLAP.5 nella workstation. Più avanti in questa sezione vengono fornite ulteriori informazioni sui requisiti della connessione.  
  
 **Avvio da SharePoint**  
  
-   Fare clic con il pulsante destro del mouse su una connessione BI Semantic Model in una raccolta e selezionare **Avvia Excel**.  
  
 ![Schermata del comando di avvio rapido BISM](../media/ssas-bism-quicklaunch.gif "Schermata del comando di avvio rapido BISM")  
  
 Fare clic su **Abilita** quando viene richiesto di abilitare le connessioni dati. In Excel verrà aperta una cartella di lavoro che contiene un elenco dei campi della tabella pivot in cui sono indicati i campi dell'origine dati sottostante.  
  
 **Avvio da Excel**  
  
1.  Avviare Excel e aprire una cartella di lavoro. In Recupera dati esterni della scheda Dati fare clic su **Da altre origini**.  
  
2.  Fare clic su **Da Analysis Services** e usare la Connessione guidata dati per importare i dati.  
  
3.  Immettere l'URL di SharePoint del file di connessione BI Semantic Model (ad esempio ** http://mysharepoint/shared Documents/Data. BISM**). Accettare l'opzione predefinita delle credenziali di accesso, **Usa autenticazione di Windows**. Fare clic su **Avanti**.  
  
4.  Nella pagina successiva fare clic di nuovo su **Avanti** . Anche se viene richiesto di selezionare un database, è possibile utilizzare solo quello specificato nella connessione BISM.  
  
5.  Nell'ultima pagina è possibile fornire un nome descrittivo e una descrizione. Fare clic su **Fine**e quindi fare clic su **OK** nella finestra di dialogo Importa dati per importare i dati.  
  
 Affinché le connessioni vengano eseguite correttamente, è necessario che sul computer client siano installati Excel 2010 e MSOLAP.5.dll. È possibile ottenere il provider installando la versione di PowerPivot per Excel corrente per questa versione oppure è possibile scaricare solo il provider di OLE DB Analysis Services dalla pagina di [download del Feature Pack](https://go.microsoft.com/fwlink/?linkid=214066).  
  
 Per verificare che MSOLAP.5.dll sia la versione corrente, verificare `HKEY_CLASSES_ROOT\MSOLAP` nel Registro di sistema. `CurVer` deve essere impostato su MSOLAP.5.  
  
 Inoltre, è necessario disporre delle autorizzazioni di lettura sul file BISM in SharePoint. In tali autorizzazioni sono inclusi i diritti di download. Excel consente di scaricare le informazioni sulla connessione BISM da SharePoint e di aprire una connessione diretta al database tramite `HTTP Get`. Le richieste di connessione non passano tramite SharePoint una volta archiviate in locale le informazioni sulla connessione BISM.  
  
 Se si è connessi a un database modello tabulare eseguito in un server Analysis Services, le autorizzazioni di SharePoint non sono sufficienti. È inoltre necessario disporre delle autorizzazioni di lettura sul server. È necessario che questo passaggio sia stato eseguito al momento della creazione della connessione BISM. Per altre informazioni, vedere [Creare una connessione BI Semantic Model a un database modello tabulare](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="connect-from-reporting-services-in-sharepoint"></a><a name="bkmk_use"></a> Connessione da Reporting Services in SharePoint  
 È possibile utilizzare una connessione BISM con la stessa modalità con cui si utilizzano la maggior parte delle origini dati, specificando il file come origine dati nel documento o lo strumento tramite cui vengono utilizzati i dati. Anche se una connessione BISM punta a un database fisico Business Intelligence Semantic Model in un altro server, viene utilizzato il file di connessione come se fosse l'origine dati. L'URL di SharePoint della connessione BI Semantic Model è un percorso dell'origine dati valido per i report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] in cui vengono usati dati BI Semantic Model.  
  
 Per la progettazione di report ad hoc in SharePoint, l'utente che crea il report deve disporre di autorizzazioni di SharePoint sul file di connessione BISM (estensione bism) e sul database Business Intelligence Semantic Model. Il contesto di sicurezza della connessione è l'utente interattivo che sta creando il report.  
  
  
