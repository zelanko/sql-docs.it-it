---
title: Finestra di dialogo Convalida | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackagevalidate.f1
- sql12.ssis.ssms.isprojectvalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8380b3ff1502088e0131b182149e90e31d2be42c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385999"
---
# <a name="validate-dialog-box"></a>Finestra di dialogo Convalida
  Utilizzare la finestra di dialogo **Convalida** per verificare i problemi comuni in un progetto o pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Se si è verificato un problema, viene visualizzato un messaggio nella parte superiore della finestra di dialogo. In caso contrario, viene visualizzato il termine Pronto.  
  
 **Per saperne di più**  
  
-   [Aprire la finestra di dialogo Convalida](#open_dialog)  
  
-   [Impostare le opzioni nella pagina Generale](#general)  
  
##  <a name="open_dialog"></a> Aprire la finestra di dialogo Convalida  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Espandere la cartella contenente il progetto o pacchetto che si desidera convalidare.  
  
5.  Fare clic con il pulsante destro del mouse sul pacchetto o sul progetto, quindi selezionare **Convalida**.  
  
##  <a name="general"></a> Impostare le opzioni nella pagina Generale  
 **Ambiente**  
 Selezionare l'ambiente da utilizzare per convalidare il progetto o pacchetto.  
  
 **Runtime a 32 bit**  
 Scegliere di utilizzare un runtime a 32 bit per eseguire un pacchetto.  
  
 Nella scheda **Parametri** sono elencati i valori dei parametri utilizzati per convalidare il progetto o pacchetto. Di seguito sono riportate le opzioni della scheda Parametri.  
  
 **Contenitore**  
 Viene elencato l'oggetto contenente il parametro.  
  
 **Parametro**  
 Viene elencato il nome dei parametri.  
  
 **Valore**  
 Viene elencato il valore del parametro.  
  
 Nella scheda **Gestioni connessioni** sono elencati i valori delle proprietà delle gestioni connessioni utilizzati per convalidare il progetto o pacchetto.  
  
 Di seguito sono riportate le opzioni della scheda **Gestioni connessioni** .  
  
 **Contenitore**  
 Viene elencato l'oggetto contenente la gestione connessione.  
  
 **Name**  
 Viene elencato il nome della gestione connessione.  
  
 **Nome proprietà**  
 Viene elencato il nome della proprietà della gestione connessione.  
  
 **Valore**  
 Viene elencato il valore assegnato alla proprietà della gestione connessione.  
  
  
