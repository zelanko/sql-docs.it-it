---
description: Finestra di dialogo Colonne indice full-text (Visual Database Tools)
title: Finestra di dialogo Colonne indice full-text
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextcolumn
ms.assetid: a6f41c5c-d950-4d64-9e42-d062925917b6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 4670e9b18ede820b703d824f87878de24e576fc3
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034884"
---
# <a name="full-text-index-columns-dialog-box-visual-database-tools"></a>Finestra di dialogo Colonne indice full-text (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
In questa finestra di dialogo sono elencate le colonne utilizzate nell'indice full-text per la tabella aperta in Progettazione tabelle. Per accedere a tale finestra di dialogo, fare clic con il pulsante destro del mouse sulla tabella in Progettazione tabelle, scegliere **Indice full-text** e nella finestra di dialogo **Indice full-text** fare clic sull'indice con le colonne da visualizzare o modificare, nel campo **Colonne** nella griglia a destra e infine sui puntini di sospensione (**...**).  
  
## <a name="options"></a>Opzioni  
**Colonna**  
Visualizza i nomi delle colonne utilizzate nell'indice full-text. Per aggiungere una colonna, fare clic sulla prima cella vuota e selezionare la colonna desiderata nell'elenco a discesa. Risulteranno accessibili solo le colonne con tipo di dati testo o image.  
  
**Tipo di dati**  
Visualizza il tipo di dati di ogni colonna. Questa proprietà è di sola lettura. Per cambiare tipo di dati, aprire la tabella in Progettazione tabelle, fare clic sulla colonna e cambiare il tipo di dati nella scheda **Proprietà colonne** .  
  
**Tipizzato per colonna**  
Si applica solo alle colonne con tipo di dati **immagine**. Nell'elenco a discesa è possibile selezionare quali altre colonne rappresentano il tipo di dati della colonna in questione. Se tale colonna non ha un tipo di dati **immagine** , il valore sarà Nessuno.  
  
Le colonne con tipo di dati **immagine** possono contenere file di Microsoft Office (con estensione doc, xls e ppt), file di testo (con estensione txt) e file HTML (con estensione htm). Pertanto, impostando su immagine il tipo di dati della colonna, sarà possibile eseguire la ricerca full-text nel contenuto dei file.  
  
**Lingua**  
Elenca tutte le lingue disponibili. Selezionare nell'elenco a discesa la lingua appropriata per i dati inclusi nella colonna. Se, ad esempio, si utilizza un sistema operativo in lingua inglese, ma si desidera indicizzare una colonna contenente testo in lingua tedesca, selezionare l'opzione corrispondente al tedesco nell'elenco a discesa per migliorare le prestazioni dell'indice.  
  
**Semantica statistica**  
Consente di selezionare se abilitare l'indicizzazione semantica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica](../../relational-databases/search/semantic-search-sql-server.md).  
  
Se si seleziona una lingua in **Lingua** prima di selezionare **Semantica statistica**e alla lingua selezionata non è associato alcun modello di lingua semantico, la casella di controllo **Semantica statistica** è disabilitata. Se si seleziona **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella casella combinata a discesa saranno limitate a quelle per cui è disponibile un modello di lingua semantico.  
  
## <a name="see-also"></a>Vedere anche  
[Finestra di dialogo Indice full-text &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/full-text-index-dialog-box-visual-database-tools.md)  
