---
title: Configurazione del firewall, servizi di SQL Server Machine Learning
description: Come configurare il firewall per le connessioni in uscita da servizi di SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fc89855364e8bfdb2c1e5de1f58d87ae57886db9
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431944"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configurazione del firewall per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra considerazioni sulla configurazione del firewall che l'amministratore o il progettista deve tenere presente quando si usa servizi di machine learning.

## <a name="default-firewall-rules"></a>Regole del firewall predefinite

Per impostazione predefinita, il programma di installazione di SQL Server disabilita le connessioni in uscita tramite la creazione di regole del firewall.

In SQL Server 2016 e 2017, queste regole sono basate su account utente locale, in cui il programma di installazione creato una regola in uscita per **SQLRUserGroup** che negato l'accesso alla rete per i relativi membri (ogni account di lavoro è stato elencato come un principio soggetto a locale la regola. Per altre informazioni sulle SQLRUserGroup, vedere [Panoramica sulla sicurezza per il framework di estendibilità in SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#sqlrusergroup).

In SQL Server 2019, come parte del passaggio a AppContainers, sono disponibili nuove regole del firewall basate su AppContainer SIDs: uno per ognuno dei 20 AppContainers creato dal programma di installazione di SQL Server. Le convenzioni di denominazione per il nome della regola firewall **bloccare l'accesso alla rete per AppContainer 00 in SQL Server instance MSSQLSERVER**, dove 00 corrisponde al numero di AppContainer (00-20 per impostazione predefinita), e MSSQLSERVER è il nome di SQL Istanza del server.

> [!Note]
> Se le chiamate di rete sono necessari, è possibile disabilitare le regole in uscita nel Firewall di Windows.

## <a name="restrict-network-access"></a>Limitare l'accesso alla rete

In un'installazione predefinita, una regola del firewall Windows consente di bloccare completamente l'accesso di rete in uscita dai processi di runtime esterni. Le regole del firewall devono essere create per evitare che i processi del runtime esterni scarichi pacchetti o effettui altre chiamate di rete che potrebbero essere potenzialmente dannose.

Se si usa un programma firewall diverso, è anche possibile creare regole per bloccare la connessione di rete in uscita per i runtime esterni, impostando le regole per gli account utente locale o per il gruppo rappresentato dal pool di account utente.

Si consiglia di attivare Windows Firewall (o un altro firewall di propria scelta) per impedire l'accesso alla rete senza restrizioni per i runtime di R o Python.

## <a name="next-steps"></a>Passaggi successivi

[Configurare Windows firewall per le connessioni in ingresso](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)