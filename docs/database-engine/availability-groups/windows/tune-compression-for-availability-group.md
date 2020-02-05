---
title: Ottimizzare la compressione per un gruppo di disponibilità | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 7632769c-b246-4766-886f-7c60ec540be8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3891d30ef5bfffb19ca1d4bfcaab290e3903816b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68013671"
---
# <a name="tune-compression-for-availability-group"></a>Ottimizzare la compressione per un gruppo di disponibilità
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Per impostazione predefinita, SQL Server comprime i flussi di dati quando opportuno per i gruppi di disponibilità. La compressione riduce il traffico di rete, aumenta il carico della CPU e può generare latenza. Per abilitare la compressione, è necessario essere membro del ruolo predefinito del server sysadmin. La tabella seguente illustra i casi in cui SQL Server usa la compressione per i flussi di log dei gruppi di disponibilità.

| Scenario | Impostazione compressione
| ---- | ----
| Replica con commit sincrono | Nessuna compressione
| Repliche con commit asincrono | Compresso
| Durante il seeding automatico | Nessuna compressione

## <a name="trace-flags-for-availability-group-compression"></a>Flag di traccia per la compressione dei gruppi di disponibilità 

Per la maggior parte degli scenari, non è consigliabile modificare queste impostazioni. Per testarne la modifica è possibile usare flag di traccia globali. SQL Server applica i flag di traccia globali all'intera istanza. Queste impostazioni influiranno su tutti i gruppi di disponibilità dell'istanza.  

La tabella seguente illustra i flag di traccia che modificheranno il comportamento di compressione predefinito in SQL Server. 

Flag di traccia | Descrizione
------------- | -------------
1462          | Disabilita la compressione dei flussi di log per i gruppi di disponibilità con repliche asincrone. Per impostazione predefinita, questa funzionalità è abilitata per le repliche asincrone per ottimizzare la larghezza di banda di rete.
9567          | Abilita la compressione del flusso di dati per i gruppi di disponibilità durante il seeding automatico. Durante il seeding automatico, la compressione può ridurre significativamente i tempi di trasferimento e aumenta il carico sul processore.
9592          | Abilita la compressione dei flussi di log per i gruppi di disponibilità con repliche sincrone. Per impostazione predefinita, questa funzionalità è disabilitata per le repliche sincrone perché la compressione aggiunge latenza. La compressione dei flussi di log è abilitata per impostazione predefinita per le repliche asincrone.


## <a name="resources"></a>Risorse


[Opzioni di avvio del motore di database](../../../database-engine/configure-windows/database-engine-service-startup-options.md)

[Seeding automatico](https://msdn.microsoft.com/library/mt735149(SQL.130).aspx)

[Prerequisiti per AlwaysOn](prereqs-restrictions-recommendations-always-on-availability.md) 
