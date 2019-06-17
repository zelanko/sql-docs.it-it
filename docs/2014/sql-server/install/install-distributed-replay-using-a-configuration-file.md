---
title: Installare riesecuzione distribuita tramite un File di configurazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9db8127a9a43478d891d5955190bd594fb6647b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094580"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>Installare i componenti Riesecuzione distribuita tramite un file di configurazione
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il programma di installazione consente di generare un file di configurazione in base alle impostazioni predefinite del sistema e ai dati di input dell'utente. Se si specifica che si desidera installare gli strumenti di gestione, è possibile utilizzare il file di configurazione per distribuire i tre componenti Riesecuzione distribuita, ovvero lo strumento di amministrazione, il controller di Riesecuzione distribuita e il client Riesecuzione distribuita. Sono supportate le operazioni di installazione, ripristino e disinstallazione dei componenti Riesecuzione distribuita.  
  
 Il programma di installazione supporta l'utilizzo del file di configurazione solo tramite la riga di comando. L'ordine di elaborazione dei parametri durante l'utilizzo del file di configurazione viene indicato di seguito:  
  
-   Il file di configurazione sovrascrive le impostazioni predefinite in un pacchetto.  
  
-   I valori della riga di comando sovrascrivono quelli presenti nel file di configurazione.  
  
 Per altre informazioni su come usare un file di configurazione, vedere [installare SQL Server 2014 tramite un File di configurazione](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md).  
  
> [!IMPORTANT]  
>  Dopo aver installato i componenti Riesecuzione distribuita, è necessario creare regole del firewall nei computer controller e client e concedere a ogni computer client autorizzazioni nel server di destinazione. Per altre informazioni, vedere [Completare i passaggi successivi all'installazione](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
### <a name="to-generate-a-configuration-file"></a>Per generare un file di configurazione  
  
1.  Seguire l'Installazione guidata nella pagina **Inizio installazione** . Il percorso del file di configurazione viene specificato nella pagina **Inizio installazione** nella sezione relativa al percorso del file di configurazione.  
  
2.  Annullare l'installazione senza completarla per generare il file INI.  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>Per installare i componenti Riesecuzione distribuita tramite il file di configurazione  
  
-   Eseguire l'installazione tramite il prompt dei comandi e specificare il file ConfigurationFile.ini utilizzando il parametro ConfigurationFile.  
  
 **Sintassi di esempio**  
  
 Di seguito viene fornito un esempio di come specificare il file di configurazione al prompt dei comandi:  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  È necessario specificare entrambe le password nella riga di comando perché non è possibile configurarle nel file di configurazione.  
  
  
