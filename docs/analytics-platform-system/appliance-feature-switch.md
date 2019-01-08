---
title: Opzione della funzionalità (sistema di piattaforma Analitica)
description: Visualizza le informazioni sulle opzioni di due funzionalità che sono stati introdotti in AU7 sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 98a59677267cc2692be7de7e6141e85ec415e61d
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53597059"
---
# <a name="appliance-feature-switches"></a>Opzioni di funzionalità delle Appliance
Il **opzione della funzionalità** pagina vengono visualizzate informazioni sulle opzioni di funzionalità che sono stati introdotti in AU7 sistema di piattaforma Analitica e versioni successive. Utilizzare questa pagina di configurazione per aggiornare o attivare/disabilitare funzionalità e impostazioni di sistema di piattaforma Analitica. 

> [!NOTE]
> Modifiche ai valori della funzionalità commutatore richiedono un riavvio del servizio.

![Opzione della funzionalità Appliance DWConig](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig Appliance funzionalità commutatore") 

## <a name="autostatsenabled"></a>AutoStatsEnabled
Controlla la funzionalità statistiche automatico. Questa opzione della funzionalità è impostata su true per impostazione predefinita dopo l'aggiornamento a AU7. Qualsiasi database creato dopo l'aggiornamento erediterà la creazione automatica e l'aggiornamento asincrono delle statistiche. Per i database esistenti, gli amministratori di database possono abilitare statistiche automatico con [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Per altre informazioni sulle statistiche, vedere [statistiche](../relational-databases/statistics/statistics.md).

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries
Consente di selezionare le impostazioni maxdop maggiore di 1 per le operazioni insert/select. Opzioni per questa impostazione sono 0, 1, 2 e 4, con valore predefinito è 1.

##<a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions
Migliora le prestazioni delle query eliminando lo spostamento dei dati per sottoespressione comuni in query optimizer di SQL. Una descrizione dettagliata di questa funzionalità è reperibile [qui](common-sub-expression-elimination.md).

## <a name="usecatalogqueries"></a>UseCatalogQueries
Utilizzando oggetti del catalogo per alcune chiamate di metadati anziché l'utilizzo di SMO è stato illustrato il miglioramento delle prestazioni. Impostato su true per impostazione predefinita in CU7.1, questa opzione controlla questo comportamento. 

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds
Controlla il tempo Data Movement Service (DMS) è in attesa per la sincronizzazione in un sistema occupato all'annullamento di una query che implica lo spostamento dei dati. L'aggiornamento a AU7 imposta questo valore per 900 secondi (15 minuti) per impostazione predefinita. L'intervallo valido è 0 - 3600 secondi.
