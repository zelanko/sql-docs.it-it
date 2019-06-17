---
title: Modello di programmazione RDS in dettaglio | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 55f5d599ea2399697a0b96cc3d316776179b7562
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699591"
---
# <a name="rds-programming-model-in-detail"></a>Informazioni dettagliate sul modello di programmazione RDS
Di seguito sono gli elementi chiave del modello di programmazione di servizi desktop remoto:  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   Evento  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 L'applicazione client deve specificare il server e il programma di server da richiamare. In cambio, l'applicazione riceve un riferimento all'applicazione server e può gestire il riferimento come se fosse il programma server stesso.  
  
 Il modello a oggetti RDS incorpora questa funzionalità con la [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetto.  
  
 Il programma del server viene specificato con un ID di programma, o *ProgID*. Il server utilizza il *ProgID* e del Registro di sistema del computer server per individuare le informazioni sul programma effettivo da avviare.  
  
 Servizi Desktop remoto viene fatta distinzione internamente a seconda se il programma del server è in un server remoto tramite Internet o una intranet. un server in una rete locale; o non in un server, anziché su una libreria di collegamento dinamico (DLL) locale. Questa distinzione determina come vengono scambiate tra il client e server, le informazioni e un prezioso tangibili nel tipo di riferimento restituito all'applicazione client. Tuttavia, dal proprio punto di vista, questa distinzione non ha alcun significato speciale. Ciò che conta è che viene restituito un riferimento di un programma utilizzabile.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 Servizi Desktop remoto offre un programma server predefinito che è possibile eseguire una query SQL sull'origine dati e restituiscono un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dell'oggetto o richiedere un' **Recordset** dell'oggetto e aggiornare l'origine dati.  
  
 Il modello a oggetti RDS incorpora questa funzionalità con il [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto.  
  
 Inoltre, questo oggetto dispone di un metodo per la creazione di un oggetto vuoto **Recordset** oggetto che è possibile compilare a livello di codice ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)), nonché un altro metodo per convertire un **Recordset**  oggetti in una stringa di testo per creare una pagina Web ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Con ADO, è possibile escludere alcuni della connessione standard e del comportamento del comando il **RDSServer** con un **DataFactory** gestore e un file di personalizzazione che contiene una connessione, comando, e i parametri di sicurezza.  
  
 Il programma del server viene a volte chiamato un *oggetto business*. È possibile scrivere il proprio oggetto business personalizzato che può eseguire l'accesso ai dati complessi, controlli di validità e così via. Anche quando si scrive un oggetto business personalizzato, è possibile creare un'istanza di un **RDSServer** dell'oggetto e usare alcuni dei metodi per eseguire le proprie attività.  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 Servizi Desktop remoto consente di combinare le funzionalità del **Servizi Desktop remoto. DataSpace** e **RDSServer**e abilitare anche controlli visivi da usare con facilità il **Recordset** oggetto restituito da una query da un'origine dati. Tenta di servizi desktop remoto, nel caso più comune, eseguire quanto più possibile accedere alle informazioni in un server e visualizzarlo in un controllo visual automaticamente.  
  
 Il modello a oggetti RDS incorpora questa funzionalità con la [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 Il **Servizi Desktop remoto. DataControl** presenta due aspetti. Uno degli aspetti riguarda l'origine dati. Se si imposta il comando e le informazioni di connessione utilizzando il **Connect** e **SQL** le proprietà del **Servizi Desktop remoto. DataControl**, verrà automaticamente usato il **Servizi Desktop remoto. DataSpace** per creare un riferimento all'impostazione predefinita **RDSServer** oggetto. Il **RDSServer** utilizzerà il **Connect** valore della proprietà per la connessione all'origine dati, usare il **SQL** valore della proprietà da ottenere un  **Recordset** dall'origine dati e restituiscono il **Recordset** dell'oggetto per il **Servizi Desktop remoto. DataControl**.  
  
 Il secondo aspetto relativo alla visualizzazione di restituita **Recordset** informazioni contenute in un controllo visivo. È possibile associare un controllo visivo con i **Servizi Desktop remoto. DataControl** (in un processo denominato associazione) e ottenere l'accesso alle informazioni nelle associato **Recordset** oggetto, visualizzare i risultati della query in una pagina Web in Microsoft® Internet Explorer. Ogni **Servizi Desktop remoto. DataControl** viene associato uno **Recordset** oggetto che rappresenta i risultati di una singola query, a uno o più controlli visivi (ad esempio, una casella di testo, casella combinata, controllo griglia e così via). Possono esistere più **Servizi Desktop remoto. DataControl** oggetto in ogni pagina. Ogni **Servizi Desktop remoto. DataControl** oggetto può essere connesso a un'altra origine dati e contiene i risultati di una query separata.  
  
 Il **Servizi Desktop remoto. DataControl** oggetto include anche metodi per lo spostamento, ordinamento e il filtraggio delle righe del controllo associato **Recordset** oggetto. Questi metodi sono simili, ma non identici, i metodi sull'oggetto ADO **Recordset** oggetto.  
  
## <a name="events"></a>Events  
 Servizi Desktop remoto supporta due degli eventi interni, che sono indipendenti tra il modello di eventi ADO. Il [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) eventi viene chiamato ogni volta che il **Servizi Desktop remoto. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) le modifiche alle proprietà, notificando all'utente dopo aver completato un'operazione asincrona, terminato o si è verificato un errore. Il [onError](../../../ado/reference/rds-api/onerror-event-rds.md) eventi viene chiamato ogni volta che si verifica un errore, anche se l'errore si verifica durante un'operazione asincrona.  
  
> [!NOTE]
>  Microsoft Internet Explorer sono disponibili due eventi aggiuntivi per Servizi Desktop remoto: **onDataSetChanged**, che indica che il **Recordset** è il recupero di righe, è ancora completamente funzionale e  **onDataSetComplete**, che indica che il **Recordset** ha completato il recupero di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello di programmazione RDS con oggetti](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace Object (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS Scenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



