---
title: Finestra di dialogo Rilevate modifiche al database (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.schema.databasechangesdetected
- vdtsql.chm:65543
- vdtsql.chm:65554
ms.assetid: 91f13086-371f-46a2-9f46-804c1415f3ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6f1927d25ebbb5e93dc8ea94eb5ce4895ada000b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263885"
---
# <a name="database-changes-detected-dialog-box-visual-database-tools"></a>Finestra di dialogo Rilevate modifiche al database (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Questa finestra di dialogo viene visualizzata quando si cerca di salvare un diagramma di database o tabelle selezionate ma alcuni oggetti di database influenzati dall'operazione di salvataggio non sono aggiornati rispetto al database. Accettando le modifiche mostrate in questa finestra di dialogo si aggiorna il database in modo che corrisponda al diagramma e si sovrascrivono le modifiche di altri utenti.  
  
> [!NOTE]  
> Sebbene non sia possibile annullare le modifiche apportate a una tabella o a un diagramma di database, le modifiche non vengono salvate nel database fino a quando non si salva la tabella o il diagramma. È possibile annullare le modifiche non salvate scegliendo **No** e chiudendo tutti i diagrammi aperti senza salvarli.  
  
## <a name="options"></a>Opzioni  
**Avvisa in caso siano rilevate differenze**  
Specifica se questa finestra di dialogo verrà visualizzata la volta successiva in cui tenta di salvare un diagramma di database o le tabelle selezionate. Se questa casella di controllo è selezionata, la finestra di dialogo viene visualizzata ogni volta che si salva un diagramma o una tabella che non è aggiornata rispetto al database. Se la casella è deselezionata, la finestra di dialogo non viene visualizzata. Per impostazione predefinita, questa casella è selezionata. Se si deseleziona questa opzione, è possibile selezionarla nuovamente nella finestra di dialogo **Opzioni** .  
  
**Sì**  
Aggiorna il database con tutte le modifiche mostrate nell'elenco.  
  
**No**  
Annulla l'operazione di salvataggio.  
  
> [!NOTE]  
> Per aggiornare il diagramma in modo che corrisponda al database, chiuderlo senza salvare le modifiche, fare clic su di esso con il pulsante destro del mouse in Esplora server, scegliere Aggiorna e quindi riaprirlo.  
  
**Salva file di testo**  
Visualizza la finestra di dialogo **Salva con nome** , in cui è possibile specificare un percorso per un file di testo contenente un elenco delle modifiche del database.  
  
## <a name="see-also"></a>Vedere anche  
[Riconciliazione di un diagramma di database con un database modificato &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/reconcile-a-database-diagram-with-a-modified-database-visual-database-tools.md)  
[Ambienti multiutente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
