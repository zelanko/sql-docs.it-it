---
title: Configurare log degli errori di SQL Server | Microsoft Docs
description: Informazioni sul riciclo dei log degli errori. Scoprire come impostare le dimensioni massime del file di log e come impostare il numero di file di log precedenti di cui SQL Server esegue il backup e l'archiviazione.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 060b3828c772a030ab095ae1bea857dc8eaa3b5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651376"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>Gestione configurazione SQL Server - Configurare log degli errori di SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento viene descritto come visualizzare o modificare la modalità di riciclo dei log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Per aprire la finestra di dialogo Configura log degli errori di SQL Server  

1. In Esplora oggetti espandere l'istanza di SQL Server, espandere **Gestione**, fare clic con il pulsante destro del mouse su **Log di SQL Server**e quindi scegliere **Configura**.

2. Nella finestra di dialogo **Configura log degli errori di SQL Server** , scegliere dalle opzioni seguenti.

    a. Conteggio file di log

      **Limita il numero di file di log degli errori creati prima di essere riciclati**

      Selezionare questa opzione per limitare il numero di log degli errori creati prima di essere riciclati. Ogni volta che viene avviata un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene creato un nuovo log degli errori. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene backup dei sei log precedenti, a meno che non si selezioni questa opzione e non si specifichi un diverso numero massimo di log degli errori tramite l'opzione seguente.  
  
      **Numero massimo di file di log degli errori**

      Specificare il numero massimo di file di log degli errori archiviati creati prima che vengano riciclati. Il valore predefinito è 6, escluso quello corrente. Questo valore determina il numero di log di backup precedenti conservati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima del riciclo.

    b. Dimensioni file di log

      **Dimensioni massime del file di log degli errori in KB**

      È possibile impostare le dimensioni per ogni file in KB. Se si lascia 0, le dimensioni del log sono illimitate.
