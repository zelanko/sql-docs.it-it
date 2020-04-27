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
manager: craigg
ms.openlocfilehash: 6592d81e91e0582c79bc1a8bb1264b6ab9a7b733
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080700"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>Finestra di dialogo Impostazioni di rappresentazione (Importazione guidata tabella)
  Utilizzare la pagina **Impostazioni di rappresentazione** per specificare le credenziali che verranno utilizzate da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per la connessione all'origine dati. Per altre informazioni sulla rappresentazione delle credenziali, vedere [Impersonation &#40;SSAS Tabular&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
## <a name="options"></a>Opzioni  
 **Nome utente e password specifici di Windows**  
 Selezionare questa opzione per fare in modo che le credenziali di sicurezza di un account utente di Windows specificato vengano utilizzate dal modello tabulare.  
  
 **Nome utente**  
 Digitare il dominio e il nome dell'account utente da utilizzare Utilizzare il seguente formato:  
  
 Nome di **\\** dominio>* \<nome account utente>* * \<*  
  
 Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .  
  
 **Password**  
 Digitare la password dell'account utente che verrà utilizzata dal modello tabulare.  
  
 Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .  
  
 **Account del servizio**  
 Selezionare questa opzione per usare le credenziali di sicurezza associate al servizio [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tramite cui viene gestito il modello.  
  
## <a name="see-also"></a>Vedi anche  
 [Rappresentazione &#40;SSAS tabulare&#41;](tabular-models/impersonation-ssas-tabular.md)  
  
  
