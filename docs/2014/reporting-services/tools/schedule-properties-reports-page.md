---
title: Proprietà pianificazione (pagina Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1ddc4ca8fa9a0d6d9a109ccb205bdd9684b2f370
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953707"
---
# <a name="schedule-properties-reports-page"></a>Proprietà pianificazione (pagina Report)
  Utilizzare questa pagina per visualizzare tutti i report che utilizzano la pianificazione condivisa. È possibile utilizzare le pianificazioni per aggiornare lo snapshot o generare la cronologia del report, attivare una sottoscrizione oppure specificare la data e l'ora di scadenza di una copia del report memorizzata nella cache. Per individuare la modalità di utilizzo della pianificazione, visualizzare le informazioni sulle proprietà e sulla sottoscrizione del report.  
  
 Anche se in questa pagina è illustrato ogni report che utilizza la pianificazione condivisa, non viene indicato quante volte la pianificazione condivisa è utilizzata all'interno di un singolo report. Si supponga, ad esempio che 20 diversi sottoscrittori del report Company Sales utilizzino tutti la stessa pianificazione condivisa per attivare l'elaborazione della sottoscrizione. In questo caso, il report Company Sales verrà indicato una sola volta nell'elenco, anche se nel report sono presenti 20 riferimenti alla pianificazione condivisa.  
  
 Per aprire questa pagina, avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi a un server di report, aprire il **pianificazioni condivise** cartella, fare clic su una pianificazione condivisa, selezionare **le proprietà**, quindi fare clic su **report** .  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="options"></a>Opzioni  
 **Cartella**  
 Consente di specificare il percorso del report.  
  
 **Report**  
 Consente di specificare il nome del report che utilizza la pianificazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Create, Modify, and Delete Schedules](../subscriptions/create-modify-and-delete-schedules.md)   
 [Pianificazioni](../subscriptions/schedules.md)   
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)   
 [Eseguire la connessione a un server di report in Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Configurare le proprietà generali per un Report &#40;gestione Report&#41;](../configure-general-properties-for-a-report-report-manager.md)  
  
  
