---
title: Recapito tramite la raccolta di SharePoint in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93a62ec076b9dc61cd01d18796f04bbaa04eb93b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100701"
---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>Recapito tramite la raccolta di SharePoint in Reporting Services
  In un server di report configurato per l'integrazione con SharePoint è disponibile un'estensione per il recapito che è possibile utili per inviare un report a una raccolta di SharePoint.  
  
 Per usare l'estensione per il recapito di SharePoint, è necessario creare una sottoscrizione da una pagina dell'applicazione in un sito di SharePoint, quindi selezionare **Raccolta documenti di SharePoint** come tipo di recapito. Non è possibile utilizzare l'estensione per il recapito di SharePoint per sottoscrizioni create in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o in Gestione report.  
  
> [!NOTE]  
>  L'estensione per il recapito non supporta l'invio di report a un sito di SharePoint se il server di report viene eseguito in modalità nativa. Se si tenta di chiamare l'estensione per il recapito a livello di programmazione per un server di report in modalità nativa, quest'ultimo restituirà l'errore `rsDeliveryExtensionNotFound` e registrerà l'errore `rsOperationNotSupportedSharePointMode` nei suoi file di log.  
  
## <a name="requirements"></a>Requisiti  
 I requisiti per il recapito di report visualizzabili a una raccolta includono quanto segue:  
  
-   Il server di report deve essere configurato per la modalità integrata SharePoint.  
  
-   Nel server di report deve essere installata e configurata l'estensione per il recapito a SharePoint.  
  
-   Il report deve essere un file di definizione (con estensione rdl). Non è possibile recapitare altri tipi di contenuto del server di report, ad esempio modelli o risorse, tramite una sottoscrizione. Non è possibile sottoscrivere report ad hoc che utilizzano modelli come origine dei dati.  
  
-   Il report deve utilizzare credenziali archiviate. Si tratta di un prerequisito per la creazione di qualsiasi sottoscrizione a un report, indipendentemente dal tipo di recapito.  
  
-   La destinazione deve essere una raccolta di SharePoint. Quando si sceglie la raccolta di destinazione, è necessario che quest'ultima si trovi nello stesso sito di SharePoint. Non è possibile recapitare il report a una raccolta disponibile in un altro server o in un altro sito della stessa raccolta siti.  
  
 Proprietà e metadati non sono inclusi nel recapito del report. La prima volta che il report viene recapitato eredita le impostazioni di sicurezza della cartella o dell'elenco che lo contiene. Se successivamente si modificano le impostazioni di sicurezza o si impostano le proprietà del report, tali impostazioni verranno mantenute. La sottoscrizione consente solo di aggiornare il report archiviato nel percorso specificato.  
  
## <a name="sharepoint-permissions"></a>Autorizzazioni di SharePoint  
 Per creare una sottoscrizione, è necessario disporre dell'autorizzazione Visualizzazione elementi per il report. Per recapitare il report, è necessario disporre dell'autorizzazione Aggiunta elementi per la raccolta a cui viene recapitato il report.  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>Come creare, modificare ed eliminare le sottoscrizioni  
  
1.  Accedere al sito di SharePoint in cui è disponibile il report.  
  
2.  Selezionare il report, fare clic sulla freccia GIÙ accanto al report e scegliere **Gestisci sottoscrizioni**.  
  
3.  Fare clic su **Crea**, **Modifica**o **Elimina**.  
  
 Verrà visualizzato un messaggio di stato nell'elenco Gestisci sottoscrizioni con informazioni aggiornate sulla sottoscrizione, tra cui l'esito e la data e l'ora dell'ultima esecuzione.  
  
## <a name="setting-delivery-options"></a>Impostazione delle opzioni di recapito  
 È possibile impostare le opzioni di recapito seguenti per una sottoscrizione che consente di recapitare un report a una raccolta di SharePoint.  
  
 Formato di output del rendering  
 Specificare il formato dell'applicazione a cui si desidera recapitare il report. Il rendering del report verrà eseguito in tale formato prima del recapito. Il formato di output selezionato determina l'estensione file predefinita.  
  
 L'elenco in cui è possibile selezionare i formati di output è costituito dalle estensioni di rendering installate nel server di report.  
  
 Si noti che non è possibile specificare formati di output destinati al solo uso interno o non supportati per i server di report eseguiti in modalità integrata SharePoint. Tali formati includono Null, RGDI e HTMLOWC.  
  
 Nome ed estensione file  
 Specificare il nome e l'estensione file del report che si desidera visualizzare nella raccolta di destinazione. Se non si specifica un'estensione file, ne verrà creata una dal server di report in base al formato di output. Questo valore è obbligatorio. Il nome file non deve contenere i caratteri seguenti: : \ / * ? " \< > | # { } %  
  
 Titolo  
 Specifica una proprietà `Title` facoltativa per il report nella raccolta di destinazione. Si tratta di una proprietà standard di tutti gli elementi archiviati in una raccolta. Gli utenti possono specificare se visualizzare o nascondere tale proprietà quando si visualizzano i contenuti della raccolta in un sito di SharePoint.  
  
 `Path`  
 Specifica l'URL completo della raccolta di SharePoint, inclusi il sito e l'applicazione Web di SharePoint. Ad esempio: <http://mySharePointWeb/MySite/MyDocLib>; in cui "<http://mySharePointWeb>" indica l'applicazione Web, "MySite" è il sito di SharePoint e "MyDocLib" è la raccolta di SharePoint in cui verrà recapitato il report.  
  
 Non è possibile specificare una pagina, un sito o un elenco. Il contenitore di destinazione deve essere una raccolta nello stesso sito o farm.  
  
 Opzioni sovrascrittura  
 Specifica se un file con lo stesso nome e la stessa estensione viene sostituito da una versione più recente quando la sottoscrizione viene elaborata. Scegliere **Sovrascrivi** se si desidera sostituire un file esistente con una versione più recente. Scegliere **None** se non si desidera che la sottoscrizione sostituisca i file. In questo caso, se esiste già un file con il nome e l'estensione di destinazione il recapito non verrà eseguito. Scegliere **Incremento automatico** se si desidera aggiungere le versioni successive dello stesso file aggiungendo un numero alla fine del nome file.  
  
 Copia automatica  
 Se si utilizza la funzionalità di copia automatica per copiare automaticamente l'ultima versione di un file in più percorsi, il file verrà copiato se l'opzione **Sovrascrivi** è abilitata. Se è stata usata **Autoincrement** oppure **None**, il recapito avrà esito negativo e il `rsDeliveryError` errore si verifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Create and Manage Subscriptions for SharePoint Mode Report Servers](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
