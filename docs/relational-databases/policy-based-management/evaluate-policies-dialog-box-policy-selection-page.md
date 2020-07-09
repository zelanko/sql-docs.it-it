---
title: Pagina "Selezione criteri" della finestra di dialogo "Valuta criteri"
description: Descrive la pagina "Selezione criteri" della finestra di dialogo "Valuta criteri" per la gestione basata su criteri in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f82a5b8760710f0d72554e1f0b5b083ccd58294c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749427"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>Finestra di dialogo Valuta criteri, pagina Selezione criteri
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare questa finestra di dialogo per valutare criteri della gestione basata su criteri. Selezionando la pagina **Risultati valutazione** , è possibile applicare criteri agli elementi non conformi ai criteri inclusi in un set di destinazioni.  
  
## <a name="options"></a>Opzioni  
 **Origine**  
 Specifica l'origine dei criteri. Per modificare l'origine, fare clic sul pulsante Sfoglia ( **...** ) per aprire la finestra di dialogo **Seleziona origine** .  
  
 **File**  
 Digitare il percorso o usare il pulsante Sfoglia ( **...** ) per selezionare un file che contiene i criteri della gestione basata su criteri.  
  
 **Server**  
 Selezionare questa opzione per eseguire una connessione a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che contiene i criteri desiderati.  
  
 **Criteri: Criteri**  
 Fare clic su questa opzione per aprire la finestra di dialogo relativa ai criteri specificati.  
  
 **Criteri: Categoria**  
 Categoria dei criteri. Il contenuto di questa casella è di sola lettura.  
  
 **Criteri: Facet**  
 Facet implementato dai criteri. Il contenuto di questa casella è di sola lettura.  
  
 **Valuta**  
 Esegue i criteri in modalità di valutazione. Verrà generato un report sulla conformità per il set di destinazioni, ma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verrà riconfigurato, né verrà applicata la conformità successiva.  
  
## <a name="possible-errors"></a>Possibili errori  
  
-   **Impossibile trovare destinazioni**  
  
     È possibile che il set di destinazioni sia vuoto a causa di uno dei motivi seguenti:  
  
    -   Non sono disponibili destinazioni nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del tipo specificato dai criteri.  
  
    -   È possibile che la restrizione server escluda l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che contiene la destinazione.  
  
    -   Se i criteri riguardano un oggetto di un database, ad esempio una tabella, una vista o un utente, è possibile che il database non sottoscriva la categoria dei criteri.  
  
    -   È possibile che il filtro del set di destinazioni escluda tutte le destinazioni nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Il tipo di server di destinazione è diverso dal tipo di server in cui vengono valutati i criteri. Se, ad esempio, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)]si tenta di valutare i criteri creati per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], si riceverà un set di destinazioni vuoto.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Finestra di dialogo Valuta criteri, pagina Risultati valutazione](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
