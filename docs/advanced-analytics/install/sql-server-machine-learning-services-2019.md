---
title: Differenze in SQL Server 2019 - SQL Server Machine Learning Services
description: Scopri quali sono le novità per R e Python SQL Server machine learning le estensioni nella versione di anteprima di SQL Server 2019.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 43d427129cae773fc17a0d73f57a26144b7cd09f
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141420"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>Differenze nell'installazione di SQL Server Machine Learning Services in SQL Server 2019  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In Windows, il programma di installazione di SQL Server 2019 cambia il meccanismo di isolamento per i processi esterni. Questa modifica sostituisce gli account di lavoro locale con [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), una tecnologia di isolamento per le applicazioni client in esecuzione su Windows. 

Non sono presenti elementi azione specifica per l'amministratore a seguito della modifica. In un server nuovo o aggiornato, tutti gli script esterni e il codice eseguito da [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) seguire automaticamente il nuovo modello di isolamento. 

Riepilogo, le differenze principali in questa versione sono:

+ Account utente locali sotto **gruppo di utenti limitati SQL (SQLRUserGroup)** vengono creati o utilizzati per eseguire i processi esterni non sono più. AppContainers sostituirli.
+ **SQLRUserGroup** appartenenza è stato modificato. Invece di più account utente locale, l'appartenenza è costituito da solo l'account del servizio Launchpad di SQL Server. I processi R e Python eseguito ora con l'identità del servizio Launchpad isolato tramite AppContainers.

Anche se è stato modificato il modello di isolamento, i parametri di procedura guidata e riga di comando di installazione sono uguali in SQL Server 2019. Per informazioni sull'installazione, vedere [installare SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Sull'isolamento AppContainer

Nelle versioni precedenti **SQLRUserGroup** contenuti di un pool di Windows gli account utente locali (MSSQLSERVER00 MSSQLSERVER20) usato per isolare e l'esecuzione di processi esterni. Quando era necessario un processo esterno, servizio Launchpad di SQL Server potrebbe richiedere un account disponibile e utilizzarlo per eseguire un processo. 

In SQL Server 2019, il programma di installazione non crea più account di lavoro locale. Al contrario, l'isolamento viene ottenuto tramite [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). In fase di esecuzione degli script incorporati o il codice quando viene rilevata in una stored procedure o query, SQL Server chiama Launchpad con una richiesta per un'utilità di avvio specifiche dell'estensione. Finestra di avvio richiama l'ambiente di runtime appropriato in un processo con la propria identità e crea un'istanza di un AppContainer per contenerlo. Questa modifica è vantaggiosa perché Gestione account e una password locale non è più necessaria. Inoltre, nelle installazioni dei componenti in cui non sono consentiti gli account utente locali, azzerare la dipendenza dall'account utente locale significa che è ora possibile usare questa funzionalità.

Come è implementato da SQL Server, AppContainers sono un meccanismo interno. Sono disponibili per constatare fisico AppContainers in Monitoraggio di processo, è possibile trovarli nelle regole del firewall in uscita create dal programma di installazione per impedire l'esecuzione di chiamate di rete di processi.

## <a name="firewall-rules-created-by-setup"></a>Regole del firewall create dal programma di installazione

Per impostazione predefinita, SQL Server disabilita le connessioni in uscita tramite la creazione di regole del firewall. In passato, queste regole sono basate su account utente locali, in cui il programma di installazione creato una regola in uscita per **SQLRUserGroup** che negato l'accesso alla rete per i relativi membri (ogni account di lavoro è stato elencato come un principio soggetti al rule_ locale. 

Come parte del passaggio a AppContainers, sono disponibili nuove regole del firewall basate su AppContainer SIDs: uno per ognuno dei 20 AppContainers creato dal programma di installazione di SQL Server. Le convenzioni di denominazione per il nome della regola firewall **bloccare l'accesso alla rete per AppContainer 00 in SQL Server instance MSSQLSERVER**, dove 00 corrisponde al numero di AppContainer (00-20 per impostazione predefinita), e MSSQLSERVER è il nome di SQL Istanza del server. 

> [!Note]
> Se le chiamate di rete sono necessari, è possibile disabilitare le regole in uscita nel Firewall di Windows.

## <a name="program-file-permissions"></a>Autorizzazioni di file di programma

Come con le versioni precedenti, il **SQLRUserGroup** continua a fornire lettura e autorizzazioni di esecuzione dei file eseguibili di SQL Server **Binn**, **R_SERVICES**e  **PYTHON_SERVICES** le directory. In questa versione, l'unico membro del **SQLRUserGroup** è l'account del servizio Launchpad di SQL Server.  Quando il servizio Launchpad viene avviato un ambiente di esecuzione R o Python, il processo viene eseguito come servizio LaunchPad.

## <a name="implied-authentication"></a>Autenticazione implicita

Come in precedenza, è comunque necessaria per una configurazione aggiuntiva *l'autenticazione implicita* nei casi in cui uno script o codice ha per la connessione al Server SQL Usa l'autenticazione attendibile per recuperare dati o risorse. La configurazione aggiuntiva comporta la creazione di un accesso al database per **SQLRUserGroup**, il cui unico membro è ora il singolo account di servizio Launchpad di SQL Server invece di più account di lavoro. Per altre informazioni su questa attività, vedere [aggiungere SQLRUserGroup come utente del database](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Collegamento simbolico creato dal programma di installazione

Per impostazione predefinita corrente viene creato un collegamento simbolico **R_SERVICES** e **PYTHON_SERVICES** come parte del programma di installazione di SQL Server. Se non si desidera creare questo collegamento, un'alternativa consiste nel concedere l'autorizzazione di lettura di 'tutti i pacchetti di applicazioni' alla gerarchia che hanno contribuito alla cartella.


## <a name="see-also"></a>Vedere anche

+ [Installare SQL Server Machine Learning Services in Windows](sql-machine-learning-services-windows-install.md)

+ [Installare SQL Server 2019 servizi Machine Learning in Linux](../../linux/sql-server-linux-setup-machine-learning.md)
