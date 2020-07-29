---
title: Finestra di dialogo Avvisi di convalida
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 3dd3f15ba7b6b42b95d8789d204bc44c2afb3f7d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002660"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>Finestra di dialogo Avvisi di convalida (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Questa finestra di dialogo viene visualizzata se si cerca di salvare modifiche che comportano conseguenze potenzialmente dannose o se l'operazione di commit sul database presenta molte probabilità di insuccesso. Indica quali potrebbero essere le conseguenze dannose o perché l'operazione di commit potrebbe non riuscire e consente di scegliere se procedere con la modifica o se annullare l'operazione.  
  
> [!NOTE]  
> Questa finestra di dialogo viene visualizzata quando si tenta di trasmettere le modifiche al database o quando si salva uno script delle modifiche.  
  
La finestra di dialogo può essere visualizzata per i seguenti motivi:  
  
-   Non si dispone delle autorizzazioni sul database per eseguire il commit di tutte le modifiche.  
  
-   Le modifiche danno come risultato colonne derivate generate in modo errato, vincoli predefiniti o vincoli CHECK.  
  
-   Una modifica al tipo di dati di una colonna potrebbe causare una perdita di dati.  
  
-   Una modifica porterebbe alla creazione di un indice più grande di 900 byte.  
  
-   Una modifica cambierebbe una tabella o una colonna che contribuisce a una vista associata a schema o una funzione definita dall'utente.  
  
-   Una modifica provocherebbe una nuova creazione di una tabella che ha uno o più trigger crittografati, con la conseguente eliminazione dei trigger.  
  
-   Le modifiche produrranno numerose assegnazioni di ANSI_NULLS o ANSI_PADDING o entrambi per le colonne all'interno di una tabella.  
  
## <a name="options"></a>Opzioni  
**Sì**  
Consente di procedere con l'operazione e generare lo script delle modifiche oppure di trasmettere le modifiche al database. È comunque possibile che si verifichino errori nell'operazione di commit, se non si dispone dei privilegi necessari per la modifica del database, se le modifiche comportano la creazione di un indice più grande di 900 byte oppure se le modifiche danno come risultato una colonna derivata generata in modo errato, un vincolo predefinito o un vincolo CHECK.  
  
**No**  
Annulla l'operazione di salvataggio.  
  
**Salva file di testo**  
Visualizza la finestra di dialogo **Salva con nome** , in cui è possibile specificare un percorso per un file di testo che include un elenco degli avvisi.  
  
## <a name="see-also"></a>Vedere anche  
[Progettazione di tabelle &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
