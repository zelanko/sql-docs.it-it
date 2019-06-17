---
title: Installare PowerPivot dal Prompt dei comandi | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e6da1b23bd23634e3edb8d92093cab6ce71a2783
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094547"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>Installazione di PowerPivot dal prompt dei comandi
  È possibile eseguire il programma di installazione dalla riga di comando per installare SQL Server PowerPivot per SharePoint. È necessario includere il parametro `/ROLE` nel comando ed escludere il parametro `/FEATURES`.  
  
## <a name="prerequisites"></a>Prerequisiti  
 SharePoint Server 2010 Enterprise Edition con Service Pack 1 (SP1) deve essere installato.  
  
 È necessario utilizzare account di dominio per eseguire il provisioning di Analysis Services.  
  
 Il computer deve essere unito in join allo stesso dominio della farm di SharePoint.  
  
##  <a name="Commands"></a> / Opzioni di installazione in base al ruolo  
 Per le distribuzioni PowerPivot per SharePoint, viene utilizzato il parametro `/ROLE` anziché `/FEATURES`. I valori validi includono:  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 Con entrambi i ruoli è possibile installare i file di distribuzione, configurazione e applicazione che consentono l'esecuzione di PowerPivot per SharePoint in una farm di SharePoint. Se si specifica uno dei due ruoli, vengono verificati i requisiti hardware e software necessari per l'integrazione con SharePoint.  
  
 Con l'opzione Farm esistente si suppone l'esistenza di una farm di SharePoint. L'opzione nuova farm si presuppone che si creerà una nuova farm; supporta l'aggiunta di un'istanza del motore di Database nella sintassi della riga di comando in modo che è possibile usare l'istanza del motore di Database come server di database della farm.  
  
 A differenza delle versioni precedenti, tutte le attività di configurazione del server vengono eseguite successivamente all'installazione. In caso di automazione delle procedure di installazione e configurazione, è possibile utilizzare PowerShell per configurare il server. Per altre informazioni, vedere [configurazione di PowerPivot tramite Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  
  
## <a name="example-commands"></a>Comando di esempio  
 Negli esempi seguenti viene illustrato l'utilizzo di ogni opzione. Esempio 1 mostra `SPI_AS_ExistingFarm`.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 Nell'esempio 2 viene illustrata l'opzione `SPI_AS_NewFarm`. Si noti che sono inclusi i parametri per eseguire il provisioning del Motore di database.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="Join"></a> Modificare la sintassi del comando  
 Utilizzare i passaggi seguenti per modificare la sintassi del comando di esempio.  
  
1.  Copiare il comando seguente in Blocco note:  
  
    ```  
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     Il parametro `/q` consente di eseguire il programma di installazione in modalità non interattiva senza l'ausilio dell'interfaccia utente.  
  
     È necessario specificare `/IAcceptSQLServerLicenseTerms` quando si specifica il parametro `/q` o `/qs` per le installazioni automatiche.  
  
     Il parametro `/action` indica al programma di installazione di eseguire un'installazione.  
  
     Il parametro `/role` indica al programma di installazione di installare il programma Analysis Services e i file di configurazione necessari per PowerPivot per SharePoint. Questo ruolo consente inoltre di rilevare e utilizzare le informazioni di connettività della farm esistente per accedere al database di configurazione di SharePoint. Questo parametro è obbligatorio. Utilizzarlo invece del parametro `/features` per specificare i componenti da installare.  
  
     Il parametro `/instancename` specifica 'PowerPivot' come un'istanza denominata. Questo valore è specificato a livello di codice e non può essere modificato. Viene specificato nel comando per scopi didattici per sapere in che modo è stato installato il servizio.  
  
     Il parametro `/indicateprogress` consente di monitorare lo stato di avanzamento nella finestra del prompt dei comandi.  
  
2.  Il parametro `PID` viene omesso dal comando, di conseguenza viene installata la copia di valutazione. Se si desidera installare la Enterprise Edition, aggiungere il PID al comando Setup e fornire un codice Product Key valido.  
  
    ```  
  
    /PID=<product key for an Enterprise installation>  
  
    ```  
  
3.  Sostituire i segnaposto per \<dominio\nome utente > e \<StrongPassword > con gli account utente valido e le password.  
  
     Il `/assvaccount` e **/assvcpassword** i parametri vengono usati per configurare il [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] istanza del server applicazioni. Sostituire questi segnaposto con informazioni sull'account valide.  
  
     Il **/assysadminaccounts** parametro deve essere impostato per l'identità dell'utente che esegue il programma di installazione di SQL Server. È necessario specificare almeno un amministratore di sistema. Si noti che il programma di installazione di SQL Server non concede più autorizzazioni sysadmin automatiche ai membri del gruppo Administrators predefinito.  
  
4.  Rimuovere le interruzioni di riga.  
  
5.  Selezionare l'intero comando e quindi fare clic su **copia** dal menu Modifica.  
  
6.  Aprire un prompt dei comandi dell'amministratore. A tale scopo, fare clic su **avviare**, fare doppio clic su prompt dei comandi e selezionare **Esegui come amministratore**.  
  
7.  Spostarsi sull'unità o sulla cartella condivisa che contiene i supporti di installazione di SQL Server.  
  
8.  Incollare il comando rivisto nella riga di comando. A tale scopo, fare clic sull'icona nell'angolo superiore sinistro della finestra del prompt dei comandi, scegliere **Edit**, quindi fare clic su **Incolla**.  
  
9. Premere **invio** per eseguire il comando. Attendere il completamento dell'installazione. È possibile monitorare lo stato di avanzamento dell'installazione nella finestra del prompt dei comandi.  
  
10. Per verificare installazione, controllare il file summary.txt in \Programmi\SQL Server\120\Setup Bootstrap\Log. Il risultato finale deve essere "Superato" se il server viene installato senza errori.  
  
11. Configurare il server. È necessario almeno distribuire soluzioni, creare un'applicazione di servizio e abilitare la caratteristica per ogni raccolta siti. Per altre informazioni, vedere [Configura o Ripristina PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41; ](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md) oppure [amministrazione Server PowerPivot e la configurazione in Amministrazione centrale ](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Installazione di PowerPivot per SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
