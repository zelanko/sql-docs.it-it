---
title: Concedere le autorizzazioni di database (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 335fe6deeb3d89483f5f5adb040b0788891053cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074952"
---
# <a name="grant-database-permissions-analysis-services"></a>Concedere le autorizzazioni per il database (Analysis Services)
  Se si affronta l'amministrazione del database di Analysis Services avendo già esperienza con i database relazionali, il primo aspetto da comprendere è che, per quanto riguarda l'accesso ai dati, il database non è l'oggetto principale a protezione diretta in Analysis Services.  
  
 La struttura di query primaria in Analysis Services è rappresentata da un cubo (o un modello tabulare), con le autorizzazioni utente impostate per specifici oggetti. A differenza del motore di database relazionale, in cui gli account di accesso al database e le autorizzazioni utente (spesso `db_datareader`) vengono impostati nel database stesso, un database di Analysis Services è per lo più un contenitore per gli oggetti query principali in un modello di dati. Se l'obiettivo immediato è consentire l'accesso ai dati per un cubo o un modello tabulare, è possibile ignorare le autorizzazioni di database per il momento e passare direttamente all'argomento: [Concedere le autorizzazioni del cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
 Le autorizzazioni di database in Analysis Services consentono di eseguire funzioni amministrative, che in senso lato equivalgono all'autorizzazione del database Controllo completo, mentre in un contesto più specifico consentono di delegare le operazioni di elaborazione. I livelli di autorizzazione per un database di Analysis Services sono specificati nel riquadro **Generale** della finestra di dialogo **Crea ruolo** , illustrata nella figura seguente e descritta di seguito.  
  
 In Analysis Services non ci sono account di accesso. È sufficiente creare i ruoli e assegnare gli account di Windows nel riquadro **Appartenenza** . Tutti gli utenti, compresi gli amministratori, si connettono ad Analysis Services con un account di Windows.  
  
 ![Crea ruolo le autorizzazioni del database che Visualizza finestra di dialogo](../media/ssas-permsdbrole.png "creare ruolo le autorizzazioni del database che Visualizza finestra di dialogo")  
  
 Esistono tre tipi di autorizzazioni specificate a livello di database.  
  
 **Controllo completo (amministratore)** : si tratta di un'autorizzazione omnicomprensiva che conferisce ampi poteri in un database di Analysis Services come, ad esempio, la possibilità di elaborare o eseguire query su qualsiasi oggetto all'interno del database e di gestire la sicurezza dei ruoli. L'autorizzazione Controllo completo consente di eseguire le stesse funzioni di un amministratore di database. Quando si seleziona `Full Control`, vengono selezionate anche le autorizzazioni `Process Database` e `Read Definition` che non è possibile rimuovere.  
  
> [!NOTE]  
>  Agli amministratori del server (membri del ruolo di amministratore del server) viene assegnata implicitamente l'autorizzazione Controllo completo per ogni database del server.  
  
 `Process Database` : Questa autorizzazione viene usata per delegare l'elaborazione a livello di database. L'amministratore può ripartire questa attività creando un ruolo che consenta a un'altra persona o servizio di richiamare le operazioni di elaborazione per un oggetto del database. In alternativa, è anche possibile creare i ruoli che consentono l'elaborazione in oggetti specifici. Per altre informazioni, vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) .  
  
 `Read Definition` Base di questa autorizzazione concede la possibilità di leggere i metadati degli oggetti, meno la possibilità di visualizzare i dati associati. In genere, questa autorizzazione viene usata nei ruoli creati per un'elaborazione dedicata, offrendo la possibilità di usare strumenti quali [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] per elaborare un database in modo interattivo. Senza `Read Definition`, l'autorizzazione `Process Database` è valida sono negli scenari con script. Per automatizzare l'elaborazione, ad esempio tramite SSIS o un'altra utilità di pianificazione, è possibile creare un ruolo con l'autorizzazione `Process Database` senza `Read Definition`. In caso contrario, provare a usare insieme le due proprietà nello stesso ruolo per supportare sia l'elaborazione automatica che interattiva tramite gli strumenti di SQL Server che visualizzano il modello di dati in un'interfaccia utente.  
  
## <a name="full-control-administrator-permissions"></a>Autorizzazioni Controllo completo (amministratore)  
 In [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], per amministratore di database si intende un'identità utente di Windows assegnata a un ruolo che include le autorizzazioni Controllo completo (amministratore). Un amministratore di database può eseguire qualsiasi attività all'interno del database, tra cui:  
  
-   Elaborazione di oggetti  
  
-   Lettura di dati e metadati per tutti gli oggetti del database, compresi cubi, dimensioni, gruppi di misure, prospettive e modelli di data mining  
  
-   Creazione o modifica dei ruoli di database mediante l'aggiunta di utenti o autorizzazioni, compresa la possibilità di aggiungere utenti a ruoli con autorizzazioni Controllo completo  
  
-   Eliminazione di ruoli di database o dell'appartenenza a ruoli  
  
-   Registrazione di assembly (o stored procedure) per il database  
  
 Si noti che un amministratore di database non può aggiungere o eliminare database dal server né concedere diritti di amministratore ad altri database sullo stesso server. Tale privilegio appartiene solo agli amministratori del server. Visualizzare [Concedi autorizzazioni di amministratore del Server &#40;Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) per altre informazioni su questo livello di autorizzazione.  
  
 Poiché tutti i ruoli sono definiti dall'utente, è consigliabile creare un ruolo dedicato a tale scopo, ad esempio un ruolo denominato "dbadmin", e quindi assegnare in modo appropriato gli account utente e di gruppo di Windows.  
  
#### <a name="create-roles-in-ssms"></a>Creare ruoli in SSMS  
  
1.  In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], aprire la cartella **Database** , selezionare un database e fare clic con il pulsante destro del mouse su **Ruoli** | **Nuovo ruolo**.  
  
2.  Nel riquadro **Generale** immettere un nome, ad esempio DBAdmin.  
  
3.  Selezionare la casella di controllo **Controllo completo (amministratore)** per il cubo. Si noti che `Process Database` e `Read Definition` vengono selezionati automaticamente. Entrambe le autorizzazioni vengono sempre incluse nei ruoli con `Full Control`.  
  
4.  Nel riquadro **Appartenenza** immettere gli account utente e di gruppo di Windows che si connettono ad Analysis Services con questo ruolo.  
  
5.  Fare clic su **OK** per completare la creazione del ruolo.  
  
## <a name="process-database"></a>Elaborazione database  
 Quando si definisce un ruolo che concede le autorizzazioni di database, è possibile ignorare `Full Control` e scegliere solo `Process Database`. Tale autorizzazione, impostata a livello di database, consente l'elaborazione in tutti gli oggetti all'interno del database. Per altre informazioni, vedere [Grant process permissions &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>Lettura definizione  
 Ad esempio `Process Database`, l'impostazione `Read Definition` autorizzazioni a livello di database ha un effetto a catena sugli altri oggetti all'interno del database. Se si vogliono impostare le autorizzazioni Lettura definizione a un livello più granulare, è necessario deselezionare Lettura definizione come proprietà del database nel riquadro Generale. Per altre informazioni, vedere [Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere autorizzazioni di amministratore del Server &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
