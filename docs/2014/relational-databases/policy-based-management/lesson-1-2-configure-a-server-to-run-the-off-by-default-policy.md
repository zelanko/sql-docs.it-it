---
title: Configurare un server per l'esecuzione di criteri Disattivata per impostazione predefinita | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8beb6998d78ad9a113ce18323133de7ed39ead56
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090635"
---
# <a name="configure-a-server-to-run-the-off-by-default-policy"></a>Configurazione di un server per l'esecuzione di criteri Disattivata per impostazione predefinita
  Sono stati creati criteri denominati Disattivata per impostazione predefinita. In questa attività si verificherà se il server è conforme ai requisiti di tali criteri.  
  
### <a name="to-run-the-off-by-default-policy"></a>Per eseguire i criteri Disattivata per impostazione predefinita  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], scegliere **Criteri** e fare clic su **Valuta**.  
  
2.  Nella finestra di dialogo **Valuta criteri[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile selezionare criteri da un'altra istanza di**  o da un file. Per questo passaggio, lasciare l'opzione **Origine[!INCLUDE[ssDE](../../includes/ssde-md.md)] impostata sull'istanza del** .  
  
3.  Nella sezione **Criteri** selezionare i criteri **Off By Default** (Disattivata per impostazione predefinita).  
  
4.  Per determinare se il server è conforme ai criteri, fare clic su **Valuta**.  
  
5.  Nell'area **Risultati[!INCLUDE[ssDE](../../includes/ssde-md.md)] verrà visualizzato un cerchio verde con un segno di spunta se il**  è conforme ai criteri. Verrà visualizzato un cerchio rosso con una X se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è conforme ai criteri.  
  
6.  Se si verifica un errore, nell'area **Dettagli di destinazione** verranno visualizzate informazioni aggiuntive nella colonna **Messaggio** . Nella colonna **Messaggio** fare clic su **Visualizza** per visualizzare un report contenente i risultati della verifica per ogni proprietà facet controllata.  
  
7.  La descrizione dei criteri viene visualizzata nella parte inferiore della pagina. Nella sezione **Guida aggiuntiva** è incluso il collegamento ipertestuale configurato per i criteri. Fare clic sul collegamento ipertestuale del messaggio per aprire la pagina Web specificata quando sono stati creat i criteri.  
  
8.  Chiudere il browser e la finestra di dialogo **Visualizzazione dettagliata risultati** .  
  
9. Se il server non è conforme e si vuole disabilitare Posta elettronica database, fare clic su **Applica** nella pagina **Risultati valutazione** .  
  
10. Chiudere le due finestre di dialogo **Visualizzazione dettagliata risultati** e **Valuta criteri** .  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Creare e applicare criteri per gli standard di denominazione](lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
