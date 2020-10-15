---
title: Connessione ad Azure Arc
titleSuffix: ''
description: Connettere un'istanza di SQL Server ad Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: d5b66ac431bfadff06c930f76517f35d95dcb12f
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987997"
---
# <a name="connect-your-sql-server-to-azure-arc"></a>Connettere l'istanza SQL Server ad Azure Arc

È possibile connettere l'istanza di SQL Server locale ad Azure Arc seguendo questa procedura.

## <a name="prerequisites"></a>Prerequisiti

* Nel computer è installata almeno un'istanza di SQL Server.
* Per i computer Windows è installato Azure PowerShell. Seguire le istruzioni per [l'installazione di Azure PowerShell](/powershell/azure/install-az-ps).
* Per i computer Linux è stata scaricata l'interfaccia della riga di comando di Azure e l'account Azure è stato connesso. Seguire le istruzioni per [l'installazione dell'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli-apt).


## <a name="generate-a-registration-script-for-sql-server"></a>Generare uno script di registrazione per SQL Server

In questo passaggio viene generato uno script che trova tutte le istanze di SQL Server installate nel computer e le registra come risorse __SQL Server - Azure Arc__. Se la macchina virtuale o fisica host non è registrata con Azure Arc, lo script esegue automaticamente la registrazione.

1. Cercare il tipo di risorsa __SQL Server - Azure Arc__ e aggiungere una nuova risorsa tramite il pannello di creazione.

![Avviare la creazione](media/join/start-creation-of-sql-server-azure-arc-resource.png)
    
2. Esaminare i prerequisiti e passare alla scheda**Dettagli server**.  

3. Selezionare la sottoscrizione, il gruppo di risorse, l'area di Azure e il sistema operativo host. Se necessario, specificare anche il proxy che la rete usa per connettersi a Internet.

> [!IMPORTANT]
> Se il computer che ospita l'istanza di SQL Server è già [connesso ad Azure Arc](/azure/azure-arc/servers/onboard-portal), assicurarsi di selezionare lo stesso gruppo di risorse che contiene la risorsa __Computer - Azure Arc__ corrispondente.

![Dettagli del server](media/join/server-details-sql-server-azure-arc.png)

4. Passare alla scheda **Esegui script** e scaricare lo script di registrazione visualizzato. Il portale genera lo script per il sistema operativo host specificato.

![Scaricare lo script](media/join/download-script-sql-server-azure-arc.png)

## <a name="connect-the-installed-sql-server-instances-to-azure-arc"></a>Connettere ad Azure Arc le istanze di SQL Server installate

In questo passaggio lo script scaricato da portale di Azure verrà eseguito nel computer fisico o nella macchina virtuale di destinazione. Di conseguenza ogni istanza di SQL Server installata nel computer verrà registrata come risorsa __SQL Server - Azure Arc__. Se inoltre nel computer non è installato l'agente di configurazione guest, questo verrà installato automaticamente e registrato come risorsa __Computer - Azure Arc__.

> [!NOTE]
> Assicurarsi di eseguire lo script con un account che soddisfi i requisiti minimi di autorizzazione descritti nei [prerequisiti](overview.md#prerequisites).

### <a name="windows"></a>WINDOWS

1. Avviare un'istanza di amministrazione di __powershell.exe__ e accedere al modulo PowerShell con le credenziali di Azure. Seguire le [istruzioni di accesso](/powershell/azure/install-az-ps#sign-in).

2. Eseguire lo script scaricato

   ```powershell
   & '.\RegisterSqlServerArc.ps1'
   ```

   > [!NOTE]
   > Se non è stato installato in precedenza il modulo AZ per PowerShell, è possibile che alla prima esecuzione si verifichino dei problemi. In tal caso, seguire le istruzioni nello script per installare e connettere l'account e quindi eseguire di nuovo lo script.

### <a name="linux"></a>Linux

1. Usare l'interfaccia della riga di comando di Azure per accedere con le credenziali di Azure. Seguire le [istruzioni per l'accesso](/cli/azure/authenticate-azure-cli).

2. Concedere l'autorizzazione di esecuzione allo script scaricato ed eseguirlo.

   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="register-sql-server-instances-on-multiple-machines"></a>Registrare istanze di SQL Server su più computer

È possibile connettere ad Azure Arc più istanze di SQL Server installate in più computer Windows o Linux usando lo stesso script generato per un singolo computer. Seguire le istruzioni per [connettere istanze di SQL Server ad Azure Arc su larga scala](connect-at-scale.md).

## <a name="validate-the-sql-server---azure-arc-resources"></a>Convalidare le risorse di SQL Server - Azure Arc

Passare al [portale di Azure](https://ms.portal.azure.com/#home) e aprire la risorsa __SQL Server - Azure Arc__ appena registrata per la convalida.

![Convalida di SQL Server connesso ](media/join/validate-sql-server-azure-arc.png)

## <a name="un-register-the-sql-server---azure-arc-resources"></a>Annullare la registrazione delle risorse SQL Server - Azure Arc

Per rimuovere una risorsa __SQL Server - Azure Arc__ esistente, passare al gruppo di risorse che la contiene e rimuoverla dall'elenco delle risorse del gruppo.

![Annullare la registrazione di SQL Server](media/join/delete-sql-server-azure-arc.png)

## <a name="next-steps"></a>Passaggi successivi

* [Configurare la sicurezza dei dati avanzata per l'istanza di SQL Server](configure-advanced-data-security.md)

* [Configurare Valutazione SQL su richiesta per l'istanza di SQL Server](assess.md)