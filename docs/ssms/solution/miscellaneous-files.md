---
title: file esterni
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c4fc8fee177588824a8dd1a93dae3387056c89b2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000816"
---
# <a name="miscellaneous-files"></a>file esterni
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
I file al di fuori di un progetto vengono identificati come *file esterni*. Quando una soluzione è aperta è possibile aprire e modificare i file esterni correlati al progetto. Un file viene classificato come esterno se la sua estensione non è associata all'editor del codice del progetto. In un progetto script [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio, i file con estensione txt o mdx verranno trattati come file esterni. In un progetto MDX i file con estensione txt o sql verranno trattati come file esterni. Per associare un'estensione di file con un editor di codice, vedere [Procedura: Associazione di estensioni di file a un editor di codice](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md).  
  
La possibilità di aggiungere file esterni al progetto è utile per diverse ragioni. Un file potrebbe non essere necessariamente uno script riconosciuto e tuttavia essere parte integrante dello sviluppo della soluzione. Note o istruzioni di sviluppo, file di dati e segmenti di codice sono esempi comuni di tali file.  
  
I file esterni assicurano flessibilità. Si supponga, ad esempio, di avere un progetto script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che dispone di numerosi script per la creazione di tabelle e stored procedure nel database e di avere inoltre diversi file di dati per le tabelle con estensione BCP e le istruzioni di esecuzione in un file LEGGIMI.TXT. È possibile associare i file di dati e LEGGIMI come file esterni al progetto per sfruttare il controllo del codice sorgente e altre caratteristiche del sistema del progetto.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] I menu e le barre degli strumenti cambiano in base al formato del file aperto. Quando si apre un file di testo, ad esempio, viene visualizzata la barra degli strumenti Editor di testo. Se si apre un file di XML Schema, viene visualizzata la barra degli strumenti XML Schema. Durante la modifica di XML Schema la barra degli strumenti Editor di testo non è disponibile. Quando si passa da un file di progetto a un file esterno e viceversa, tutte le barre degli strumenti e i comandi correlati al progetto vengono sostituiti con quelli appropriati per il file esterno.  
  
## <a name="see-also"></a>Vedere anche  
[File per la gestione di soluzioni e progetti](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[Soluzioni &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Progetti &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
  
