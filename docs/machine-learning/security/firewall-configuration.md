---
title: Configurazione del firewall
description: Come configurare il firewall per le connessioni in uscita da Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/17/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f8cf14b294c85f90b0e44375f751a84a50b30e04
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180418"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configurazione del firewall per Machine Learning Services per SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questo articolo elenca alcune considerazioni sulla configurazione del firewall che l'amministratore o l'architetto deve tenere in considerazione quando usa Machine Learning Services.

## <a name="default-firewall-rules"></a>Regole del firewall predefinite

Per impostazione predefinita, il programma di installazione di SQL Server disabilita le connessioni in uscita creando regole del firewall.

In SQL Server 2016 and 2017, queste regole sono basate sugli account utente locali, in cui il programma di installazione creava una regola in uscita per **SQLRUserGroup** che negava l'accesso alla rete ai suoi membri. Ogni account di lavoro era elencato come principio locale soggetto alla regola. Per altre informazioni su SQLRUserGroup, vedere [Panoramica della sicurezza per il framework di estendibilità in Machine Learning Services per SQL Server](../../machine-learning/concepts/security.md#sqlrusergroup).

In SQL Server 2019, in seguito al passaggio alla tecnologia AppContainer, sono disponibili nuove regole del firewall basate sui SID di AppContainer: una per ognuno dei 20 AppContainer creati dal programma di installazione di SQL Server. Per il nome della regola del firewall viene usata la convenzione di denominazione **Blocca accesso alla rete per AppContainer-00 nell'istanza di SQL Server MSSQLSERVER**, dove 00 è il numero dell'ambiente AppContainer (00-20 per impostazione predefinita) e MSSQLSERVER è il nome dell'istanza di SQL Server.

> [!Note]
> Se sono necessarie chiamate di rete, è possibile disabilitare le regole in uscita in Windows Firewall.

## <a name="restrict-network-access"></a>Limitare l'accesso alla rete

In un'installazione predefinita si usa una regola del firewall di Windows per bloccare tutto l'accesso alla rete in uscita da processi di runtime esterni. È consigliabile creare regole del firewall per impedire che i processi di runtime scarichino pacchetti o eseguano altre chiamate di rete che potrebbero essere potenzialmente dannose.

Se si usa un programma firewall diverso, è anche possibile creare regole per bloccare la connessione di rete in uscita per runtime esterni, impostando regole per gli account utente locali o per il gruppo rappresentato dal pool di account utente.

È consigliabile attivare Windows Firewall (o un altro firewall preferito) per impedire l'accesso illimitato alla rete da parte dei runtime R o Python.

## <a name="next-steps"></a>Passaggi successivi

[Configurare Windows Firewall per le connessioni in ingresso](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)