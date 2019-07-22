---
title: Installare PolyBase in Windows | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, installation
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 9538ad04a6e9e1e95a1fafc1080d132e218a196d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062204"
---
# <a name="install-polybase-on-windows"></a>Installare PolyBase in Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Per installare una versione di valutazione di SQL Server, visitare [SQL Server Valutazioni](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016). 
   
## <a name="prerequisites"></a>Prerequisites  
   
- Copia di valutazione di SQL Server a 64 bit.  
   
- Microsoft .NET Framework 4.5.  

- Oracle Java SE Runtime Environment (JRE). Sono supportate le versioni 7 (a partire da 7.51) e 8. Funzionano sia [JRE](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) che [Server JRE](https://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html). Passare a [Java SE downloads](https://www.oracle.com/technetwork/java/javase/downloads/index.html)(Download di Java SE). Se JRE non è presente, il programma di installazione ha esito negativo. JRE9 e JRE10 non sono supportati.

- Memoria minima: 4 GB. 
   
- Spazio su disco rigido minimo: 2 GB.
  
- Consigliata: Almeno 16 GB di RAM.
   
- Polybase funziona correttamente se è abilitato il protocollo TCP/IP. TCP/IP è abilitato per impostazione predefinita in tutte le edizioni di SQL Server tranne le edizioni Developer e SQL Server Express. Perché PolyBase funzioni correttamente nelle edizioni Developer ed Express è necessario abilitare la connettività TCP/IP. Vedere [Abilitare o disabilitare un protocollo di rete del server](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


>[!NOTE] 
> È possibile installare PolyBase in una sola istanza di SQL Server per computer.


>[!NOTE]
>Per usare PolyBase, sono necessarie le autorizzazioni a livello di CONTROLLO SERVER o sysadmin per il database.

>[!IMPORTANT]
>Per usare la funzionalità di distribuzione di calcolo su Hadoop, il cluster Hadoop di destinazione deve disporre dei componenti principali di HDFS, YARN e MapReduce con il server della cronologia processo abilitato. PolyBase invia la query di distribuzione tramite MapReduce e recupera lo stato dal server della cronologia processo. Senza uno dei due componenti la query ha esito negativo.
  
## <a name="single-node-or-polybase-scale-out-group"></a>Singolo nodo o gruppo di scalabilità orizzontale di PolyBase

Prima di installare PolyBase nelle istanze di SQL Server, decidere se si vuole eseguire un'installazione in un singolo nodo o in un [gruppo con scalabilità orizzontale PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).

Per un gruppo con scalabilità orizzontale PolyBase, verificare le condizioni seguenti:

- Tutti i computer si trovano nello stesso dominio.
- Usare lo stesso account del servizio e la stessa password durante l'installazione di PolyBase.
- Le istanze di SQL Server possono comunicare tra loro in rete.
- Le istanze di SQL Server sono tutte della stessa versione di SQL Server.

Dopo aver installato PolyBase autonomo o in un gruppo di scalabilità orizzontale, non è possibile apportare modifiche. Per modificare questa impostazione, è necessario disinstallare e reinstallare la funzionalità.

## <a name="use-the-installation-wizard"></a>Usare l'installazione guidata
   
1. Eseguire il file di installazione setup.exe di SQL Server.   
   
2. Selezionare **Installazione**e quindi scegliere **Nuova installazione di SQL Server autonomo o aggiunta di funzionalità**.  
   
3. Nella pagina Selezione funzionalità scegliere **Servizio query PolyBase per i dati esterni**.  

   ![Servizi PolyBase](../../relational-databases/polybase/media/install-wizard.png "Servizi PolyBase")  
   
4. Nella pagina Configurazione server configurare il **servizio motore PolyBase di SQL Server** e **SQL Server PolyBase Data Movement Service** per l'esecuzione con lo stesso account di dominio.  

   >[!IMPORTANT]
   >In un gruppo con scalabilità orizzontale di PolyBase, il motore PolyBase e il servizio di spostamento dati di PolyBase su tutti i nodi devono essere eseguiti con lo stesso account di dominio. Vedere [Gruppi con scalabilità orizzontale di PolyBase](#enable).

5. Nella pagina Configurazione di PolyBase, selezionare una delle due opzioni. Per altre informazioni, vedere [Gruppi con scalabilità orizzontale di PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).  
   
   - Usare un'istanza di SQL Server come istanza abilitata di PolyBase autonoma.  
   
     Scegliere questa opzione per usare l'istanza di SQL Server come nodo head autonomo.  
   
   - Usare l'istanza di SQL Server come parte di un gruppo con scalabilità orizzontale di PolyBase. Questa opzione apre il firewall per consentire le connessioni in ingresso. Le connessioni sono consentite per il motore di database di SQL Server, il motore PolyBase di SQL Server, SQL Server PolyBase Data Movement Service e SQL Browser. Il firewall consente anche le connessioni in ingresso da altri nodi in un gruppo con scalabilità orizzontale di PolyBase.  
   
     Questa opzione abilita anche le connessioni al firewall di Microsoft Distributed Transaction Coordinator (MSDTC) e modifica le impostazioni del registro di MSDTC.  
   
6. Nella pagina Configurazione di PolyBase, specificare un intervallo di porte che comprenda almeno sei porte. L'installazione di SQL Server alloca le prime sei porte disponibili dell'intervallo.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

   >[!IMPORTANT]
   > Dopo l'installazione, è necessario [abilitare la funzionalità PolyBase](#enable).


##  <a name="installing"></a> Usare un prompt dei comandi

Usare i valori in questa tabella per creare gli script di installazione. Il servizio motore PolyBase di SQL Server e SQL Server PolyBase Data Movement Service devono essere eseguiti con lo stesso account. In un gruppo con scalabilità orizzontale di PolyBase, i servizi di PolyBase su tutti i nodi devono essere eseguiti con lo stesso account di dominio.  
   
<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017"

|componente di SQL Server|Parametro e valori|Descrizione|  
|--------------------------|--------------------------|-----------------|  
|Controllo dell'installazione di SQL Server|**Required**<br /><br /> /FEATURES=PolyBase|Viene selezionata la funzionalità PolyBase.|  
|servizio motore PolyBase di SQL Server|**Facoltativo**<br /><br /> /PBENGSVCACCOUNT|Viene specificato l'account per il servizio motore. L'impostazione predefinita è **NT Authority\NETWORK SERVICE**.|  
|Motore di PolyBase per SQL Server|**Facoltativo**<br /><br /> /PBENGSVCPASSWORD|Viene specificata la password per l'account del servizio motore.|  
|Motore di PolyBase per SQL Server|**Facoltativo**<br /><br /> /PBENGSVCSTARTUPTYPE|Viene specificata la modalità di avvio per il motore PolyBase: Automatico (predefinito), disabilitato e manuale.|  
|SQL Server PolyBase Data Movement |**Facoltativo**<br /><br /> /PBDMSSVCACCOUNT|Viene specificato l'account per il servizio di spostamento dati. L'impostazione predefinita è **NT Authority\NETWORK SERVICE**.|  
|SQL Server PolyBase Data Movement |**Facoltativo**<br /><br /> /PBDMSSVCPASSWORD|Viene specificata la password per l'account di spostamento dati.|  
|SQL Server PolyBase Data Movement |**Facoltativo**<br /><br /> /PBDMSSVCSTARTUPTYPE|Viene specificata la modalità di avvio per il servizio di spostamento dati: Automatico (predefinito), disabilitato e manuale.|  
|PolyBase|**Facoltativo**<br /><br /> /PBSCALEOUT|Viene indicato se l'istanza di SQL Server viene usata come parte di un gruppo di calcolo con scalabilità orizzontale di PolyBase. <br />Valori supportati: True, False.|  
|PolyBase|**Facoltativo**<br /><br /> /PBPORTRANGE|Viene specificato un intervallo di porte con almeno sei porte per i servizi PolyBase. Esempio:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

|componente di SQL Server|Parametro e valori|Descrizione|  
|--------------------------|--------------------------|-----------------|  
|Controllo dell'installazione di SQL Server|**Obbligatorio**<br /><br /> /FEATURES=PolyBaseCore, PolyBaseJava, PolyBase | PolyBaseCore installa il supporto per tutte le funzionalità di PolyBase, ad eccezione della connettività Hadoop. PolyBaseJava abilita la connettività Hadoop. PolyBase installa entrambe le funzionalità. |  
|Motore di PolyBase per SQL Server|**Facoltativo**<br /><br /> /PBENGSVCACCOUNT|Viene specificato l'account per il servizio motore. L'impostazione predefinita è **NT Authority\NETWORK SERVICE**.|  
|Motore di PolyBase per SQL Server|**Facoltativo**<br /><br /> /PBENGSVCPASSWORD|Viene specificata la password per l'account del servizio motore.|  
|Motore di PolyBase per SQL Server|**Facoltativo**<br /><br /> /PBENGSVCSTARTUPTYPE|Viene specificata la modalità di avvio per il motore PolyBase: Automatico (predefinito), disabilitato e manuale.|  
|SQL Server PolyBase Data Movement |**Facoltativo**<br /><br /> /PBDMSSVCACCOUNT|Viene specificato l'account per il servizio di spostamento dati. L'impostazione predefinita è **NT Authority\NETWORK SERVICE**.|  
|SQL Server PolyBase Data Movement |**Facoltativo**<br /><br /> /PBDMSSVCPASSWORD|Viene specificata la password per l'account di spostamento dati.|  
|SQL Server PolyBase Data Movement |**Facoltativo**<br /><br /> /PBDMSSVCSTARTUPTYPE|Viene specificata la modalità di avvio per il servizio di spostamento dati: Automatico (predefinito), disabilitato e manuale.|  
|PolyBase|**Facoltativo**<br /><br /> /PBSCALEOUT|Viene indicato se l'istanza di SQL Server viene usata come parte di un gruppo di calcolo con scalabilità orizzontale di PolyBase. <br />Valori supportati: True, False.|  
|PolyBase|**Facoltativo**<br /><br /> /PBPORTRANGE|Viene specificato un intervallo di porte con almeno sei porte per i servizi PolyBase. Esempio:<br /><br /> `/PBPORTRANGE=16450-16460`|  

::: moniker-end

Dopo l'installazione, è necessario [abilitare la funzionalità PolyBase](#enable).



**Esempio**

Questo esempio mostra un esempio di script di installazione.  

```cmd
   
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,PolyBase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
   
```  

## <a id="enable"></a> Abilitare PolyBase

Dopo l'installazione, è necessario abilitare PolyBase per accedere alle relative funzionalità. Per connettersi a SQL Server 2019 CTP 2.0 è necessario abilitare PolyBase dopo l'installazione. Usare il comando Transact-SQL seguente.


```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [ WITH OVERRIDE ]  ;
```
L'istanza deve quindi essere riavviata.


## <a name="post-installation-notes"></a>Note sulle operazioni successive all'installazione  

PolyBase installa tre database utente, DWConfiguration, DWDiagnostics e DWQueue. Questi database sono per l'uso con PolyBase. Non modificarli o eliminarli.  
   
### <a id="confirminstall"></a> Come confermare l'installazione  

Eseguire il comando seguente. Se installato, PolyBase restituisce 1; in caso contrario, restituisce 0.  

```sql  
SELECT SERVERPROPERTY ('IsPolyBaseInstalled') AS IsPolyBaseInstalled;  
```  

### <a name="firewall-rules"></a>Regole del firewall  

L'installazione di PolyBase di SQL Server crea sul computer le regole del firewall seguenti:  
   
- SQL Server PolyBase - Motore di database - \<NomeIstanzaSQLServer> (TCP-In)  
   
- SQL Server PolyBase - Servizi PolyBase - \<NomeIstanzaSQLServer> (TCP-In)  

- PolyBase di SQL Server - SQL Browser - (UDP-In)  
   
Al momento dell'installazione, se si usa l'istanza di SQL Server come parte di un gruppo di scalabilità orizzontale di PolyBase, queste regole sono attivate. Il firewall viene aperto per consentire le connessioni in ingresso. Tali connessioni sono consentite per il motore di database di SQL Server, il motore PolyBase di SQL Server, SQL Server PolyBase Data Movement Service e SQL Browser. Se il servizio firewall nel computer non è in esecuzione durante l'installazione, l'installazione di SQL Server non è in grado di attivare queste regole. In tal caso, avviare il servizio firewall sul computer e abilitare queste regole dopo l'installazione.  
   
#### <a name="to-enable-the-firewall-rules"></a>Per abilitare le regole del firewall  

1. Aprire il **Pannello di controllo**.  

2. Selezionare **Sistema e sicurezza** e selezionare **Windows Firewall**.  
   
3. Selezionare **Impostazioni avanzate**e selezionare **Regole connessioni in entrata**.  
   
4. Fare clic con il pulsante destro del mouse sulla regola disattivata e selezionare **Abilita regola**.  
   
### <a name="polybase-service-accounts"></a>Account del servizio PolyBase

Per modificare gli account del servizio per il motore PolyBase e PolyBase Data Movement Service, disinstallare e reinstallare la funzionalità PolyBase.

## <a name="next-steps"></a>Passaggi successivi  

Vedere [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md).
