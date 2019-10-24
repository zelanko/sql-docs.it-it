---
title: Registrare un database come applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerdacwizard.registerdac.f1
- sql12.swb.registerdacwizard.summary.f1
- sql12.swb.registerdacwizard.introduction.f1
- sql12.swb.registerdacwizard.setproperties.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ed991d65858d40b96013659caa2d83c479ca1d3
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782714"
---
# <a name="register-a-database-as-a-dac"></a>Registrare un database come applicazione livello dati
  Utilizzare la **procedura guidata Registra applicazione livello dati** o uno script di Windows PowerShell per compilare una definizione di applicazione livello dati (DAC) che descrive gli oggetti in un database esistente e registrare la definizione DAC nel database di sistema `msdb` ( **Master** in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]).  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **Per aggiornare un'applicazione livello dati (DAC) tramite:**  [la procedura guidata Registra applicazione livello dati](#UsingRegisterDACWizard), [PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Il processo di registrazione genera una definizione di applicazione livello dati che definisce gli oggetti nel database. La definizione dell'applicazione livello dati e il database combinati costituiscono un'istanza di applicazione livello dati. Se si registra un database come applicazione livello dati in un'istanza gestita del Motore di database, l'applicazione livello dati registrata viene incorporata in Utilità SQL Server al successivo invio del set di raccolta dell'utilità dall'istanza al punto di controllo dell'utilità. L'applicazione livello dati sarà quindi presente nel nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Deployed Data-tier Applications** details page.  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 La registrazione di un'applicazione livello dati può essere effettuata solo per un database in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o versioni successive. La registrazione di un'applicazione livello dati non può essere eseguita se è stata già registrata un'applicazione livello dati per il database. Se, ad esempio, il database è stato creato distribuendo un'applicazione livello dati, non è possibile eseguire la procedura guidata **Registra applicazione livello dati**.  
  
 Non è possibile registrare un'applicazione livello dati se il database include oggetti non supportati nell'applicazione livello dati o utenti contenuti. Per ulteriori informazioni sui tipi di oggetti supportati in un'applicazione livello dati, vedere [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="Permissions"></a> Permissions  
 La registrazione di un'applicazione livello dati in un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] richiede almeno autorizzazioni ALTER ANY LOGIN e VIEW DEFINITION per l'ambito del database, nonché autorizzazioni SELECT su **sys.sql_expression_dependencies**, oltre all'appartenenza al ruolo predefinito del server **dbcreator** . Possono registrare un'applicazione livello dati anche i membri del ruolo predefinito del server **sysadmin** o dell'account amministratore di sistema SQL Server predefinito denominato **sa** . La registrazione di un'applicazione livello dati che non contiene accessi in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] richiede l'appartenenza ai ruoli **dbmanager** o **serveradmin** . La registrazione di un'applicazione livello dati che contiene account di accesso in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] richiede l'appartenenza ai ruoli **loginmanager** o **serveradmin** .  
  
##  <a name="UsingRegisterDACWizard"></a> Utilizzo della procedura guidata Registra applicazione livello dati  
 **Per registrare un'applicazione livello dati tramite procedura guidata**  
  
1.  In **Esplora oggetti**espandere il nodo dell'istanza contenente il database per il quale registrare l'applicazione livello dati.  
  
2.  Espandere il nodo di **Database** .  
  
3.  Fare clic con il pulsante destro del mouse sul database da registrare, scegliere **Attività** e quindi selezionare **Registra come applicazione livello dati**.  
  
4.  Completare le finestre di dialogo della procedura guidata.  
  
    1.  [Pagina Introduzione](#Introduction)  
  
    2.  [Pagina Imposta proprietà](#Set_properties)  
  
    3.  [Pagina Convalida e riepilogo](#Summary)  
  
    4.  [Pagina Registra DAC](#Register)  
  
##  <a name="Introduction"></a> Pagina Introduzione  
 In questa pagina vengono descritti i passaggi per la registrazione di un'applicazione livello dati.  
  
 **Non visualizzare più questa pagina.** - Fare clic sulla casella di controllo per evitare che la pagina venga visualizzata nuovamente in futuro.  
  
 **Avanti >** : consente di passare alla pagina **Imposta proprietà**.  
  
 **Annulla** : consente di terminare la procedura guidata senza registrare un'applicazione livello dati.  
  
##  <a name="Set_properties"></a> Pagina Imposta proprietà  
 Utilizzare questa pagina per specificare le proprietà a livello di applicazione livello dati quali il nome dell'applicazione e la versione.  
  
 **Nome applicazione** - Stringa che specifica il nome usato per identificare la definizione dell'applicazione livello dati; il campo viene popolato con il nome del database.  
  
 **Versione** - Valore numerico che identifica la versione dell'applicazione livello dati. La versione DAC viene utilizzata in Visual Studio per identificare la versione della DAC alla quale stanno lavorando gli sviluppatori. Quando si distribuisce un'applicazione livello dati, la versione viene archiviata nel database di `msdb` e può essere visualizzata successivamente nel nodo **applicazioni livello dati** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Descrizione** - (Facoltativa). Testo che illustra lo scopo dell'applicazione livello dati. Quando si distribuisce un'applicazione livello dati, la descrizione viene archiviata nel database di `msdb` e può essere visualizzata successivamente nel nodo **applicazioni livello dati** di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **\< indietro** : consente di tornare alla pagina **Introduzione** .  
  
 **Avanti >** : consente di verificare che sia possibile compilare un'applicazione livello dati dagli oggetti nel database e di visualizzare i risultati nella pagina **Convalida e riepilogo**.  
  
 **Annulla** : consente di terminare la procedura guidata senza registrare l'applicazione livello dati.  
  
##  <a name="Summary"></a> Pagina Convalida e riepilogo  
 Utilizzare questa pagina per verificare le azioni eseguite dalla procedura guidata durante la registrazione dell'applicazione livello dati. La pagina passa attraverso tre stati per verificare se un'applicazione livello dati possa essere compilata dagli oggetti contenuti nel database.  
  
### <a name="retrieving-objects"></a>Recupero degli oggetti  
 **Recupero di oggetti database e server.** - Consente di visualizzare un indicatore di stato durante il recupero di tutti gli oggetti richiesti dal database e dall'istanza del Motore di database.  
  
 **\< indietro** : consente di tornare alla pagina **Imposta proprietà** per modificare le voci.  
  
 **Avanti>** : consente di registrare l'applicazione livello dati e visualizzare i risultati nella pagina **Registra applicazione livello dati**.  
  
 **Annulla** : consente di terminare la procedura guidata senza registrare l'applicazione livello dati.  
  
### <a name="validating-objects"></a>Convalida degli oggetti  
 **Controllo di**  _SchemaName_ **.** _ObjectName_ **.** - Consente di visualizzare un indicatore di stato durante la verifica delle dipendenze degli oggetti recuperati e della loro validità per l'applicazione livello dati. _NomeSchema_ **.** _NomeOggetto_ identifica l'oggetto attualmente sottoposto a verifica.  
  
 **\< indietro** : consente di tornare alla pagina **Imposta proprietà** per modificare le voci.  
  
 **Avanti>** : consente di registrare l'applicazione livello dati e visualizzare i risultati nella pagina **Registra applicazione livello dati**.  
  
 **Annulla** : consente di terminare la procedura guidata senza registrare l'applicazione livello dati.  
  
### <a name="summary"></a>Riepilogo  
 **Per la registrazione dell'applicazione livello dati verranno utilizzate le impostazioni seguenti.** - Consente di visualizzare un report delle proprietà e degli oggetti che verranno inclusi nell'applicazione livello dati.  
  
 **Salva report** consente di salvare una copia del report di convalida come file HTML. La cartella predefinita, **SQL Server Management Studio\DAC Packages** , si trova all'interno della cartella Documenti dell'account di Windows.  
  
 **\< indietro** : consente di tornare alla pagina **Imposta proprietà** per modificare le voci.  
  
 **Avanti>** : consente di registrare l'applicazione livello dati e visualizzare i risultati nella pagina **Registra applicazione livello dati**.  
  
 **Annulla** : consente di terminare la procedura guidata senza registrare l'applicazione livello dati.  
  
##  <a name="Register"></a> Pagina Registra DAC  
 In questa pagina viene riportato l'esito positivo o negativo della registrazione.  
  
 **Registrazione dell'applicazione livello dati** : consente di visualizzare l'esito positivo o negativo di ogni azione eseguita per la registrazione dell'applicazione livello dati. Verificare le informazioni che determinano l'esito positivo o negativo di ciascuna azione. Ogni azione che ha rilevato un errore avrà un collegamento nella colonna **Risultato** . Selezionare il collegamento per visualizzare un report dell'errore per l'azione.  
  
 **Salva report** consente di salvare il report della registrazione come file HTML. Nel file viene riportato lo stato di ogni azione, inclusi tutti gli errori generati da qualsiasi azione. La cartella predefinita, **SQL Server Management Studio\DAC Packages** , si trova all'interno della cartella Documenti dell'account di Windows. Il nome del file è nel formato \<NomePacchettoDAC>_RegisterDACReport_aaaammgg, dove \<*NomePacchettoDAC*> è il nome del pacchetto da distribuire, *aaaa* indica l'anno corrente, *mm* il mese corrente e *gg* il giorno corrente.  
  
 **Fine** : consente di terminare la procedura guidata.  
  
##  <a name="RegisterDACPowerShell"></a> Registrare un'applicazione livello dati tramite PowerShell  
 **Per registrare un database come applicazione livello dati usando il metodo Register() in uno script di PowerShell**  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza contenente il database che si desidera registrare come applicazione livello dati.  
  
2.  Aggiungere una variabile che specifichi il nome del database.  
  
3.  Specificare i metadati per l'applicazione livello dati, quali nome dell'applicazione livello dati, versione e descrizione.  
  
4.  Eseguire il metodo Register con le informazioni specificate in precedenza.  
  
### <a name="example-powershell"></a>Esempio (PowerShell)  
 Nell'esempio seguente viene registrato un database denominato MyDB come applicazione livello dati.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](data-tier-applications.md)  
