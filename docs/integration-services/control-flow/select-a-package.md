---
title: Seleziona pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 561495eaad4dbe41a0af05e80d3c2ba35d91cb74
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293959"
---
# <a name="select-a-package"></a>Seleziona pacchetto

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la finestra di dialogo **Seleziona pacchetto** per specificare il pacchetto da cui l'attività Message Queue può ricevere messaggi.  
  
## <a name="static-options"></a>Opzioni statiche  
 **Posizione**  
 Consente di specificare il percorso del pacchetto. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Impostare il percorso su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona questo valore vengono visualizzate le opzioni dinamiche **Server**, **Usa autenticazione di Windows**, **Usa autenticazione di SQL Server**, **Nome utente**e **Password**.|  
|File DTSX|Consente di impostare il percorso su un file DTSX. Se si seleziona questo valore viene visualizzata l'opzione dinamica **Nome file**.|  
  
## <a name="location-dynamic-options"></a>Opzioni dinamiche relative al percorso  
  
### <a name="location--sql-server"></a>Percorso = SQL Server  
 **Nome pacchetto**  
 Consente di selezionare un pacchetto archiviato nel server specificato.  
  
 **Server**  
 Consente di specificare il nome del server o di selezionarlo nell'elenco.  
  
 **Usa autenticazione di Windows**  
 Fare clic su questa opzione per utilizzare l'autenticazione di Windows.  
  
 **Usa autenticazione di SQL Server**  
 Fare clic su questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Nome utente**  
 Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare il nome utente da usare per l'accesso al server.  
  
 **Password**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare una password.  
  
### <a name="location--dtsx-file"></a>Percorso = File DTSX  
 **Nome file**  
 Specificare il percorso di un pacchetto oppure fare clic sul pulsante Sfoglia **(...)** per trovare il pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Message Queue](../../integration-services/control-flow/message-queue-task.md)  
  
  
