---
title: Pagina Autorizzazioni o Entità a sicurezza diretta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.common.permissions.f1
- sql12.swb.SecurableAndEffectPermissions.f1
- sql12.swb.availabilitygroupproperties.permission.f1
- sql12.swb.common.columnperm.f1
- sql12.swb.SecurableAndEffectivePermission.f1
ms.assetid: b3bf077a-bec2-4161-ac0c-460586199906
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c83d92da6708c8c63e1ba4c2cea60b1497a54883
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284551"
---
# <a name="permissions-or-securables-page"></a>Pagina Autorizzazioni o Entità a sicurezza diretta
  Usare la pagina **Autorizzazioni** o la pagina **Entità a protezione diretta** per visualizzare o impostare le autorizzazioni per le entità a protezione diretta. È possibile accedere a questa pagina da diversi tipi di oggetti. Il contenuto della pagina può modificare leggermente, in base alle modalità in cui la pagina è aperta e al contenuto. Quando la pagina viene visualizzata, la griglia superiore della pagina potrebbe contenere alcuni elementi o potrebbe essere vuota. Per aggiungere elementi alla griglia superiore, fare clic su **Cerca**. Selezionare un elemento in tale griglia, quindi impostare le autorizzazioni appropriate nella scheda **Esplicita** . Per visualizzare autorizzazioni aggregate, usare la scheda **Valide**.  
  
 Per comprendere le possibili combinazioni di entità a protezione diretta ed entità, vedere i collegamenti relativi alla sintassi specifica delle entità a protezione diretta nell'argomento [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql). Per altre informazioni, vedere [Entità a protezione diretta](securables.md).  
  
## <a name="page-header"></a>Intestazione di pagina  
 L'intestazione della pagina **Autorizzazioni** o **Entità a protezione diretta** dipende dall'entità a protezione diretta o dall'entità. Vengono visualizzate informazioni significative sull'elemento, ad esempio il nome.  
  
## <a name="upper-grid"></a>Griglia superiore  
 La griglia superiore include uno o più elementi per i quali è possibile impostare le autorizzazioni. In questa finestra di dialogo è disponibile un pulsante **Cerca** che consente di selezionare oggetti o entità da aggiungere alla griglia superiore. Nel nome della griglia potrebbe essere visualizzato **Entità a protezione diretta** oppure uno o più tipi di entità o di entità a protezione diretta. Le colonne visualizzate nella griglia superiore variano a seconda del tipo di entità o di entità a sicurezza diretta.  
  
 **Name**  
 Nome di ogni entità o entità a sicurezza diretta aggiunto alla griglia.  
  
 **Tipo**  
 Descrive il tipo di ogni elemento.  
  
## <a name="explicit-tab"></a>Scheda Esplicita  
 Nella scheda **Esplicita** sono elencate le possibili autorizzazioni per l'entità a protezione diretta selezionate nella griglia superiore. Per configurare le autorizzazioni, selezionare o deselezionare le caselle di controllo **Concedi** (o **Consenti**), **Con diritto di concessione**e **Nega** . Le opzioni effettivamente disponibili dipendono dall'autorizzazione esplicita in questione.  
  
 **Autorizzazioni**  
 Nome dell'autorizzazione.  
  
 **Utente che concede le autorizzazioni**  
 Entità che ha concesso l'autorizzazione.  
  
 **Concedi**  
 Selezionare questa opzione per concedere l'autorizzazione all'account di accesso, deselezionarla per revocare l'autorizzazione.  
  
 **Con diritto di concessione**  
 Riflette lo stato dell'opzione WITH GRANT relativo all'autorizzazione elencata. Il contenuto di questa casella è di sola lettura. Per applicare questa autorizzazione, utilizzare l'istruzione [GRANT](/sql/t-sql/statements/grant-transact-sql) .  
  
 **Nega**  
 Selezionare questa opzione per negare l'autorizzazione all'account di accesso, deselezionarla per revocare l'autorizzazione.  
  
 **Autorizzazioni colonna**  
 Per oggetti che contengono colonne, ad esempio tabelle, viste o funzioni con valori di tabella, il pulsante **Autorizzazioni colonna** consente di visualizzare la finestra di dialogo **Autorizzazioni colonna** . In questa finestra di dialogo è possibile impostare le autorizzazioni **Concedi**, **Consenti**o **Nega** in colonne singole di una tabella o di una vista. Questa opzione non è disponibile per tutti i tipi di oggetti o tutte le autorizzazioni.  
  
## <a name="effective-tab"></a>Scheda Valide  
 Le autorizzazioni di un'entità correlate a quelle di un'entità a sicurezza diretta possono derivare da autorizzazioni impostate per numerose entità diverse. A un account di accesso, ad esempio, potrebbero essere concesse autorizzazioni sia a livello individuale che come appartenente a un gruppo. Nella scheda **Valide** viene visualizzato il risultato della combinazione di autorizzazioni esplicite e di quelle ricevute in base all'appartenenza a un gruppo oppure a un ruolo. Le autorizzazioni concesse vengono aggregate. Un'autorizzazione negata ha la priorità su tutte le autorizzazioni concesse.  
  
 **Autorizzazioni**  
 Nome dell'autorizzazione.  
  
 **Colonna**  
 Nomi delle colonne interessate dall'autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli a livello di database](authentication-access/database-level-roles.md)   
 [Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
