---
title: Finestra di dialogo informazioni di rappresentazione (importazione guidata tabella) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.impersonationinfo.f1
ms.assetid: bee7eee5-0650-41f1-a372-5076ae97a58c
author: minewiskan
ms.author: owend
ms.openlocfilehash: b29901213da4653c2d8867b9f450b359c39bded3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544254"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>Finestra di dialogo Impostazioni di rappresentazione (Importazione guidata tabella)
  Utilizzare la pagina **Impostazioni di rappresentazione** per specificare le credenziali che verranno utilizzate da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per la connessione all'origine dati. Per altre informazioni sulla rappresentazione delle credenziali, vedere [Impersonation &#40;SSAS Tabular&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
## <a name="options"></a>Opzioni  
 **Nome utente e password specifici di Windows**  
 Selezionare questa opzione per fare in modo che le credenziali di sicurezza di un account utente di Windows specificato vengano utilizzate dal modello tabulare.  
  
 **Nome utente**  
 Digitare il dominio e il nome dell'account utente da utilizzare Utilizzare il seguente formato:  
  
 *\<Domain name>* **\\** *\<User account name>*  
  
 Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .  
  
 **Password**  
 Digitare la password dell'account utente che verrà utilizzata dal modello tabulare.  
  
 Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .  
  
 **Account di servizio**  
 Selezionare questa opzione per usare le credenziali di sicurezza associate al servizio [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tramite cui viene gestito il modello.  
  
## <a name="see-also"></a>Vedere anche  
 [Rappresentazione &#40;SSAS tabulare&#41;](tabular-models/impersonation-ssas-tabular.md)  
  
  
