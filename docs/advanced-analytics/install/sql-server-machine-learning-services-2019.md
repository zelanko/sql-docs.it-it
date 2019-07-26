---
title: Differenze in SQL Server 2019
description: Informazioni sulle novità di R e Python SQL Server le estensioni di Machine Learning nella versione di anteprima SQL Server 2019.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 218ae9bd0685370f38942592fd32da75272fbcac
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470303"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>Differenze nell'installazione di SQL Server Machine Learning Services in SQL Server 2019  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In Windows il programma di installazione di SQL Server 2019 modifica il meccanismo di isolamento per i processi esterni. Questa modifica sostituisce gli account di lavoro locali con [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), una tecnologia di isolamento per le applicazioni client in esecuzione su Windows. 

Non sono presenti elementi di azione specifici per l'amministratore in seguito alla modifica. In un server nuovo o aggiornato tutti gli script esterni e il codice eseguito da [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) seguono automaticamente il nuovo modello di isolamento. 

Riepilogate, le principali differenze in questa versione sono:

+ Gli account utente locali nel **gruppo di utenti con restrizioni SQL (SQLRUserGroup)** non vengono più creati o usati per eseguire processi esterni. AppContainers sostituirli.
+ L'appartenenza a **SQLRUserGroup** è cambiata. Anziché più account utente locali, l'appartenenza è costituita solo dall'account del servizio Launchpad di SQL Server. I processi R e Python vengono ora eseguiti con l'identità del servizio Launchpad, isolati tramite AppContainers.

Anche se il modello di isolamento è stato modificato, la procedura guidata di installazione e i parametri della riga di comando rimangono invariati nella SQL Server 2019. Per informazioni sull'installazione, vedere [Install SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Informazioni sull'isolamento AppContainer

Nelle versioni precedenti, **SQLRUserGroup** conteneva un pool di account utente di Windows locali (MSSQLSERVER00-MSSQLSERVER20) usato per isolare ed eseguire i processi esterni. Quando è necessario un processo esterno, Launchpad di SQL Server servizio prende un account disponibile e lo usa per eseguire un processo. 

In SQL Server 2019, il programma di installazione non crea più account di lavoro locali. Viene invece realizzata l'isolamento tramite [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). In fase di esecuzione, quando il codice o lo script incorporato viene rilevato in una stored procedure o in una query, SQL Server chiama Launchpad con una richiesta per un'utilità di avvio specifica dell'estensione. Launchpad richiama l'ambiente di runtime appropriato in un processo con la relativa identità e crea un'istanza di un AppContainer per contenerlo. Questa modifica è vantaggiosa perché la gestione di account e password locali non è più necessaria. Inoltre, nelle installazioni in cui gli account utente locali non sono consentiti, l'eliminazione della dipendenza dell'account utente locale significa che è ora possibile usare questa funzionalità.

Come implementato da SQL Server, AppContainers sono un meccanismo interno. Sebbene non venga visualizzata la prova fisica di AppContainers in Process Monitor, è possibile trovarli nelle regole del firewall in uscita create dal programma di installazione per impedire ai processi di effettuare chiamate di rete.

## <a name="firewall-rules-created-by-setup"></a>Regole del firewall create dal programma di installazione

Per impostazione predefinita, SQL Server disabilita le connessioni in uscita creando le regole del firewall. In passato, queste regole sono basate sugli account utente locali, in cui il programma di installazione ha creato una regola in uscita per **SQLRUserGroup** che ha negato l'accesso alla rete ai propri membri. ogni account di lavoro è stato elencato come principio locale soggetto al rule_. 

Nell'ambito del passaggio a AppContainers sono disponibili nuove regole del firewall basate sui SID di AppContainer: una per ognuno dei 20 AppContainers creati dal programma di installazione di SQL Server. Le convenzioni di denominazione per il nome della regola firewall sono **Blocca accesso alla rete per appcontainer-00 in SQL Server istanza MSSQLSERVER**, dove 00 è il numero di AppContainer (00-20 per impostazione predefinita) e MSSQLServer è il nome dell'istanza di SQL Server. 

> [!Note]
> Se sono necessarie chiamate di rete, è possibile disabilitare le regole in uscita in Windows Firewall.

## <a name="program-file-permissions"></a>Autorizzazioni per i file di programma

Come per le versioni precedenti, il **SQLRUserGroup** continua a fornire autorizzazioni di lettura ed esecuzione per i file eseguibili nelle directory SQL Server **contenitori**, **R_SERVICES**e **PYTHON_SERVICES** . In questa versione, l'unico membro di **SQLRUserGroup** è l'account del servizio launchpad di SQL Server.  Quando il servizio Launchpad avvia un ambiente di esecuzione R o Python, il processo viene eseguito come servizio LaunchPad.

## <a name="implied-authentication"></a>Autenticazione implicita

Come prima, è ancora necessaria una configurazione aggiuntiva per *l'autenticazione implicita* nei casi in cui script o codice debbano riconnettersi a SQL Server usando l'autenticazione trusted per recuperare dati o risorse. La configurazione aggiuntiva comporta la creazione di un account di accesso al database per **SQLRUserGroup**, il cui unico membro è ora il singolo account del servizio launchpad di SQL Server anziché più account di lavoro. Per ulteriori informazioni su questa attività, vedere [aggiungere SQLRUserGroup come utente del database](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Collegamento simbolico creato dal programma di installazione

Viene creato un collegamento simbolico alle **R_SERVICES** predefinite correnti e **PYTHON_SERVICES** come parte del programma di installazione di SQL Server. Se non si desidera creare questo collegamento, un'alternativa consiste nell'concedere l'autorizzazione di lettura "tutti i pacchetti dell'applicazione" alla gerarchia che conduce alla cartella.


## <a name="see-also"></a>Vedere anche

+ [Installare SQL Server Machine Learning Services in Windows](sql-machine-learning-services-windows-install.md)

+ [Installare SQL Server Machine Learning Services 2019 in Linux](../../linux/sql-server-linux-setup-machine-learning.md)
