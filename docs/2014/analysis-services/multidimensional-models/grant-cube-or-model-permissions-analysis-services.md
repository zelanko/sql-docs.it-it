---
title: Concedere le autorizzazioni per un cubo o un modello (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.cubes.f1
helpviewer_keywords:
- user access rights [Analysis Services], cubes
- cubes [Analysis Services], security
- read/write permissions
- permissions [Analysis Services], cubes
ms.assetid: 55b1456e-2f6b-4101-b316-c926f40304e3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12eb2a2f6ea7501e03830724b24c5808375db7c4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075030"
---
# <a name="grant-cube-or-model-permissions-analysis-services"></a>Concedere le autorizzazioni per un cubo o un modello (Analysis Services)
  Un cubo o un modello tabulare è l'oggetto query primario in un modello di dati di Analysis Services. Quando un utente si connette ai dati tabulari o multidimensionali da Excel per l'esplorazione ad hoc dei dati, in genere inizia selezionando un cubo o un modello tabulare specifico come struttura di dati necessaria per l'oggetto report Pivot. Questo argomento illustra come concedere le autorizzazioni necessarie per l'accesso ai dati tabulari o del cubo.  
  
 Per impostazione predefinita, solo l'amministratore del server o l'amministratore del database dispone delle autorizzazioni per eseguire le query sui cubi in un database. L'accesso ai cubi da parte di un utente non amministratore richiede l'appartenenza a un ruolo creato per il database contenente il cubo. L'appartenenza è supportata per gli account di gruppo o utente di Windows, definiti in Active Directory o nel computer locale. Prima di iniziare, identificare gli account a cui verrà assegnata l'appartenenza ai ruoli che verranno creati.  
  
 L'accesso `Read` a un cubo fornisce anche le autorizzazioni per le dimensioni, i gruppi di misure e le prospettive in esso contenuti. La maggior parte degli amministratori concede le autorizzazioni di lettura a livello di cubo e quindi limita le autorizzazioni su oggetti specifici, dati associati o in base all'identità utente.  
  
 Per conservare le definizioni dei ruoli nelle distribuzioni successive della soluzione, è consigliabile definire i ruoli in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] come parte integrante del modello e quindi procedere all'assegnazione delle appartenenze ai ruoli in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] da parte di un amministratore del database dopo la pubblicazione del database. È tuttavia possibile usare uno dei due strumenti per entrambe le attività. Per semplificare l'esercizio, verrà usato [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sia per la definizione dei ruoli che per l'assegnazione delle appartenenze.  
  
> [!NOTE]  
>  Solo gli amministratori del server o gli amministratori del database con autorizzazioni di controllo completo possono distribuire un cubo dai file di origine in un server o creare ruoli e assegnare membri. Per informazioni dettagliate su questi livelli di autorizzazione, vedere concedere le autorizzazioni di [amministratore del Server &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) e [concedere autorizzazioni per il database &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md) .  
  
#### <a name="step-1-create-the-role"></a>Passaggio 1: Creare il ruolo  
  
1.  In SSMS connettersi ad Analysis Services. Se è necessaria assistenza per questo passaggio, vedere [Connettersi dalle applicazioni client &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md).  
  
2.  Aprire la cartella **Database** in Esplora oggetti e selezionare un database.  
  
3.  Fare clic con il pulsante destro del mouse su **Ruoli** e scegliere **Nuovo ruolo**. Si noti che i ruoli vengono creati a livello di database e si applicano agli oggetti in esso contenuti. Non è possibile condividere i ruoli tra i database.  
  
4.  Nel riquadro **Generale** immettere un nome e, se si vuole, una descrizione. Questo riquadro contiene anche diverse autorizzazioni per il database quali Controllo completo, Elaborazione database e Lettura definizione. Nessuna di tali autorizzazioni è necessaria per l'esecuzione di query su un cubo o un modello tabulare. Per altre informazioni su queste autorizzazioni, vedere [Concedere autorizzazioni per il database &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md).  
  
5.  Procedere al passaggio successivo dopo avere immesso un nome ed eventualmente una descrizione.  
  
#### <a name="step-2-assign-membership"></a>Passaggio 2: Assegnare l'appartenenza  
  
1.  Nel riquadro **Appartenenza** fare clic su **Aggiungi** per immettere gli account di gruppo o utente di Windows che accederanno al cubo tramite questo ruolo. Analysis Services supporta solo le identità di sicurezza di Windows. Si noti che in questo passaggio non vengono creati gli account di accesso al database. In Analysis Services gli utenti si connettono tramite gli account di Windows.  
  
2.  Procedere al passaggio successivo per impostare le autorizzazioni per il cubo.  
  
     Si noti che il riquadro Origine dati verrà ignorato. La maggior parte degli utenti normali dei dati di Analysis Services non necessita di autorizzazioni per l'oggetto origine dati. Per informazioni dettagliate sui livelli di autorizzazione, vedere [Concedere le autorizzazioni per un oggetto origine dati &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md) .  
  
#### <a name="step-3-set-cube-permissions"></a>Passaggio 3: Impostare le autorizzazioni per il cubo  
  
1.  Nel riquadro **cubi** selezionare un cubo e quindi fare clic su `Read` accesso in **lettura/scrittura** .  
  
     `Read`l'accesso è sufficiente per la maggior parte delle operazioni. **Lettura/Scrittura** viene usato solo per il writeback e non per l'elaborazione. Per altre informazioni su questa funzionalità, vedere [Set Partition Writeback](set-partition-writeback.md) .  
  
     Si noti che è possibile selezionare più cubi nonché altri oggetti disponibili nella finestra di dialogo Crea ruolo. Quando si concedono le autorizzazioni a un cubo, si autorizza l'accesso alle dimensioni e alle prospettive associate al cubo. Non è necessario aggiungere manualmente gli oggetti già rappresentati nel cubo.  
  
     Se è necessario modificare l'autorizzazione per gli oggetti o un utente, ad esempio per rendere alcune misure non disponibili, è possibile consentire o negare l'accesso in modo atomico per oggetti specifici, anche per le celle. Per informazioni dettagliate, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) e [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md).  
  
2.  A questo punto, dopo avere fatto clic su **OK**, tutti i membri di questo ruolo avranno accesso ai cubi ai livelli di autorizzazione specificati.  
  
     Si noti che nel riquadro **Cubi** è possibile concedere l'autorizzazione agli utenti per creare cubi locali da un cubo sul server tramite **Drill-through e cubo locale**o consentire solo il drill-through tramite l'autorizzazione **Drill-through** .  
  
     Infine, in questo riquadro è possibile concedere i diritti di **Elaborazione database** sul cubo per consentire a tutti i membri di questo ruolo di elaborare i dati per il cubo. Poiché l'elaborazione è in genere un'operazione con restrizioni, è consigliabile che siano gli amministratori a eseguire tale attività oppure definire ruoli separati specifici per l'attività. Per altre informazioni sulle procedure consigliate per le autorizzazioni di elaborazione, vedere [Concedere autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md).  
  
#### <a name="step-4-test"></a>Passaggio 4: Test  
  
1.  Usare Excel per testare le autorizzazioni di accesso al cubo. È anche possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seguendo la stessa procedura descritta più avanti, eseguendo l'applicazione come utente non amministratore.  
  
    > [!NOTE]  
    >  Per gli amministratori di Analysis Services, le autorizzazioni di amministratore vengono usate insieme ai ruoli che dispongono di autorizzazioni minori rendendo difficile testare singolarmente le autorizzazioni dei ruoli. Per semplificare il test, è consigliabile aprire una seconda istanza di SSMS, usando l'account assegnato al ruolo che si sta testando.  
  
2.  Tenere premuto il tasto MAIUSC e fare clic con il pulsante destro del mouse sul collegamento **Excel** per accedere all'opzione **Esegui come altro utente** . Immettere uno degli account di gruppo o utente di Windows con l'appartenenza a questo ruolo.  
  
3.  In Excel usare la scheda Dati per connettersi ad Analysis Services. Poiché Excel viene eseguito come altro utente di Windows, per il test dei ruoli usare l'opzione **Usa autenticazione di Windows** come tipo di credenziali corretto. Se è necessaria assistenza per questo passaggio, vedere [Connettersi dalle applicazioni client &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md).  
  
     Se alla connessione si verifica un errore, controllare la configurazione della porta per Analysis Services e verificare che il server accetti le connessioni remote. Vedere [configurare il Windows Firewall per consentire l'accesso Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) per la configurazione della porta.  
  
#### <a name="step-5-script-role-definition-and-assignments"></a>Passaggio 5: Generare uno script per la definizione e le assegnazioni di ruolo  
  
1.  Come passaggio finale, generare uno script per acquisire la definizione del ruolo appena creata.  
  
     Quando si ridistribuisce un progetto da [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] vengono sovrascritti tutti i ruoli o le relative appartenenze non definiti all'interno del progetto. Lo script rappresenta il modo più rapido per ricompilare i ruoli e le relative appartenenze dopo una ridistribuzione.  
  
2.  In SSMS passare alla cartella **Ruoli** e fare clic con il pulsante destro del mouse su un ruolo esistente.  
  
3.  Selezionare **script Role come** | **Crea nel** | **file**.  
  
4.  Salvare il file con estensione xmla. Per testare lo script, eliminare il ruolo corrente, aprire il file in SSMS e premere F5 per eseguire lo script.  
  
## <a name="next-step"></a>Passaggio successivo  
 È possibile ottimizzare le autorizzazioni del cubo per limitare l'accesso ai dati delle celle o della dimensione. Per informazioni dettagliate, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) e [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Metodologie di autenticazione supportate da Analysis Services](../instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Concedere le autorizzazioni per data mining strutture e modelli &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Concedere le autorizzazioni per un oggetto origine dati &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
