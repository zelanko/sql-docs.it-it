---
title: Attestazioni per il servizio token Windows (c2WTS) e Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.date: 09/15/2017
ms.openlocfilehash: 8d53445544c360250ed35c322e2fc4078559bbbe
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454566"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Attestazioni per il servizio token Windows (C2WTS) e Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

La visualizzazione di report in modalità nativa all'interno della [web part Visualizzatore di report di SQL Server Reporting Services](../report-server-sharepoint/deploy-report-viewer-web-part.md) richiede il componente Attestazioni per il servizio token Windows (C2WTS) di SharePoint.

C2WTS è inoltre necessario con la modalità SharePoint di SQL Server Reporting Services se si vuole usare l'autenticazione di Windows per le origini dati all'esterno della farm di SharePoint. Il servizio C2WTS è necessario anche se l'origine dati si trova nello stesso computer del servizio condiviso, sebbene in questo scenario la delega vincolata non sia richiesta.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

## <a name="report-viewer-native-mode-web-part-configuration"></a>Configurazione della web part (modalità nativa) di Visualizzatore di report

La web part Visualizzatore di report può essere usata per incorporare i report in modalità nativa di SQL Server Reporting Services nel sito di SharePoint. Questa web part è disponibile per SharePoint 2013 e SharePoint 2016. SharePoint 2013 e SharePoint 2016 usano l'autenticazione delle attestazioni. Di conseguenza, C2WTS deve essere configurato nel modo giusto e Reporting Services deve essere configurato per l'autenticazione Kerberos perché i report vengano generati correttamente.

1. Per configurare l'istanza di Reporting Services (modalità nativa) per l'autenticazione Kerberos, determinare l'account del servizio SSRS, impostare un SPN e aggiornare il file rsreportserver.config per usare il tipo di autenticazione RSWindowsNegotiate. [Registrare un nome dell'entità servizio (SPN) per un server di report](https://docs.microsoft.com/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server)

2. Seguire la procedura in [Passaggi necessari per configurare c2WTS](https://docs.microsoft.com/sql/reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services?view=sql-server-2017#steps-needed-to-configure-c2wts)
 

## <a name="sharepoint-mode-integration"></a>Integrazione della modalità SharePoint

**Questa sezione si applica solo a SQL Server 2016 Reporting Services e versioni precedenti.**

Il componente Attestazioni per il servizio token Windows (C2WTS) di SharePoint è necessario con la modalità SharePoint di SQL Server Reporting Services se si vuole usare l'autenticazione di Windows per le origini dati all'esterno della farm di SharePoint. La condizione è valida anche se l'utente accede alle origini dati tramite l'autenticazione di Windows perché la comunicazione tra il Web front-end (WFE) e il servizio condiviso Reporting Services si basa sempre sull'autenticazione delle attestazioni.

## <a name="steps-needed-to-configure-c2wts"></a>Passaggi necessari per configurare c2WTS

I token creati da C2WTS funzioneranno solo con la delega vincolata (vincoli a servizi specifici) e l'opzione di configurazione che prevede l'uso di qualsiasi protocollo di autenticazione (transizione di protocollo).

Se l'ambiente utilizzerà la delega vincolata Kerberos, le origini dati esterne e il servizio SharePoint Server devono trovarsi nello stesso dominio Windows. Qualsiasi servizio basato su Attestazioni per il servizio token Windows (c2WTS) deve usare la delega **vincolata** Kerberos per consentire a c2WTS di usare la transizione del protocollo Kerberos per convertire le attestazioni in credenziali di Windows. Questi requisiti sono validi per tutti i servizi condivisi SharePoint. Per altre informazioni, vedere [Pianificare l'autenticazione Kerberos in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).  

1. Configurare l'account di dominio del servizio C2WTS. 

    **Come procedura consigliata C2WTS deve essere eseguito con la propria identità di dominio.**

    * Creare un account Active Directory e registrarlo come account gestito in SharePoint Server. Per altre informazioni sugli account gestiti, vedere [Managed Accounts in Sharepoint](https://blog.wbaer.net/2010/04/11/managed-accounts-in-sharepoint-2010/) (Account gestiti in Sharepoint)
   
    * Configurare il servizio C2WTS per usare l'account gestito tramite Amministrazione centrale SharePoint > Sicurezza > Configura account di servizio > Servizio Windows - Attestazioni per il servizio token Windows

    Aggiungere l'account del servizio C2WTS al gruppo di amministratori locale in ogni server in cui si userà C2WTS. Per la **web part Visualizzatore di report** saranno i server Web front-end (WFE). Per la **modalità integrata SharePoint** saranno i server applicazioni in cui è in esecuzione il servizio Reporting Services.
    * Concedere all'account C2WTS le autorizzazioni seguenti nei criteri di sicurezza locale in Criteri locali > Assegnazione diritti utente:
        * Agisci come parte del sistema operativo
        * Rappresenta un client dopo l'autenticazione
        * Accedi come servizio

    
2. Configurare la delega per l'account del servizio C2WTS.

    L'account necessita della delega vincolata con transizione di protocollo e delle autorizzazioni per la delega ai servizi con cui deve comunicare, ovvero il motore di database di SQL Server e SQL Server Analysis Services. Per configurare la delega è possibile usare lo snap-in Utenti e computer di Active Directory ed è necessario essere un amministratore di dominio.

    > [!IMPORTANT]
    > Qualsiasi impostazione configurata per l'account del servizio C2WTS nella scheda relativa alla delega deve corrispondere all'account del servizio principale in uso. Per la **web part Visualizzatore di report** sarà l'account del servizio per l'applicazione Web SharePoint. Per la **modalità integrata SharePoint** sarà l'account del servizio Reporting Services.
    >
    > Se ad esempio si consente all'account del servizio C2WTS la delega a un servizio SQL, la stessa operazione dovrà essere eseguita sull'account del servizio Reporting Services per la modalità integrata SharePoint.

    * Fare clic con il pulsante destro del mouse su ogni account del servizio e aprire la finestra di dialogo delle proprietà. Nella finestra di dialogo fare clic sulla scheda **Delega** .

        La scheda relativa alla delega è visibile solo se all'oggetto è stato assegnato un nome dell'entità servizio (SPN). C2WTS non richiede un nome SPN nel proprio account. Tuttavia, senza questo nome, la scheda **Delega** non sarà visibile. Un modo alternativo per configurare la delega vincolata consiste nell'impiego di un'utilità, ad esempio **ADSIEdit**.

    * Di seguito vengono indicate le opzioni di configurazione principali nella scheda relativa alla delega:

        * Selezionare **Utente attendibile per la delega solo ai servizi specificati**
        * Selezionare **Usa un qualsiasi protocollo di autenticazione**

    * Selezionare **Aggiungi** per aggiungere un servizio per la delega.

    * Selezionare **Users or Computers...&#42;** (Utenti o computer) e immettere l'account che ospita il servizio. Ad esempio, se SQL Server è in esecuzione con un account denominato *sqlservice*, immettere `sqlservice`. 
      Per la **Web part Visualizzatore di report** sarà l'account del servizio per l'istanza di Reporting Services (modalità nativa).

    * Selezionare l'elenco del servizio. Verranno visualizzati i nomi SPN disponibili per tale account. Se non viene visualizzato, il servizio indicato per l'account può essere mancante o inserito in un altro account. è possibile usare l'utilità SetSPN per modificare i nomi SPN. Per la **Web part Visualizzatore di report**, verrà visualizzato il nome SPN http configurato in [Configurazione della web part (modalità nativa) di Visualizzatore di report](https://docs.microsoft.com/sql/reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services?view=sql-server-2017#report-viewer-native-mode-web-part-configuration).

    * Selezionare OK per uscire dalle finestre di dialogo.

3. Configurare *AllowedCallers* per C2WTS.

    In C2WTS è necessario che le identità chiamanti siano elencate esplicitamente nel file di configurazione **C2WTShost.exe.config**. C2WTS accetta richieste da tutti gli utenti autenticati nel sistema solo se viene configurato appositamente. In questo caso il chiamante è il gruppo di Windows WSS_WPG. Il file C2WTShost.exe.config viene salvato nel percorso seguente:

    Modificando l'account del servizio in Amministrazione centrale SharePoint, per il servizio C2WTS, tale account verrà aggiunto al gruppo WSS_WPG.

    **\Programmi\Windows Identity Foundation\v3.5\c2WTShost.exe.config**

    Di seguito viene illustrato un esempio del file di configurazione:

    ```
    <configuration>
      <windowsTokenService>
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->
        <allowedCallers>
          <clear/>
          <add value="WSS_WPG" />
        </allowedCallers>
      </windowsTokenService>
    </configuration>
    ```

4. Avviare (arrestare e avviare di nuovo nel caso fosse già stato avviato) Attestazioni per il servizio token Windows tramite Amministrazione centrale SharePoint nella pagina **Gestisci servizi nel server**. Il servizio deve essere avviato nel server che eseguirà l'azione. Ad esempio, in presenza di un server WFE e di un server applicazioni in cui è in esecuzione il servizio condiviso SQL Server Reporting Services, sarà sufficiente avviare C2WTS solo nel server applicazioni. La presenza di C2WTS è necessaria in un server WFE solo se si esegue la web part Visualizzatore di report.

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
