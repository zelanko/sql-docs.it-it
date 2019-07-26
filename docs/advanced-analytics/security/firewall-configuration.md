---
title: Configurazione del firewall
description: Come configurare il firewall per le connessioni in uscita da SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 754e243f45965801b9295d2b40a920d52bd2c95c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469860"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configurazione del firewall per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo elenca le considerazioni sulla configurazione del firewall che l'amministratore o l'architetto deve tenere in considerazione quando usa i servizi di machine learning.

## <a name="default-firewall-rules"></a>Regole del firewall predefinite

Per impostazione predefinita, il programma di installazione di SQL Server disabilita le connessioni in uscita creando le regole del firewall.

In SQL Server 2016 e 2017 queste regole sono basate su account utente locali, dove il programma di installazione ha creato una regola in uscita per **SQLRUserGroup** che ha negato l'accesso alla rete ai propri membri (ogni account di lavoro è stato elencato come principio locale soggetto alla regola. Per ulteriori informazioni su SQLRUserGroup, vedere [Cenni preliminari sulla sicurezza per il Framework di estendibilità in SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#sqlrusergroup).

In SQL Server 2019, come parte del passaggio a AppContainers, sono disponibili nuove regole del firewall basate sui SID di AppContainer: una per ognuno dei 20 AppContainers creati da SQL Server installazione. Le convenzioni di denominazione per il nome della regola firewall sono **Blocca accesso alla rete per appcontainer-00 in SQL Server istanza MSSQLSERVER**, dove 00 è il numero di AppContainer (00-20 per impostazione predefinita) e MSSQLServer è il nome dell'istanza di SQL Server.

> [!Note]
> Se sono necessarie chiamate di rete, è possibile disabilitare le regole in uscita in Windows Firewall.

## <a name="restrict-network-access"></a>Limitazione dell'accesso alla rete

In un'installazione predefinita, una regola di Windows Firewall viene utilizzata per bloccare l'accesso alla rete in uscita dai processi di runtime esterni. È necessario creare regole del firewall per impedire che i processi di runtime esterni scarichino pacchetti o possano effettuare altre chiamate di rete potenzialmente dannose.

Se si usa un programma firewall diverso, è anche possibile creare regole per bloccare la connessione di rete in uscita per i runtime esterni, impostando regole per gli account utente locali o per il gruppo rappresentato dal pool di account utente.

È consigliabile attivare Windows Firewall (o un altro firewall di propria scelta) per impedire l'accesso alla rete senza restrizioni da parte dei runtime di R o Python.

## <a name="next-steps"></a>Passaggi successivi

[Configurare Windows Firewall per le connessioni in ingresso](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)